# 🖨️ Configuración del slicer — UGR-A20M

Perfiles de referencia para **OrcaSlicer** y **PrusaSlicer** adaptados a la build UGR-A20M (Fase 1: extrusor directo Sharkfin + CHC V6 Volcano + Mini Stealth v2).

> Estos valores son puntos de partida. Ajustar según el filamento y la marca concreta.

---

## Configuración de máquina

### Start G-code

```gcode
START_PRINT BED_TEMP=[first_layer_bed_temperature] EXTRUDER_TEMP=[first_layer_temperature]
```

> En **Cura** usar:
> ```gcode
> START_PRINT BED_TEMP={material_bed_temperature_layer_0} EXTRUDER_TEMP={material_print_temperature_layer_0}
> ```

### End G-code

```gcode
END_PRINT
```

### Dimensiones de la impresora

| Parámetro | Valor |
|-----------|-------|
| Volumen X | 255 mm |
| Volumen Y | 255 mm |
| Volumen Z | 255 mm |
| Origen | Esquina (0, 0) |
| Diámetro de boquilla | 0.4 mm |
| Diámetro de filamento | 1.75 mm |

### Activar "Label objects"

En OrcaSlicer/PrusaSlicer activar **Print Settings → Label objects** para habilitar la macro `[exclude_object]` de Klipper, que permite cancelar objetos individuales durante la impresión.

---

## Perfiles por material

### 🟡 PLA

| Parámetro | Valor |
|-----------|-------|
| Temperatura hotend | 215 °C (primera capa: 220 °C) |
| Temperatura cama | 60 °C (primera capa: 65 °C) |
| Velocidad impresión | 150 mm/s |
| Velocidad primera capa | 30 mm/s |
| Velocidad perímetros externos | 80 mm/s |
| Velocidad relleno | 200 mm/s |
| Velocidad viaje | 250 mm/s |
| Aceleración impresión | 2000 mm/s² |
| Aceleración primera capa | 500 mm/s² |
| Retracción | 0.8 mm a 45 mm/s |
| Z-hop en retracción | 0.2 mm |
| Refrigeración | 100% desde capa 3 |
| Relleno | 15% gyroid (piezas funcionales: 40%) |
| Perímetros | 3 (piezas de estrés: 4) |
| Capas sólidas sup/inf | 4 |
| Altura de capa | 0.2 mm |

---

### 🔴 ABS / ASA

| Parámetro | Valor |
|-----------|-------|
| Temperatura hotend | 250 °C (primera capa: 255 °C) |
| Temperatura cama | 100 °C (primera capa: 105 °C) |
| Velocidad impresión | 100 mm/s |
| Velocidad primera capa | 20 mm/s |
| Velocidad perímetros externos | 60 mm/s |
| Velocidad relleno | 150 mm/s |
| Velocidad viaje | 200 mm/s |
| Aceleración impresión | 1500 mm/s² |
| Aceleración primera capa | 400 mm/s² |
| Retracción | 1.0 mm a 40 mm/s |
| Z-hop en retracción | 0.3 mm |
| Refrigeración | 0% (ABS) / 20% máx. desde capa 4 (ASA) |
| Relleno | 40% gyroid |
| Perímetros | 4 |
| Capas sólidas sup/inf | 5 |
| Altura de capa | 0.2 mm |

> ⚠️ Imprimir con recinto cerrado para evitar warping. Si no hay recinto, usar brim de 5–8 mm y desactivar completamente la refrigeración.

---

### 🟢 PETG

| Parámetro | Valor |
|-----------|-------|
| Temperatura hotend | 235 °C (primera capa: 240 °C) |
| Temperatura cama | 80 °C (primera capa: 85 °C) |
| Velocidad impresión | 100 mm/s |
| Velocidad primera capa | 25 mm/s |
| Velocidad perímetros externos | 60 mm/s |
| Velocidad relleno | 150 mm/s |
| Velocidad viaje | 200 mm/s |
| Aceleración impresión | 1500 mm/s² |
| Retracción | 1.2 mm a 35 mm/s |
| Z-hop en retracción | 0.4 mm |
| Refrigeración | 50–70% (evitar corriente directa sobre la pieza) |
| Relleno | 20% gyroid |
| Perímetros | 3 |
| Capas sólidas sup/inf | 4 |
| Altura de capa | 0.2 mm |

> ℹ️ El PETG es propenso al stringing. Si aparece, reducir la temperatura 5 °C o aumentar la retracción 0.2 mm.

---

### ⚫ TPU (flexible) — Solo con direct drive

| Parámetro | Valor |
|-----------|-------|
| Temperatura hotend | 220–240 °C (según shore) |
| Temperatura cama | 30–40 °C |
| Velocidad impresión | 30 mm/s máx. |
| Velocidad primera capa | 15 mm/s |
| Velocidad perímetros externos | 25 mm/s |
| Velocidad relleno | 35 mm/s |
| Velocidad viaje | 100 mm/s |
| Aceleración impresión | 500 mm/s² |
| Aceleración primera capa | 300 mm/s² |
| Retracción | 0.5 mm a 25 mm/s |
| Z-hop en retracción | 0 mm |
| Refrigeración | 50% |
| Relleno | 15% gyroid |

> ℹ️ El TPU no puede imprimirse en Bowden — una de las ventajas clave del extrusor directo Sharkfin.

---

## Ajustes de calidad — Recomendaciones generales

### Altura de primera capa

