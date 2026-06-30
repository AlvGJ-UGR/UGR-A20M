# 📋 Changelog — UGR-A20M

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).  
Versiones siguiendo [Semantic Versioning](https://semver.org/).

---

## [Unreleased]

Sin cambios pendientes. La siguiente entrada se abrirá al iniciar el montaje físico real de la Fase 1.

---

## [1.0.0-docs] — 2025-06-30

**Documentación completa de la Fase 1 cerrada.** Esta versión marca el punto en el que toda la planificación, configuración de firmware y guías de montaje están listas para ejecutarse físicamente. No implica que el montaje físico esté terminado — ver el estado real de cada fase en el [README](README.md).

### Añadido

**Documentación de fases**
- Especificaciones base de la Geeetech A20M original y justificación de cada decisión de diseño (`docs/fase-0/`)
- Guía completa de instalación SKR Mini E3 V3 + Klipper en Orange Pi Zero 3, desde Armbian hasta el primer `G28` (`docs/fase-1/electronica/`)
- Guía de montaje y calibración del extrusor directo Sharkfin + BMG Clone (`docs/fase-1/extrusor/`)
- Guía de montaje del toolhead Mini Stealth v2 + CHC V6 Volcano + CR-Touch (`docs/fase-1/toolhead/`)
- Plan de instalación de guías lineales MGN12H para la Fase 2 (`docs/fase-2/`)
- Plan de cierre del proyecto: benchmarks, fotografías y release final (`docs/fase-3/`)

**Guías transversales**
- Guía de calibración completa en 10 pasos ordenados (`docs/guia_calibracion.md`)
- Perfiles de slicer por material, incluyendo boquilla 0.6 mm y Bambu Studio (`docs/slicer_settings.md`)
- Guía de materiales compatibles con el CHC V6 Volcano (`docs/materiales.md`)
- Calendario de mantenimiento preventivo con consumibles (`docs/mantenimiento.md`)
- Troubleshooting centralizado por subsistema, incluyendo advertencias de seguridad eléctrica (`docs/troubleshooting.md`)
- Glosario técnico de 40+ términos (`docs/glosario.md`)

**Hardware**
- BOM de Fase 1 (~106 €) y Fase 2 (~35–47 €) con enlaces y tornillería (`hardware/bom/`)
- Esquema de conexiones completo de la SKR Mini E3 V3, incluyendo advertencias de amperaje (`hardware/electronica/`)
- Pinout de referencia con pines libres para expansión futura (`hardware/electronica/pinout_skr_mini_e3_v3.md`)
- Registro de piezas a imprimir con parámetros de material (`hardware/prints/`)

**Firmware**
- `printer.cfg` completo con las 16 secciones documentadas, comentarios de calibración y notas de orden de pasos
- 29 macros de Klipper organizadas en 6 categorías: impresión, flujo, filamento, material, calibración y mantenimiento
- Referencia Marlin del estado original como documentación histórica

**Repositorio**
- Web del proyecto en GitHub Pages (`docs/index.html`)
- `CONTRIBUTING.md`, `SECURITY.md`, templates de Issue y PR
- Licencia CC BY-SA 4.0

### Corregido

Durante el proceso de revisión se identificaron y corrigieron 30+ inconsistencias técnicas, entre ellas:
- Un riesgo de seguridad eléctrica no documentado: el amperaje de la cama original (~6.3–8.3 A) cerca del límite del MOSFET de la nueva placa
- El orden incorrecto de pasos de calibración (nivelar tornillos debe ir antes que calibrar z_offset)
- Varios bugs en macros de Klipper (`M300` inexistente sin buzzer, condiciones Jinja2 incorrectas, falta de comprobación de mesh antes de cargarlo)
- Inconsistencias numéricas entre documentos (precios, tensión de correa en Hz, temperaturas de primera capa)
- Carpetas residuales con nombres de brace-expansion mal interpretada, sustituidas por estructura limpia con `.gitkeep`

Detalle completo de cada corrección disponible en el [historial de commits](https://github.com/AlvGJ-UGR/UGR-A20M/commits/main).

---

## [0.2.0] — 2025-04-15

### Añadido
- Investigación y selección de componentes: Sharkfin + BMG Clone, CHC V6 Volcano, Mini Stealth v2, SKR Mini E3 V3.0, Orange Pi Zero 3

---

## [0.1.0] — 2025-04-10

### Añadido
- Creación del repositorio, README inicial, licencia CC BY-SA 4.0
