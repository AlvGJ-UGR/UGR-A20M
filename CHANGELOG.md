# 📋 Changelog — UGR-A20M

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).  
Versiones siguiendo [Semantic Versioning](https://semver.org/).

---

## [Unreleased] — Fase 1 en progreso

### Mejorado
- `docs/fase-2/04_guias_lineales.md` — Inconsistencia de coste corregida (€35–50 → €35–47, alineado con BOM_fase2); procedimiento concreto de alineación en Y con tres puntos de medición y tolerancia < 0.3 mm; referencia de tensión de correas en Hz (objetivo ~50 Hz); alineación en X cambiada a método práctico (deslizar carro y buscar punto duro)
- `docs/fase-0/00_especificaciones_base.md` — Checklist de fotos duplicado eliminado (referencia a `photos/README.md`); tabla comparativa de modelos Orange Pi añadida explicando por qué la Zero 3 específicamente vs Orange Pi 3B y 5 (consumo RAM de Klipper, precio, factor de forma)
- `firmware/klipper/config/printer.cfg` — Sección `[screws_tilt_adjust]` documentada con la fórmula para calcular coordenadas a partir de la posición física de los tornillos y los offsets del CR-Touch; posiciones físicas estimadas de los 4 tornillos de la A20M
- `firmware/marlin/README.md` — E-steps de 96 steps/mm aclarados como específicos del extrusor Bowden original — no trasladables al Sharkfin
- `CONTRIBUTING.md` — Política de revisión ajustada para reflejar la realidad de proyecto personal: sin SLA formal, sin "mergeado automático", instrucción de mencionar al autor si hay silencio > 2 semanas
- `docs/mantenimiento.md` — Tabla de consumibles ampliada con columna de precio orientativo y fila de total (~26 €)
- `CHANGELOG.md` — Consolidado y actualizado

### Añadido
- `docs/glosario.md` — Glosario técnico con 40+ definiciones orientado a estudiantes UGR sin experiencia previa en impresión 3D avanzada
- `docs/materiales.md` — Guía de materiales: cuándo usar cada uno, preparación, adhesión, secado y boquillas; sin duplicar los parámetros del slicer
- `docs/mantenimiento.md` — Calendario preventivo (antes de imprimir, cada 20 h, 50 h, 200 h, 500 h), consumibles recomendados en stock y log de horas
- `docs/troubleshooting.md` — Guía centralizada de problemas frecuentes por subsistema con tablas causa→solución
- `docs/slicer_settings.md` — Perfiles para OrcaSlicer, PrusaSlicer y Cura: PLA, ABS/ASA, PETG, TPU; boquilla 0.6 mm; Bambu Studio
- `SECURITY.md` — Advertencias de seguridad eléctrica/térmica, seguridad de red para Fluidd y política de reporte de vulnerabilidades
- `CONTRIBUTING.md` — Flujo de trabajo completo con git (fork web + clone + upstream + rebase), tabla de tipos de commit y convenciones del proyecto
- `hardware/electronica/pinout_skr_mini_e3_v3.md` — Referencia completa de pines usados y disponibles, UART TMC2209, configuración de ADXL345, sensor de filamento y FAN2
- `.github/ISSUE_TEMPLATE/bug_report.md` — Template estructurado para reportar errores
- `.github/ISSUE_TEMPLATE/feature_request.md` — Template para propuestas de mejora
- `.github/pull_request_template.md` — Template de PR con checklist de convenciones

### Mejorado
- `docs/index.html` — Página de GitHub Pages con todos los links como URLs absolutas de GitHub, 11 tarjetas de documentación, sección de Recursos externos con 8 tarjetas, nav sticky con backdrop-filter, animaciones de entrada, gradientes radiales, responsive mobile
- `docs/_config.yml` — Configuración Jekyll completa: title, description, url, baseurl, exclude list
- `firmware/klipper/config/printer.cfg` — Añadidos `[tmc2209]` para los 4 drivers, `[screws_tilt_adjust]`, `[exclude_object]`, `[gcode_arcs]`, `[filament_switch_sensor]` comentado, `gear_ratio` en extrusor, `kick_start_time` en ventiladores; índice de 16 secciones
- `firmware/klipper/macros/macros.cfg` — 29 macros en 6 categorías: añadidas `FILAMENT_RUNOUT`, `SET_MATERIAL`, `PREHEAT_TPU`, `PRINT_STATS`, `NOZZLE_CHANGE`, `CALIBRATE_INPUT_SHAPING`; `END_PRINT` con safe_z dinámico; `STATUS` con formato mejorado
- `firmware/README.md` — Tabla de las 29 macros con parámetros disponibles, instrucciones de instalación paso a paso
- `hardware/electronica/esquema_conexiones.md` — Reescrito: longitudes de cable para el extrusor, orden de pines JST XH de motores, gestión del segundo conector Bowden libre, advertencia de cama 220V AC, nota sobre calidad del cable USB, checklist pre-encendido expandido
- `hardware/prints/README.md` — Parámetros ASA completados en todas las piezas de Fase 1 (temperatura, cama, relleno); tabla de parámetros duplicada sustituida por referencia a `slicer_settings.md`
- `hardware/bom/BOM_fase2.md` — BOM completa Fase 2 con notas de calidad y coste total acumulado
- `docs/fase-0/00_especificaciones_base.md` — Ampliado con decisiones de diseño: por qué Klipper vs Marlin, por qué SKR Mini E3 V3, por qué Orange Pi Zero 3
- `docs/fase-1/electronica/01_skr_klipper.md` — Reescrito: Armbian desde cero, WiFi con nmtui, KIAUH, make menuconfig con tabla exacta, flash por SD, verificación post-instalación, troubleshooting de 6 síntomas
- `docs/fase-1/extrusor/02_sharkfin_bmg.md` — Corregido F300→F150 en calibración; ejemplo numérico de rotation_distance; troubleshooting de 7 síntomas; comparativa Bowden vs direct drive
- `docs/fase-2/04_guias_lineales.md` — Reescrito: justificación técnica, BOM con links, proceso de instalación con puntos críticos de alineación, notas de calidad para guías de AliExpress, tabla de mejoras esperadas
- `docs/fase-3/05_documentacion_final.md` — Tabla de benchmarks con metodología, modelos de test con links, comando Pandoc correcto, checklist expandido con estado del firmware
- `docs/guia_calibracion.md` — Corregido orden de pasos 6 y 7 (nivelar tornillos antes del z_offset); eliminada tabla de troubleshooting duplicada; nota explicando el motivo del orden
- `README.md` — Badges con colores coherentes y link a GitHub Pages; tabla de specs como comparativa stock vs objetivo; árbol de ficheros completo; tabla de documentación con 17 entradas
- `LICENSE` — Sustituido texto MIT por **CC BY-SA 4.0** completo con datos del autor y enlace al texto legal
- `.gitignore` — Ampliado: slicer (gcode, 3mf, prusa), CAD (FreeCAD, Fusion 360), sistema operativo, editores, temporales

### Eliminado (redundancias)
- Tabla de troubleshooting al final de `guia_calibracion.md` → apunta a `troubleshooting.md`
- Tablas de parámetros de temperatura/retracción de `materiales.md` → apuntan a `slicer_settings.md`
- Descripción completa de inversión de `dir_pin` en `troubleshooting.md` → apunta a `guia_calibracion.md`
- Tabla de parámetros ABS/ASA de `hardware/prints/README.md` → apunta a `slicer_settings.md`

---

## [0.2.0] — 2025-04-15

### Añadido
- Investigación y selección de componentes: Sharkfin + BMG Clone, CHC V6 Volcano, Mini Stealth v2, SKR Mini E3 V3.0, Orange Pi Zero 3

---

## [0.1.0] — 2025-04-10

### Añadido
- Creación del repositorio en GitHub
- README inicial con descripción y objetivos
- Licencia CC BY-SA 4.0
- Banner del proyecto
- Definición inicial de fases
