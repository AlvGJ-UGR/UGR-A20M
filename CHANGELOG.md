# 📋 Changelog — UGR-A20M

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).  
Versiones siguiendo [Semantic Versioning](https://semver.org/).

---

## [Unreleased] — Fase 1 en progreso

### Corregido
- `docs/fase-1/electronica/01_skr_klipper.md`
  - Imagen de Armbian especificada exactamente: **Server minimal**, no Desktop (evita confusión y consumo de RAM innecesario)
  - Aclarado que la compilación de Klipper se hace en la propia Orange Pi, no en un PC externo
  - Añadida alternativa `make -j1` si la compilación falla por falta de RAM
  - Checklist: añadida verificación del grupo `dialout` (causa frecuente de fallo de conexión por permisos, no documentada antes)
  - Checklist: "Klipper no muestra errores" sustituido por instrucción concreta de dónde mirar (pestaña Console/Klippy log en Fluidd)
- `docs/fase-1/extrusor/02_sharkfin_bmg.md`
  - Paso 2: añadida verificación del flat del eje del motor NEMA 17 pancake — su ausencia (frecuente en motores baratos) es la causa real de que el engranaje conductor patine sin que sea evidente a simple vista
  - Procedimiento de calibración: especificado el uso de PLA para la prueba de 100 mm, con nota de que el resultado es válido para todos los materiales
  - Troubleshooting de sobre/sub-extrusión: añadido el primer paso de diagnóstico (repetir la prueba de 100 mm) antes de recalcular a ciegas; sub-extrusión incluye verificar obstrucción de boquilla antes de tocar `rotation_distance`
- `firmware/klipper/macros/macros.cfg`
  - `FILAMENT_RUNOUT`: eliminado `M300` (no existe en Klipper sin buzzer configurado — causaba error silencioso); reemplazado por `action_respond_info`
  - `CHANGE_FILAMENT`: ahora pasa la temperatura actual del hotend a `UNLOAD_FILAMENT` en lugar de descargar siempre a 200 °C
  - `NOZZLE_CHANGE`: eliminado el doble `M117` consecutivo (el segundo sobreescribía al primero de inmediato); reemplazado por `action_respond_info` con mensaje completo
  - `PARK`: corregida la condición de homing de `!= "xyz"` a `"xyz" not in ...` (sintaxis correcta de Jinja2 en Klipper)
  - `START_PRINT`: añadida comprobación de existencia del perfil mesh `default` antes de cargarlo — evita error de Klipper si aún no se ha generado el mesh
- `firmware/klipper/config/printer.cfg`
  - `[bltouch]`: eliminado `z_offset: 0` hardcodeado — Klipper escribe ese valor automáticamente vía `SAVE_CONFIG`; tenerlo a 0 podría hacer que el nozzle chocara con la cama si alguien ejecuta `G28` antes de calibrar
- `hardware/electronica/pinout_skr_mini_e3_v3.md`
  - Sección de sensor de filamento: corregida la nota de cableado — los microswitches de contacto seco no necesitan VCC; explicado el papel del pull-up interno `^` del pin PC15

### Mejorado
- `firmware/klipper/config/printer.cfg`
  - Drivers TMC2209: añadido `interpolate: True` en X/Y/Z e `interpolate: False` en extrusor (sin interpolación en extrusor mejora el control de flujo); comentarios más claros sobre por qué SpreadCycle en Z y E
- `hardware/electronica/pinout_skr_mini_e3_v3.md`
  - Pin `PA8` (FAN2) añadido a la tabla de pines disponibles con su tipo correcto (PWM 24V)
- `docs/materiales.md`
  - WOOD PLA: boquilla corregida a ≥ 0.5 mm (no 0.4 mm — las partículas de madera obstruyen la boquilla de 0.4 mm)
  - Typo "structurales" → "estructurales"
  - Tabla de secado: añadida columna de síntoma de humedad característico por material
- `docs/glosario.md`
  - `gear_ratio`: corregida la explicación de la relación 50:17 — la descripción anterior era confusa e incorrecta
- `hardware/bom/BOM_fase1.md`
  - Tabla de piezas a imprimir: añadidos pesos estimados por pieza y total (~126 g), especificada la variante `probe-mount left`, notas críticas de impresión por pieza
- `docs/fase-3/05_documentacion_final.md`
  - Método de test de velocidad máxima concretado (cubos a velocidades crecientes)
  - Columna Δ total aclarada con formato de resultado; añadida fila de tiempo de calentamiento
- `docs/guia_calibracion.md`
  - Paso 9 (PA): corregido el malentendido — la macro modifica la impresión en curso; procedimiento en 9 pasos con instrucción de cancelar a los 40 mm
  - Paso 4 (PID cama): temperatura 100 °C para ABS, duración 15–25 min, cómo saber que terminó
- `docs/troubleshooting.md`
  - Tensión de correa unificada a ~50 Hz; sección `BLTouch not deployed` con 4 causas
- `docs/slicer_settings.md`
  - TPU: añadida aceleración; IS: formato exacto del log de Klipper; ABS 0.6 mm primera capa corregida a 255 °C

---

## [0.2.0] — 2025-04-15

### Añadido
- Investigación y selección de componentes: Sharkfin + BMG Clone, CHC V6 Volcano, Mini Stealth v2, SKR Mini E3 V3.0, Orange Pi Zero 3

---

## [0.1.0] — 2025-04-10

### Añadido
- Creación del repositorio, README inicial, licencia CC BY-SA 4.0
