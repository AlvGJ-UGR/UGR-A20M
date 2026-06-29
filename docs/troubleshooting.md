# 🔧 Troubleshooting — UGR-A20M

Guía centralizada de problemas frecuentes, organizada por subsistema. Cada problema incluye causa probable y solución paso a paso.

> Para problemas de calibración (PID, z_offset, rotation_distance...) ver también [`docs/guia_calibracion.md`](guia_calibracion.md).

---

## 🖥️ Klipper y conexión MCU

### `MCU Unable to connect` al arrancar Klipper

**Causa más frecuente:** el serial del MCU en `printer.cfg` es incorrecto o la SKR no está reconocida por la Orange Pi.

**Solución:**
```bash
# En la Orange Pi por SSH:
ls /dev/serial/by-id/
# Si no aparece nada → el cable USB no está bien o el flash de Klipper falló
# Si aparece → copiar la ruta completa y actualizar [mcu] serial: en printer.cfg
```

Si el serial existe pero Klipper sigue fallando, verificar que el firmware se flasheó correctamente: la microSD de la SKR debe tener el archivo renombrado a `firmware.cur` tras el arranque.

---

### Fluidd no carga en el navegador

| Síntoma | Causa | Solución |
|---------|-------|----------|
| Página en blanco o "Connection refused" | Moonraker o Fluidd no están corriendo | `sudo systemctl status moonraker fluidd` |
| "Klipper not connected" en Fluidd | Serial incorrecto o Klipper caído | Revisar serial; `sudo systemctl restart klipper` |
| IP de la Orange Pi no accesible | La OPi cambió de IP por DHCP | Usar `nmap -sn 192.168.1.0/24` para encontrarla; asignar IP fija en el router |

---

### Klipper muestra errores de configuración al arrancar

Leer el mensaje completo en el log de Fluidd (sección "Logs"). Los errores más frecuentes:

| Error | Causa | Solución |
|-------|-------|----------|
| `Option 'serial' in section 'mcu'...` | Serial vacío o con placeholder | Actualizar con el serial real |
| `Unknown pin chip name 'PC14'` | Placa incorrecta en la compilación | Recompilar Klipper con STM32G0B1 |
| `Pin ... is not valid` | `printer.cfg` de otra placa | Usar el `printer.cfg` del proyecto sin modificar los pin_names |

---

## 🌡️ Temperatura y calentadores

### Temperatura del hotend muestra 0 °C, -14 °C o valor absurdo

**Causas posibles:**
1. Termistor en conector equivocado (TH0 ↔ THB invertidos)
2. Cable del termistor suelto o roto
3. Tipo de termistor incorrecto en `printer.cfg`

**Verificación:**
- Con la impresora fría, ambos termistores deben leer ~temperatura ambiente (±5 °C)
- Si TH0 lee la temperatura de la cama → termistores intercambiados
- Si lee -14 °C → circuito abierto (cable roto o no conectado)

**Tipos de termistor correctos:**
```ini
# CHC V6 Volcano:
sensor_type: Generic 3950

# Cama caliente Geeetech A20M:
sensor_type: EPCOS 100K B57560G104F
```

---

### Hotend no alcanza la temperatura objetivo / tarda demasiado

| Síntoma | Causa probable | Solución |
|---------|---------------|----------|
| Se queda a ~5 °C del objetivo oscilando | PID no calibrado | `CALIBRATE_PID_HOTEND TEMP=220` → `SAVE_CONFIG` |
| Muy lento (>3 min para 200 °C) | Voltaje de la fuente bajo o calentador defectuoso | Medir voltaje en HE0: debe ser ~24V |
| Error `Heating failed` | No alcanza objetivo en el tiempo límite | PID descalibrado o calentador dañado |
| Temperatura oscila ±10 °C | PID descalibrado | Recalibrar PID |

---

### Error `Extruder not heating at expected rate`

Klipper cancela el calentamiento si la temperatura no sube al ritmo esperado. Causas:

1. **PID muy desajustado** → ejecutar `CALIBRATE_PID_HOTEND`
2. **Ventilador hotend soplando demasiado frío** → el ventilador 2510 solo debe activarse con el hotend caliente; verificar la sección `[heater_fan]`
3. **Calentador de 12V conectado a 24V** → el CHC V6 debe ser de 24V; verificar la etiqueta

