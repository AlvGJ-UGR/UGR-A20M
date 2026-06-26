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

Tras calibrar Input Shaping en Klipper y configurar las frecuencias en `printer.cfg`, la aceleración máxima recomendada por Klipper aparece en el log. Actualizar la aceleración máxima del slicer con ese valor.

Típicamente, con la A20M modificada se esperan valores de:
- **Eje X:** 3000–5000 mm/s² (más ligero con direct drive)
- **Eje Y:** 2000–3500 mm/s² (cama más pesada)

Usar el **valor menor** de los dos ejes como aceleración global en el slicer para resultados equilibrados.
