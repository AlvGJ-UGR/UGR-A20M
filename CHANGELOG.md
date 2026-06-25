# 📋 Changelog — UGR-A20M

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).  
Versiones siguiendo [Semantic Versioning](https://semver.org/).

---

## [Unreleased] — Fase 1 en progreso

### Añadido
- `docs/guia_calibracion.md` — Guía centralizada de calibración (10 pasos, checklist, solución de problemas)
- `hardware/electronica/esquema_conexiones.md` — Conexionado completo SKR Mini E3 V3 con diagramas ASCII
- `docs/fase-3/05_documentacion_final.md` — Plan de benchmarks, GitHub Pages e informe UGR
- `CONTRIBUTING.md` — Guía de contribución con convenciones del proyecto
- Macros Klipper ampliadas: `CHANGE_FILAMENT`, `PREHEAT_PLA/ABS/PETG`, `COOLDOWN`, `PARK`, `CLEAN_NOZZLE`, `STATUS`, `PRESSURE_ADVANCE_TOWER`, `CALIBRATE_Z_OFFSET`, `LEVEL_BED_SCREWS`, `GENERATE_MESH`
- Tabla de documentación rápida en README (acceso directo a los documentos clave)

### Mejorado
- `firmware/klipper/config/printer.cfg` — Añadidos `[tmc2209]` para los 4 drivers, `[screws_tilt_adjust]`, `[exclude_object]`, `gear_ratio` en extrusor, `kick_start_time` en ventiladores, sección de notas de calibración A–K
- `firmware/klipper/macros/macros.cfg` — Reescrito completamente con índice, PAUSE mejorado con safe_z, macros de precalentamiento y mantenimiento
- `docs/fase-1/toolhead/03_mini_stealth_chc_crtouch.md` — Eliminadas etiquetas `<cite>` residuales, texto limpio
- `README.md` — Árbol de ficheros actualizado, tabla de documentación rápida, fases actualizadas

---

## [0.2.0] — 2025-04-15

### Añadido
- Investigación y selección de componentes (`hardware/notas`)
- Extrusor: Sharkfin + BMG Clone
- Hotend: CHC V6 Volcano
- Toolhead: Mini Stealth v2
- Placa: BTT SKR Mini E3 V3.0
- SBC: Orange Pi Zero 3 (1 GB)

---

## [0.1.0] — 2025-04-10

### Añadido
- Creación del repositorio en GitHub
- README inicial con descripción y objetivos
- Licencia CC BY-SA 4.0
- Banner del proyecto
- Definición inicial de fases
