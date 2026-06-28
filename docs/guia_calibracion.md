# 🎯 Guía de Calibración — UGR-A20M

Guía paso a paso para calibrar la impresora desde cero tras completar la Fase 1.  
Seguir los pasos **en el orden indicado**; cada calibración depende de la anterior.

---

## Requisitos previos

Antes de empezar, verificar:

- [ ] Klipper arranca sin errores en Fluidd/Mainsail
- [ ] El serial del MCU está correctamente configurado en `printer.cfg`
- [ ] Todos los motores responden y se mueven en la dirección correcta
- [ ] Los endstops X e Y se activan al pulsar (`QUERY_ENDSTOPS`)
- [ ] El CR-Touch despliega y recoge la sonda correctamente
- [ ] Los termistores leen temperaturas coherentes (±5 °C de la temperatura ambiente)

---

## Paso 1 — Verificar dirección de motores

Mover cada eje 10 mm desde Fluidd y comprobar que la dirección es la esperada.

```
# En la consola de Klipper:
G28 X    # Homing solo X — verificar que el carro va hacia el endstop
G28 Y    # Homing solo Y
```

Si algún eje se mueve en sentido contrario, añadir o quitar el `!` en el `dir_pin` correspondiente en `printer.cfg`.

---

## Paso 2 — Calibrar rotation_distance del extrusor

La `rotation_distance` determina cuánto filamento mueve el extrusor por cada vuelta del motor. Un valor incorrecto causa sub o sobre-extrusión.

### Procedimiento

1. Calentar el hotend a 200 °C (`PREHEAT_PLA` y esperar)
2. Cargar filamento hasta que salga por la boquilla (`LOAD_FILAMENT`)
3. Cortar el filamento a ras de la entrada del extrusor
4. Marcar el filamento con un rotulador a exactamente **100 mm** de la entrada
5. Ejecutar en la consola:
   ```
   G91
   G1 E100 F150
   G92 E0
   G90
   ```
6. Medir la distancia desde la entrada del extrusor hasta la marca
7. Calcular el valor correcto:
   ```
   rotation_distance_nuevo = rotation_distance_actual × distancia_real / 100
   ```
8. Actualizar `rotation_distance` en `printer.cfg` y repetir hasta error < 1 %

### Valores de referencia

| Extrusor | rotation_distance inicial | gear_ratio |
|----------|--------------------------|------------|
| Sharkfin + BMG Clone | 22.67 | 50:17 |

---

## Paso 3 — Calibrar PID del hotend

El control PID mantiene la temperatura estable durante la impresión. Sin calibrar, la temperatura puede oscilar ±5–10 °C.

```
CALIBRATE_PID_HOTEND TEMP=220
```

Klipper calentará y enfriará el hotend varias veces de forma automática. En la consola de Fluidd se verán líneas como:
```
// PID Autotune: Try 1
// PID Autotune: Try 2
...
// PID parameters: pid_Kp=XX.XX pid_Ki=X.XX pid_Kd=XXX.XX
```

El proceso **ha terminado** cuando aparece la línea con `pid_Kp`, `pid_Ki` y `pid_Kd`. Dura entre 8 y 15 minutos según la masa térmica del hotend. Al finalizar, guardar:

```
SAVE_CONFIG
```

> Klipper se reiniciará automáticamente y escribirá los valores de PID al final del `printer.cfg` en el bloque `#*# SAVE_CONFIG`.

### Temperatura de calibración por material

| Material | Temperatura de calibración recomendada |
|----------|----------------------------------------|
| PLA | 200 °C |
| PETG | 235 °C |
| ABS / ASA | 250 °C |

Calibrar a la temperatura más alta que se vaya a usar habitualmente.

---

## Paso 4 — Calibrar PID de la cama

```
CALIBRATE_PID_BED TEMP=60
```

Esperar 10–15 minutos y guardar:

```
SAVE_CONFIG
```

---

## Paso 5 — Medir offsets del CR-Touch

Los offsets definen la posición del CR-Touch relativa al nozzle. Un valor incorrecto desplaza el mesh respecto a la zona real de impresión, provocando que los bordes de la cama queden sin medir.

### Medición con calibre

Con el toolhead instalado en el carro X y la impresora **apagada**, llevar el carro manualmente al centro del eje X para tener acceso cómodo:

```
Vista desde arriba del toolhead:

  [CR-Touch]          [Nozzle]
       │                  │
       ←── x_offset (─) ──→
       │                  │
       └──── y_offset ────┘
              (─ si sonda
              detrás del nozzle)
```

1. **x_offset** — distancia horizontal entre el centro del pin del CR-Touch y el centro del nozzle.
   - CR-Touch a la **izquierda** del nozzle → valor **negativo** (caso habitual con Mini Stealth probe-mount left)
   - CR-Touch a la **derecha** → valor positivo

2. **y_offset** — distancia en profundidad entre el pin y el nozzle.
   - CR-Touch **por detrás** del nozzle → valor **negativo**

3. Actualizar en `printer.cfg`:
   ```ini
   [bltouch]
   x_offset: -44    # ← reemplazar con tu medición real
   y_offset: -9     # ← reemplazar con tu medición real
   ```

