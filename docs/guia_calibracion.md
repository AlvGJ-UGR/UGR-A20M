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

Esperar a que el proceso termine (10–15 minutos). Al finalizar:

```
SAVE_CONFIG
```

> La impresora se reiniciará. Los valores se guardan automáticamente al final de `printer.cfg`.

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

Los offsets definen la distancia física entre el pin del CR-Touch y el centro del nozzle.

### Método con calibre

1. Con la impresora apagada, medir con calibre:
   - **x_offset**: distancia horizontal (eje X) entre el pin del CR-Touch y el nozzle. Negativo si la sonda está a la izquierda del nozzle.
   - **y_offset**: distancia en profundidad (eje Y). Negativo si la sonda está por detrás.

2. Actualizar en `printer.cfg`:
   ```ini
   [bltouch]
   x_offset: -44    # ← tu valor medido
   y_offset: -9     # ← tu valor medido
   ```

3. Verificar que `mesh_min` y `mesh_max` en `[bed_mesh]` compensan estos offsets para que la sonda no salga de la cama durante el mesh.

---

## Paso 6 — Calibrar z_offset (altura de primera capa)

El z_offset determina a qué altura queda el nozzle cuando el CR-Touch indica que ha tocado la cama. Un valor incorrecto arruina la primera capa.

```
CALIBRATE_Z_OFFSET
```

Esto ejecuta `G28` y luego `PROBE_CALIBRATE`. Usar el método del papel:

1. Colocar un folio de papel entre el nozzle y la cama
2. Ajustar con los comandos `TESTZ Z=-0.1` (bajar) o `TESTZ Z=+0.1` (subir)
3. Cuando el papel tenga resistencia leve al deslizar: `ACCEPT`
4. Guardar: `SAVE_CONFIG`

### Referencia visual de primera capa

| Aspecto | Diagnóstico | Corrección |
|---------|-------------|-----------|
| Líneas separadas, no se pegan | Demasiado alto | `TESTZ Z=-0.05` (más negativo) |
| Líneas bien adheridas y brillantes | ✅ Correcto | — |
| Líneas aplastadas, boquilla rasca | Demasiado bajo | `TESTZ Z=+0.05` (más positivo) |

---

## Paso 7 — Nivelar tornillos de cama

Aunque el CR-Touch compensa la inclinación de la cama, es mejor empezar con la cama lo más plana posible.

```
LEVEL_BED_SCREWS
```

Klipper medirá los cuatro tornillos y mostrará cuánto girar cada uno (en horas de reloj). Repetir hasta que todos los tornillos muestren una diferencia < 0.1 mm.

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
| 6 | z_offset calibrado y guardado | ⬜ |
| 7 | Tornillos de cama nivelados (< 0.1 mm diferencia) | ⬜ |
| 8 | Mesh de nivelación generado y guardado | ⬜ |
| 9 | Pressure Advance calibrado | ⬜ |
| 10 | Input Shaping calibrado (opcional) | ⬜ |

---

## Solución de problemas frecuentes

| Síntoma | Causa probable | Solución |
|---------|---------------|----------|
| Error `MCU unable to connect` | Serial incorrecto | `ls /dev/serial/by-id/` y actualizar `printer.cfg` |
| Temperatura del hotend oscila ±5 °C | PID sin calibrar | Ejecutar `CALIBRATE_PID_HOTEND` |
| Primera capa no se adhiere | z_offset muy alto | `CALIBRATE_Z_OFFSET` y ajustar más abajo |
| CR-Touch error `probe triggered prior to movement` | z_offset muy bajo o sonda defectuosa | Ajustar z_offset; verificar conexión sonda |
| Motor X/Y va en dirección contraria | dir_pin incorrecto | Añadir/quitar `!` en `dir_pin` del motor afectado |
| Extrusor pierde pasos | run_current bajo o velocidad alta | Subir `run_current` en el TMC2209 del extrusor |
| Stringing excesivo | PA bajo o retracción insuficiente | Subir `pressure_advance`; ajustar retracción en slicer |
| Ondas en las paredes (ringing) | Vibraciones del chasis | Calibrar Input Shaping |