---

## 🔩 Motores y movimiento

### Motor X/Y/Z se mueve en dirección contraria

Añadir o quitar el `!` en el `dir_pin` del motor afectado en `printer.cfg`. Ver procedimiento completo en [`docs/guia_calibracion.md`](guia_calibracion.md) — Paso 1.

---

### Pérdida de pasos (el cabezal se desplaza de su posición)

| Causa probable | Cómo detectarlo | Solución |
|---------------|----------------|----------|
| Velocidad demasiado alta | Solo ocurre a alta velocidad | Reducir `max_velocity` en `[printer]` |
| `run_current` demasiado bajo | Motor caliente + pérdidas | Subir `run_current` en `[tmc2209]` (máx. ~0.85A para NEMA 17 estándar) |
| Correa GT2 floja | Sonido flojo, holgura visible | Tensar la correa hasta ~50 Hz midiendo con app de afinador de guitarra o Gates Carbon Drive |
| Obstrucción mecánica | El eje roza o tiene fricción | Verificar que las guías o barras están limpias y lubricadas |

---

### Motor extrusor hace "click-click" (patina)

El extrusor no puede empujar el filamento. Causas por orden de probabilidad:

1. **Temperatura del hotend demasiado baja** — el filamento no funde lo suficiente. Subir 5–10 °C.
2. **Obstrucción en la boquilla** — hacer un cold pull o sustituir la boquilla.
3. **Tensión del latch del Sharkfin insuficiente** — apretar el tornillo de tensión.
4. **`run_current` bajo** — subir a 0.70–0.75A en `[tmc2209 extruder]`.
5. **Velocidad de extrusión demasiado alta** — reducir el caudal volumétrico máximo en el slicer.

---

## 📡 CR-Touch y nivelación

### Error `Probe triggered prior to movement`

El CR-Touch detecta que la sonda ya está activa antes de moverse. Causas:

1. **z_offset demasiado negativo** — el nozzle está por debajo de la cama. Ejecutar `PROBE_CALIBRATE` y ajustar con `TESTZ Z=+0.5`.
2. **Sonda defectuosa** — el CR-Touch no retrae correctamente. Probar con `BLTOUCH_DEBUG COMMAND=reset`.
3. **Conexión incorrecta** — verificar el cable según [`hardware/electronica/esquema_conexiones.md`](../hardware/electronica/esquema_conexiones.md).

---

### CR-Touch no despliega la sonda (`pin_down` no responde)

```bash
# Probar manualmente desde la consola de Klipper:
BLTOUCH_DEBUG COMMAND=pin_down
BLTOUCH_DEBUG COMMAND=pin_up
BLTOUCH_DEBUG COMMAND=self_test
```

Si no responde: verificar el pin de control (`PA1` en la SKR Mini E3 V3) y que el conector BLTouch está en el orden correcto: GND · 5V · SENSOR · SERVO.

---

### Error `BLTouch not deployed` durante el homing

Klipper intenta medir con el CR-Touch pero la sonda no ha bajado. Causas:

1. **Pin `control_pin` incorrecto** — debe ser `PA1` para la SKR Mini E3 V3
2. **Tensión insuficiente en el pin de servo** — algunos CR-Touch clónicos necesitan 5V en el servo; verificar que el pin BLTouch de la SKR suministra 5V
3. **CR-Touch en estado de error** — la luz parpadea en rojo. Ejecutar `BLTOUCH_DEBUG COMMAND=reset` y volver a intentarlo
4. **Velocidad de homing Z demasiado alta** — reducir `homing_speed` en `[stepper_z]` a 5 mm/s e intentar de nuevo

---

### El mesh de nivelación tiene variaciones > 1 mm

Una variación tan grande indica un problema físico, no de calibración:

1. **Cama no nivelada** — ejecutar `SCREWS_TILT_CALCULATE` y ajustar los tornillos físicamente hasta que la diferencia sea < 0.1 mm entre esquinas.
2. **Cama combada** — sustituir el cristal o añadir una lámina de aluminio bajo la cama.
3. **Offsets del CR-Touch incorrectos** — medir físicamente con calibre y actualizar `x_offset` / `y_offset`.

