# Proyecto UGR-A20M

[![Estado](https://img.shields.io/badge/Estado-Fase_1_en_progreso-f0a500?style=flat-square)](https://github.com/AlvGJ-UGR/UGR-A20M)
[![Licencia](https://img.shields.io/badge/Licencia-CC_BY--SA_4.0-0ea5e9?style=flat-square)](LICENSE)
[![UGR](https://img.shields.io/badge/Universidad_de_Granada-2025-e8505b?style=flat-square)](https://www.ugr.es)
[![Klipper](https://img.shields.io/badge/Firmware-Klipper-3ecf8e?style=flat-square)](https://www.klipper3d.org/)
[![Web](https://img.shields.io/badge/GitHub_Pages-Ver_web-7c3aed?style=flat-square)](https://alvgj-ugr.github.io/UGR-A20M/)

**Modernización de una impresora 3D Geeetech A20M** con electrónica de 32 bits, extrusión directa tipo Voron y firmware Klipper.  
Proyecto de investigación aplicada de la **Universidad de Granada**, documentado para ser completamente reproducible por ~150 €.

---

## ¿Qué es este proyecto?

Una Geeetech A20M con placa de 8 bits, sistema Bowden y drivers A4988 ruidosos se transforma progresivamente en una máquina moderna: 32 bits con TMC2209 silenciosos, extrusor directo Sharkfin, toolhead Mini Stealth v2 estilo Voron y firmware Klipper con interfaz web. Cada fase está documentada de forma que cualquier persona pueda reproducirla.

---

## Estado del proyecto

| Fase | Descripción | Estado |
|------|-------------|--------|
| **0** | Especificaciones, investigación de componentes y repositorio | ✅ Completada |
| **1a** | Electrónica: SKR Mini E3 V3 + Orange Pi Zero 3 + Klipper | 🟡 En progreso |
| **1b** | Extrusor directo: Sharkfin + BMG Clone + NEMA 17 pancake | 🟡 En progreso |
| **1c** | Toolhead: Mini Stealth v2 + CHC V6 Volcano + CR-Touch | 🟡 En progreso |
| **2** | Guías lineales MGN12H en X e Y | 🔜 Planificada |
| **3** | Benchmarks, informe UGR y publicación final | 🔜 Planificada |

---

## Especificaciones

| | Original | Objetivo (Fase 1) |
|--|----------|------------------|
| **Placa** | GT2560 v3 (ATmega2560, 8-bit) | BTT SKR Mini E3 V3.0 (STM32G0B1, 32-bit) |
| **Drivers** | A4988 | TMC2209 (UART, StealthChop) |
| **Host** | — | Orange Pi Zero 3 (1 GB, Armbian) |
| **Firmware** | Marlin 1.x | Klipper + Moonraker + Fluidd |
| **Extrusión** | Bowden dual mixing | Direct drive — Sharkfin + BMG (~3.5:1) |
| **Toolhead** | J-Head stock | Mini Stealth v2 (Voron-style) |
| **Hotend** | 250 °C máx. | CHC V6 Volcano — 285 °C máx. |
| **Nivelación** | Manual (4 tornillos) | CR-Touch — mesh autom. 5×5 |
| **Velocidad práctica** | ~60 mm/s | ~150–200 mm/s |
| **Control** | LCD local + SD | Fluidd web — cualquier dispositivo |

---

## Inicio rápido

Si ya tienes el hardware instalado y quieres poner la impresora en marcha:

```
1. Instalar Armbian + Klipper en la Orange Pi  →  docs/fase-1/electronica/01_skr_klipper.md
2. Flashear Klipper en la SKR Mini E3 V3       →  (misma guía, Parte 3)
3. Copiar printer.cfg y actualizar el serial   →  firmware/README.md
4. Calibrar en orden (10 pasos)                →  docs/guia_calibracion.md
5. Configurar el slicer                        →  docs/slicer_settings.md
```

---

## Documentación

| Documento | Descripción |
|-----------|-------------|
| [🎯 Guía de calibración](docs/guia_calibracion.md) | 10 pasos ordenados — **empezar aquí** tras instalar |
| [🖨️ Configuración del slicer](docs/slicer_settings.md) | Perfiles PLA / ABS / PETG / TPU con start G-code |
| [⚙️ Firmware — instalación y macros](firmware/README.md) | Instalar printer.cfg y referencia de las 20 macros |
| [⚡ Esquema de conexiones](hardware/electronica/esquema_conexiones.md) | Pin a pin: SKR Mini E3 V3 completo |
| [📋 Especificaciones base](docs/fase-0/00_especificaciones_base.md) | La A20M original y decisiones de diseño |
| [⚡ SKR Mini E3 V3 + Klipper](docs/fase-1/electronica/01_skr_klipper.md) | Armbian, KIAUH, compilar, flashear |
| [🔩 Sharkfin + BMG Clone](docs/fase-1/extrusor/02_sharkfin_bmg.md) | Montaje y calibración del extrusor directo |
| [🏎️ Mini Stealth v2 + CR-Touch](docs/fase-1/toolhead/03_mini_stealth_chc_crtouch.md) | Toolhead completo con CHC V6 Volcano |
| [📐 Guías lineales MGN12H](docs/fase-2/04_guias_lineales.md) | Instalación en X e Y (Fase 2) |
| [🔧 Troubleshooting](docs/troubleshooting.md) | Problemas frecuentes centralizados |
| [📦 BOM Fase 1](hardware/bom/BOM_fase1.md) | ~106 € — electrónica, extrusor y toolhead |
| [📦 BOM Fase 2](hardware/bom/BOM_fase2.md) | ~35–47 € — guías lineales MGN12H |
| [🖨️ Registro de impresiones](hardware/prints/README.md) | Seguimiento de piezas con parámetros y resultado |
| [🌐 Web del proyecto](https://alvgj-ugr.github.io/UGR-A20M/) | GitHub Pages — documentación navegable |

---

## Estructura del repositorio

```
UGR-A20M/
├── README.md                 ← Este archivo
├── CHANGELOG.md              ← Historial de cambios por versión
├── CONTRIBUTING.md           ← Cómo contribuir al proyecto
├── SECURITY.md               ← Política de seguridad
├── LICENSE                   ← CC BY-SA 4.0
├── .gitignore
│
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md     ← Template para reportar errores
│   │   └── feature_request.md← Template para propuestas de mejora
│   └── pull_request_template.md
│
├── docs/                     ← Documentación (GitHub Pages desde aquí)
│   ├── index.html            ← Web del proyecto
│   ├── _config.yml           ← Configuración Jekyll/GitHub Pages
│   ├── guia_calibracion.md   ← Calibración completa paso a paso ⭐
│   ├── slicer_settings.md    ← Perfiles por material para el slicer
│   ├── troubleshooting.md    ← Problemas frecuentes centralizados ⭐
│   ├── fase-0/
│   │   └── 00_especificaciones_base.md
│   ├── fase-1/
│   │   ├── electronica/01_skr_klipper.md
│   │   ├── extrusor/02_sharkfin_bmg.md
│   │   └── toolhead/03_mini_stealth_chc_crtouch.md
│   ├── fase-2/
│   │   └── 04_guias_lineales.md
│   ├── fase-3/
│   │   └── 05_documentacion_final.md
│   └── img/
│       └── banner-ugr-a20m.png
│
├── hardware/
│   ├── bom/
│   │   ├── BOM_fase1.md      ← ~106 € — electrónica, extrusor, toolhead
│   │   └── BOM_fase2.md      ← ~35–47 € — guías lineales MGN12H
│   ├── prints/
│   │   └── README.md         ← Registro de piezas impresas
│   └── electronica/
│       └── esquema_conexiones.md
│
├── firmware/
│   ├── README.md             ← Instalación y referencia de macros
│   ├── klipper/
│   │   ├── config/printer.cfg
│   │   └── macros/macros.cfg
│   └── marlin/
│       └── README.md         ← Valores originales (referencia histórica)
│
└── photos/
    ├── README.md             ← Convención de nombres y checklist fotográfico
    ├── estado-inicial/
    ├── fase-1/
    └── fase-2/
```

---

## Presupuesto total

| Fase | Contenido | Coste |
|------|-----------|-------|
| Fase 1 | SKR Mini E3 V3 + Orange Pi Zero 3 + Sharkfin + Mini Stealth v2 + CHC Volcano + CR-Touch | ~106 € |
| Fase 2 | 3× guías MGN12H 300 mm + tornillería + adaptadores | ~35–47 € |
| **Total** | | **~141–153 €** |

---

## Referencias

**Hardware:** [Sharkfin Extruder](https://github.com/KayosMaker/Sharkfin_Extruder) · [Mini Stealth v2](https://github.com/atrushing/Mini_Stealth) · [SKR Mini E3 V3](https://github.com/bigtreetech/BIGTREETECH-SKR-mini-E3)

**Firmware:** [Klipper](https://www.klipper3d.org/) · [Moonraker](https://moonraker.readthedocs.io/) · [Fluidd](https://fluidd.xyz/) · [KIAUH](https://github.com/dw-0/kiauh)

**SBC:** [Orange Pi Zero 3](http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/Orange-Pi-Zero-3.html) · [Armbian](https://www.armbian.com/orange-pi-zero3/)

**Inspiración:** [Voron Design](https://vorondesign.com/)

---

## Créditos y licencia

**Autor:** Álvaro González Jiménez · `alvarogj1@correo.ugr.es`  
**Institución:** Universidad de Granada (UGR) · 2025  
**Licencia:** [CC BY-SA 4.0](LICENSE) — libre uso con atribución y misma licencia
