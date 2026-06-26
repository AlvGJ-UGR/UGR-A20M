# ⚙️ Firmware — UGR-A20M

Configuración de **Klipper** para la Geeetech A20M modificada con SKR Mini E3 V3.0 y Orange Pi Zero 3.

---

## Estructura

```
firmware/
├── klipper/
│   ├── config/
│   │   └── printer.cfg      ← Configuración principal de la impresora
│   └── macros/
│       └── macros.cfg       ← Macros: START_PRINT, calibración, mantenimiento
└── marlin/                  ← Configuración Marlin original (solo referencia)
```

---

## Instalación

### Requisitos previos

- Klipper, Moonraker y Fluidd instalados en la Orange Pi Zero 3  
  → Ver guía completa: [`docs/fase-1/electronica/01_skr_klipper.md`](../docs/fase-1/electronica/01_skr_klipper.md)
- SKR Mini E3 V3.0 flasheada con Klipper  
  → Ver proceso de compilación y flash en la misma guía

### Copiar los archivos de configuración

```bash
# En la Orange Pi Zero 3, desde el directorio del proyecto:
cp firmware/klipper/config/printer.cfg ~/printer_data/config/
cp firmware/klipper/macros/macros.cfg  ~/printer_data/config/

# O subir directamente desde Fluidd:
# Configuration → icono de subida → seleccionar ambos archivos
```

### Editar el serial del MCU

**Este paso es obligatorio.** El serial es único para cada placa.

```bash
# En la Orange Pi, con la SKR conectada por USB:
ls /dev/serial/by-id/
# Resultado ejemplo:
# usb-Klipper_stm32g0b1xx_2B0044000B50304158373520-if00
```

Abrir `printer.cfg` y actualizar:

```ini
[mcu]
serial: /dev/serial/by-id/PEGAR_AQUÍ_EL_SERIAL_COMPLETO
```

### Reiniciar Klipper

```bash
sudo systemctl restart klipper
```

O desde Fluidd: botón **Restart** → **Firmware Restart**.

---

## Parámetros que requieren calibración

Los siguientes valores en `printer.cfg` están marcados con `# ← CALIBRAR` y **deben personalizarse** antes de imprimir:

| Parámetro | Sección | Descripción |
|-----------|---------|-------------|
| `serial` | `[mcu]` | Serial único de la SKR Mini E3 V3 |
| `rotation_distance` | `[extruder]` | Calibrar con prueba de extrusión |
| `x_offset`, `y_offset` | `[bltouch]` | Medir físicamente con calibre |
| `z_offset` | `[bltouch]` | Calibrar con `PROBE_CALIBRATE` |
| `pid_Kp/Ki/Kd` | `[extruder]` | Calibrar con `CALIBRATE_PID_HOTEND` |
| `pid_Kp/Ki/Kd` | `[heater_bed]` | Calibrar con `CALIBRATE_PID_BED` |
| `pressure_advance` | `[extruder]` | Calibrar con `PRESSURE_ADVANCE_TOWER` |
| Posiciones en `[screws_tilt_adjust]` | — | Medir posición real de los tornillos de cama |

→ Ver procedimiento completo paso a paso: [`docs/guia_calibracion.md`](../docs/guia_calibracion.md)

---

## Macros disponibles

### Impresión

| Macro | Uso |
|-------|-----|
| `START_PRINT BED_TEMP=X EXTRUDER_TEMP=Y` | Inicio de impresión — llamar desde el slicer |
| `END_PRINT` | Fin de impresión — llamar desde el slicer |
| `PAUSE` | Pausar y aparcar el cabezal |
| `RESUME` | Reanudar desde la posición de pausa |
| `CANCEL_PRINT` | Cancelar la impresión en curso |

### Filamento

| Macro | Uso |
|-------|-----|
| `LOAD_FILAMENT [TEMP=200]` | Cargar filamento |
| `UNLOAD_FILAMENT [TEMP=200]` | Descargar filamento |
| `CHANGE_FILAMENT` | Pausa guiada para cambio de filamento |

### Precalentamiento

| Macro | Uso |
|-------|-----|
| `PREHEAT_PLA` | Hotend 200 °C, cama 60 °C |
| `PREHEAT_ABS` | Hotend 250 °C, cama 100 °C |
| `PREHEAT_PETG` | Hotend 235 °C, cama 80 °C |
| `COOLDOWN` | Apagar todos los calentadores y ventiladores |

### Calibración

| Macro | Uso |
|-------|-----|
| `CALIBRATE_PID_HOTEND [TEMP=220]` | Calibrar PID del hotend |
| `CALIBRATE_PID_BED [TEMP=60]` | Calibrar PID de la cama |
| `CALIBRATE_Z_OFFSET` | Calibrar z_offset del CR-Touch |
| `LEVEL_BED_SCREWS` | Nivelar tornillos de cama con guía |
| `GENERATE_MESH` | Generar y guardar mesh de nivelación |
| `PRESSURE_ADVANCE_TOWER` | Torre de calibración de Pressure Advance |

### Mantenimiento

| Macro | Uso |
|-------|-----|
| `HOME_ALL` | Homing completo de todos los ejes |
| `PARK` | Aparcar en posición de mantenimiento (centro, Z alto) |
| `MOTORS_OFF` | Desactivar todos los motores |
| `CLEAN_NOZZLE [TEMP=220]` | Rutina de limpieza de boquilla |
| `STATUS` | Mostrar temperatura y posición en la consola |

---

## Configuración del slicer

Añadir en el campo **Start G-code** del slicer:

```gcode
START_PRINT BED_TEMP=[first_layer_bed_temperature] EXTRUDER_TEMP=[first_layer_temperature]
```

Añadir en el campo **End G-code**:

```gcode
END_PRINT
```

→ Ver perfiles completos por material: [`docs/slicer_settings.md`](../docs/slicer_settings.md)

---

## Archivo Marlin (referencia)

La carpeta `firmware/marlin/` está reservada para guardar la configuración original de Marlin de la GT2560 como referencia histórica. No se usa activamente — la impresora corre Klipper.
