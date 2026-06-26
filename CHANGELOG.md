# 📋 Changelog — UGR-A20M

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).  
Versiones siguiendo [Semantic Versioning](https://semver.org/).

---

## [Unreleased] — Fase 1 en progreso

### Añadido
- `docs/slicer_settings.md` — Perfiles completos para OrcaSlicer/PrusaSlicer/Cura: PLA, ABS/ASA, PETG y TPU con start/end G-code, velocidades, temperaturas y notas por material
- `firmware/README.md` — Guía de instalación del firmware, tabla de todos los parámetros a calibrar con enlace a la sección correspondiente, y referencia completa de macros disponibles
- `docs/index.md` — Índice para GitHub Pages con inicio rápido y navegación por fases

### Mejorado
- `docs/fase-0/00_especificaciones_base.md` — Ampliado con sección de decisiones de diseño (por qué Klipper vs Marlin, por qué SKR Mini E3 V3, por qué Orange Pi Zero 3), contexto técnico y parámetros de referencia del slicer stock
- `docs/fase-1/electronica/01_skr_klipper.md` — Reescrito completamente: guía de Armbian desde cero, configuración SSH y WiFi, instalación KIAUH paso a paso, tabla de opciones `make menuconfig`, proceso de flash detallado, checklist de verificación post-instalación y tabla de troubleshooting
- `docs/fase-1/extrusor/02_sharkfin_bmg.md` — Corregido F300→F150 en procedimiento de calibración (velocidad incorrecta que causaba patinaje), añadido ejemplo numérico de cálculo de rotation_distance, tabla de troubleshooting y comparativa Bowden vs direct drive ampliada
- `docs/fase-2/04_guias_lineales.md` — Reescrito completamente: justificación técnica detallada, especificaciones de las guías (MGN12H en X e Y), BOM con enlaces reales, proceso de instalación con puntos críticos de alineación, notas de calidad y tabla de mejoras esperadas
- `hardware/prints/README.md` — Sección Fase 2 actualizada con las 4 piezas reales necesarias para la instalación de MGN12H y sus funciones
- `README.md` — Tabla de documentación rápida ampliada con slicer settings y firmware README

---

## [0.2.0] — 2025-10-17

### Añadido
- Investigación y selección de componentes (`hardware/notas`)
- Extrusor: Sharkfin + BMG Clone
- Hotend: CHC V6 Volcano
- Toolhead: Mini Stealth v2
- Placa: BTT SKR Mini E3 V3.0
- SBC: Orange Pi Zero 3 (1 GB)

---

## [0.1.0] — 2025-10-10

### Añadido
- Creación del repositorio en GitHub
- README inicial con descripción y objetivos
- Licencia CC BY-SA 4.0
- Banner del proyecto
- Definición inicial de fases