4. Actualizar `mesh_min` y `mesh_max` en `[bed_mesh]` para que la sonda nunca salga de la cama:
   ```ini
   [bed_mesh]
   mesh_min: 15, 15      # mínimo: |x_offset| + 5 mm de margen en X
   mesh_max: 210, 245    # máximo: 255 - |y_offset| - 5 mm en Y
   ```

> Los valores del proyecto (`x_offset: -44`, `y_offset: -9`) son estimaciones para el Mini Stealth v2 con probe-mount izquierdo. Siempre medir físicamente — varían según la variante de shroud impresa.

---

## Paso 6 — Nivelar tornillos de cama

Antes de calibrar el z_offset, la cama debe estar lo más plana posible físicamente. Klipper mide los cuatro tornillos y calcula cuánto girar cada uno.

```
LEVEL_BED_SCREWS
```

Klipper ejecuta `G28` y luego `SCREWS_TILT_CALCULATE`. Para cada tornillo mostrará en pantalla cuánto girarlo y en qué dirección (por ejemplo, `00:20 en sentido horario`). Repetir hasta que todos los tornillos muestren una diferencia **< 0.1 mm** entre sí.

> **¿Por qué antes del z_offset?** El z_offset se mide en el centro de la cama. Si la cama está inclinada, el z_offset medido no será representativo de toda la superficie. Nivelar primero garantiza un z_offset más estable.

---

## Paso 7 — Calibrar z_offset (altura de primera capa)

El z_offset determina a qué altura queda el nozzle cuando el CR-Touch indica que ha tocado la cama. Un valor incorrecto arruina la primera capa.

```
CALIBRATE_Z_OFFSET
```

Esto ejecuta `G28` y luego `PROBE_CALIBRATE`. Usar el método del papel:

1. Colocar un folio de papel estándar (80 g/m²) entre el nozzle y la cama en el centro
2. Bajar con `TESTZ Z=-0.1` hasta notar resistencia leve al mover el papel
3. El papel debe moverse con algo de fricción pero sin rasgarse
4. Cuando la resistencia sea correcta: `ACCEPT`
5. Guardar: `SAVE_CONFIG`

### Referencia visual de primera capa

| Aspecto al imprimir | Diagnóstico | Corrección |
|---------------------|-------------|-----------|
| Líneas separadas, no se pegan entre sí | Demasiado alto | `TESTZ Z=-0.05` → `ACCEPT` → `SAVE_CONFIG` |
| Líneas bien adheridas, brillantes, sin espacios | ✅ Correcto | — |
| Líneas aplastadas, boquilla rasca la cama | Demasiado bajo | `TESTZ Z=+0.05` → `ACCEPT` → `SAVE_CONFIG` |

> Si se cambia la temperatura de la cama o el cristal, recalibrar el z_offset — la expansión térmica modifica la altura.

---

## Paso 8 — Generar mesh de nivelación

```
GENERATE_MESH
```

Genera una malla 5×5 (25 puntos) de la superficie de la cama y la guarda como perfil `default`. Este mesh se carga automáticamente en cada `START_PRINT`.

Para ver el mesh en Fluidd: pestaña **Heightmap**.

---

## Paso 9 — Calibrar Pressure Advance

El Pressure Advance compensa el retraso del hotend al cambiar de velocidad, mejorando las esquinas y reduciendo el stringing.

```
PRESSURE_ADVANCE_TOWER
```

### Procedimiento

1. Imprimir un cubo o torre sencilla con la macro activada
2. Observar las esquinas de la torre: buscar la altura donde las esquinas están más nítidas y sin bultos
3. Calcular el valor: `PA = altura_en_mm × 0.005`
4. Actualizar en `printer.cfg`:
   ```ini
   pressure_advance: 0.05    # ← tu valor calculado
   ```

### Valores de referencia por material

| Material | PA típico (direct drive) |
|----------|--------------------------|
| PLA | 0.04–0.07 |
| PETG | 0.06–0.10 |
| ABS / ASA | 0.03–0.06 |
| TPU | 0.00–0.02 |

---

## Paso 10 — Input Shaping (opcional)

El Input Shaping reduce las vibraciones del chasis que producen ringing (ondas en las paredes de la pieza), permitiendo imprimir más rápido con mejor calidad.

Requiere conectar un acelerómetro **ADXL345** a la SKR Mini E3 V3 y descomentar la sección 13 de `printer.cfg`.

```
SHAPER_CALIBRATE
SAVE_CONFIG
```

Tras calibrar, la velocidad máxima puede aumentarse hasta 250–300 mm/s dependiendo del resultado.

---

## Checklist de calibración completa

| Paso | Acción | Estado |
|------|--------|--------|
| 1 | Dirección de motores verificada | ⬜ |
| 2 | rotation_distance calibrado (error < 1 %) | ⬜ |
| 3 | PID hotend calibrado y guardado | ⬜ |
| 4 | PID cama calibrado y guardado | ⬜ |
| 5 | Offsets CR-Touch medidos y actualizados | ⬜ |
| 6 | Tornillos de cama nivelados (diferencia < 0.1 mm) | ⬜ |
| 7 | z_offset calibrado y guardado | ⬜ |
| 8 | Mesh de nivelación generado y guardado | ⬜ |
| 9 | Pressure Advance calibrado | ⬜ |
| 10 | Input Shaping calibrado (opcional — requiere ADXL345) | ⬜ |

---

---

> Para una guía completa de diagnóstico y solución de problemas ver [`docs/troubleshooting.md`](troubleshooting.md).