Usar **0.2–0.25 mm** de altura para la primera capa, independientemente de la altura general. Una primera capa más alta mejora la adhesión y da más margen al z_offset.

### Seam (costura)

Configurar la costura en **"Alineada"** o **"Esquina trasera"**. Evitar "Aleatoria" — con direct drive y PA bien calibrado la costura es apenas visible en modo alineado.

### Soporte

Con el Mini Stealth v2 y su refrigeración dual, el rendimiento en voladizos mejora respecto al stock. Se pueden eliminar soportes en ángulos de hasta **55–60°** con PLA bien refrigerado.

### Brim

- PLA: no necesario en la mayoría de casos
- ABS/ASA: brim de 5 mm si no hay recinto; 3 mm con recinto
- PETG: brim de 3 mm para piezas con poca superficie de contacto

---

## Configuración de Pressure Advance en el slicer

Una vez calibrado el PA en Klipper (`pressure_advance: X.XX` en `printer.cfg`), el slicer no necesita configuración adicional de Linear Advance — Klipper lo gestiona a nivel de firmware.

Lo que sí conviene ajustar en el slicer:
- **Desactivar "Linear Advance"** si el slicer lo tiene (Cura: "Enable Linear Advance")
- **No usar "Coasting"** — es incompatible con Pressure Advance

---

## Configuración de Input Shaping en el slicer

Tras ejecutar `SHAPER_CALIBRATE`, Klipper muestra en la consola algo similar a:

```
Fitted shaper 'mzv' frequency = 40.2 Hz (vibrations = 3.2%, smoothing ~= 0.105)
To avoid too much smoothing with 'mzv', suggested max_accel <= 4800 mm/sec^2
```

El valor `suggested max_accel` es el límite de aceleración recomendado para ese eje con el shaper elegido. Actualizar la aceleración del slicer con el valor **menor** entre X e Y.

Típicamente, con la A20M modificada se esperan valores de:
- **Eje X:** 3000–5000 mm/s² (más ligero con direct drive)
- **Eje Y:** 2000–3500 mm/s² (cama más pesada)

Usar el **valor menor** de los dos ejes como aceleración global en el slicer para resultados equilibrados.

---

## Perfil para boquilla 0.6 mm (alto caudal)

El CHC V6 Volcano está diseñado para alto caudal. Con boquilla de 0.6 mm se aprovecha mejor su capacidad y se reducen los tiempos de impresión manteniendo buena calidad.

> Cambiar el diámetro de boquilla en la configuración de máquina del slicer antes de usar este perfil.

### 🟡 PLA con boquilla 0.6 mm

| Parámetro | Valor |
|-----------|-------|
| Altura de capa | 0.3 mm (máx. recomendado: 0.45 mm) |
| Temperatura hotend | 220 °C (primera capa: 225 °C) |
| Temperatura cama | 60 °C |
| Velocidad impresión | 120 mm/s |
| Velocidad primera capa | 25 mm/s |
| Velocidad perímetros externos | 70 mm/s |
| Velocidad relleno | 180 mm/s |
| Retracción | 1.0 mm a 45 mm/s |
| Refrigeración | 100% desde capa 2 |
| Relleno | 15% gyroid |
| Perímetros | 3 |
| Capas sólidas sup/inf | 3 |

### 🔴 ABS/ASA con boquilla 0.6 mm

| Parámetro | Valor |
|-----------|-------|
| Altura de capa | 0.3 mm |
| Temperatura hotend | 255 °C (primera capa: 255 °C — misma temperatura, la primera capa no necesita más) |
| Temperatura cama | 100 °C |
| Velocidad impresión | 80 mm/s |
| Velocidad primera capa | 18 mm/s |
| Velocidad perímetros externos | 50 mm/s |
| Velocidad relleno | 120 mm/s |
| Retracción | 1.2 mm a 40 mm/s |
| Refrigeración | 0% |
| Relleno | 40% gyroid |
| Perímetros | 3 |
| Capas sólidas sup/inf | 4 |

> Con boquilla 0.6 mm y 0.3 mm de capa, el tiempo de impresión se reduce aproximadamente un 40% respecto a boquilla 0.4 mm / 0.2 mm de capa, con calidad similar en piezas funcionales.

---

## Configuración en Bambu Studio / OrcaSlicer for Bambu

Bambu Studio y OrcaSlicer (versión Bambu) usan variables de plantilla distintas:

### Start G-code

```gcode
START_PRINT BED_TEMP=[bed_temperature_initial_layer_single] EXTRUDER_TEMP=[nozzle_temperature_initial_layer]
```

### End G-code

```gcode
END_PRINT
```

### Notas específicas de Bambu Studio

- En **Printer Settings → Machine G-code**, añadir el Start y End G-code anteriores
- Activar **"Label objects"** en Print Settings → Others para compatibilidad con `[exclude_object]`
- El **"flow ratio"** de Bambu Studio equivale al multiplicador de flujo — dejarlo en 1.0 si `rotation_distance` está bien calibrado
- Desactivar **"Pressure advance"** en Bambu Studio — Klipper lo gestiona con su propio PA

---

## Referencia rápida de alturas de capa por boquilla

| Boquilla | Capa mín. | Capa recomendada | Capa máx. |
|----------|-----------|-----------------|----------|
| 0.4 mm | 0.05 mm | 0.2 mm | 0.32 mm |
| 0.6 mm | 0.08 mm | 0.3 mm | 0.48 mm |

> Regla general: la altura de capa no debe superar el **80%** del diámetro de la boquilla.