---

## 🧵 Calidad de impresión

### Stringing excesivo (hilos entre partes separadas)

Con extrusión directa el stringing debe ser mínimo. Si persiste:

| Causa | Solución |
|-------|---------|
| Pressure Advance no calibrado | Ejecutar `PRESSURE_ADVANCE_TOWER` y calibrar |
| Retracción demasiado corta | Aumentar a 1.0–1.5 mm (direct drive) |
| Temperatura del hotend demasiado alta | Bajar 5 °C hasta eliminar el stringing |
| Z-hop excesivo (deja más tiempo para rezumar) | Reducir z-hop a 0.2 mm |

---

### Primera capa no se adhiere / se levanta

| Causa | Solución |
|-------|---------|
| z_offset demasiado alto | `PROBE_CALIBRATE` → `TESTZ Z=-0.05` hasta que la capa quede aplastada |
| Cama sucia | Limpiar con IPA al 90% |
| Temperatura de cama baja | PLA: 60–65 °C; ABS: 100–105 °C |
| Velocidad de primera capa alta | Reducir a 20–25 mm/s en el slicer |

---

### Ondas en las paredes verticales (ringing / ghosting)

El ringing aparece como ondas en las paredes después de una esquina. Causas:

1. **Sin Input Shaping calibrado** — es la solución principal. Conectar ADXL345 y ejecutar `SHAPER_CALIBRATE`.
2. **Aceleración demasiado alta** — reducir `max_accel` a 1500 mm/s² temporalmente.
3. **Correas flojas** — tensionar hasta ~50 Hz.
4. **Guías o barras con juego** — (Fase 2: guías MGN12H eliminan este problema).

---

### Sobre-extrusión (capas demasiado gruesas, relleno desbordado)

```
rotation_distance_nuevo = rotation_distance_actual × distancia_real / 100
```

Si la extrusión está calibrada y sigue habiendo sobre-extrusión: bajar el multiplicador de flujo al 95% en el slicer y ajustar desde ahí.

---

### Sub-extrusión (relleno con huecos, capas débiles)

Verificar en orden:
1. `rotation_distance` calibrado — ver [`docs/guia_calibracion.md`](guia_calibracion.md) Paso 2
2. Temperatura del hotend suficiente — subir 5 °C y volver a probar
3. Boquilla no obstruida — hacer cold pull (procedimiento en [`docs/mantenimiento.md`](mantenimiento.md))
4. El extrusor no patina — ver troubleshooting de patinado más arriba
5. Tubo PTFE recto y sin dobleces — en direct drive debe ser ~10 mm y perfectamente recto

---

## 🖨️ Piezas impresas (ABS/ASA)

### Warping en piezas de ABS

| Causa | Solución |
|-------|---------|
| Sin recinto cerrado | Usar una caja improvisada (cartón, IKEA Lack) |
| Cama fría | ABS: 100–105 °C; calentar 10 min antes de imprimir |
| Sin brim | Añadir brim de 5–8 mm en el slicer |
| Corrientes de aire | Cerrar ventanas y puertas de la habitación |
| Primera capa demasiado fría | Subir temperatura de primera capa 5 °C |
| Apertura del recinto durante la impresión | Con hotends de alto caudal (CHC V6 Volcano) la masa térmica es mayor y el enfriamiento brusco al abrir el recinto provoca microwarping en capas intermedias; no abrir el recinto durante la impresión de ABS/ASA |

---

### Delaminación entre capas (piezas débiles en ABS)

1. Temperatura del hotend demasiado baja — ABS necesita 245–255 °C para buena adhesión entre capas
2. Velocidad demasiado alta — reducir a 40–50 mm/s
3. Refrigeración excesiva — desactivar completamente el ventilador de capa para ABS

---

## 🔗 Recursos adicionales

- [Klipper — Troubleshooting oficial](https://www.klipper3d.org/FAQ.html)
- [Klipper — Config checks](https://www.klipper3d.org/Config_checks.html)
- [Ellis' Print Tuning Guide (referencia en inglés)](https://ellis3dp.com/Print-Tuning-Guide/)
- [Reportar un error en este proyecto](https://github.com/AlvGJ-UGR/UGR-A20M/issues/new?template=bug_report.md)
