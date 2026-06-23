

# 🧠 Proyecto UGR-A20M
![Status](https://img.shields.io/badge/Status-Fase_1_en_progreso-yellow.svg)
![License](https://img.shields.io/badge/License-CC_BY--SA_4.0-blue.svg)
![UGR](https://img.shields.io/badge/Universidad-Granada-red.svg)

### Mejora y documentación de una impresora 3D Geeetech A20M — Hacia una arquitectura tipo Voron

![Banner del proyecto](docs/img/banner-ugr-a20m.png)

---

## 🧩 Descripción general

Este proyecto documenta la **modernización progresiva** de una impresora 3D **Geeetech A20M**, incorporando componentes de alto rendimiento y rediseñando la arquitectura hacia un sistema **inspirado en la filosofía Voron**.

El proyecto está **subvencionado por la Universidad de Granada (UGR)**, con fines educativos, divulgativos y de investigación aplicada en el ámbito de la fabricación digital.

---

## 🎯 Objetivos

- 🔧 Mejorar el rendimiento, fiabilidad y velocidad de la Geeetech A20M
- 🖨️ Implementar extrusión directa de alto caudal (Sharkfin + CHC V6 Volcano)
- ⚙️ Migrar la electrónica a SKR Mini E3 V3 + Orange Pi Zero 3 con Klipper
- 📐 Adaptar la estructura hacia diseño tipo Voron (guías lineales, CoreXY)
- 📚 Crear una **guía reproducible** para estudiantes y makers de la UGR
- 🎨 Personalizar la máquina con identidad visual UGR

---

## 🚀 Estado del proyecto

| Fase | Descripción | Estado |
|------|-------------|--------|
| **0** | Repositorio, documentación base y especificaciones | ✅ Completada |
| **1a** | Actualización electrónica (SKR Mini E3 V3 + Klipper) | 🟡 En progreso |
| **1b** | Extrusor directo Sharkfin + hotend CHC V6 Volcano | 🟡 En progreso |
| **2** | Guías lineales y bastidor reforzado | 🔜 Planificada |
| **3** | Conversión CoreXY completa (T250 / Voron) | 🔜 Planificada |
| **4** | Informe final, publicación GitHub Pages y PDF UGR | 🔜 Planificada |

---

## ⚙️ Especificaciones

### Máquina base

| Parámetro | Valor |
|-----------|-------|
| **Modelo** | Geeetech A20M |
| **Volumen de impresión** | 255 × 255 × 255 mm |
| **Cinemática original** | Cartesian Bowden |
| **Placa base original** | GT2560 v3 (8-bit) |
| **Firmware original** | Marlin 1.x |
| **Alimentación** | 24V DC |
| **Cama caliente** | 220V AC / 24V DC calefactada |

### Objetivo final (tras mejoras)

| Parámetro | Valor |
|-----------|-------|
| **Placa base** | BTT SKR Mini E3 V3.0 (32-bit) |
| **SBC (ordenador)** | Orange Pi Zero 3 (1 GB RAM) |
| **Firmware** | Klipper + Fluidd / Mainsail |
| **Toolhead** | Mini Stealth v2 (shroud estilo Voron) |
| **Extrusor** | Sharkfin + BMG Clone (direct drive) |
| **Hotend** | CHC V6 Volcano (alto caudal) |
| **Refrigeración capa** | 2× ventilador 4010 radial (dual simétrico) |
| **Nivelación** | CR-Touch (autonivelado mesh) |
| **Cinemática futura** | CoreXY (Fase 3) |

---

## 🗂️ Estructura del repositorio

```
UGR-A20M/
│
├── README.md                    ← Este archivo
├── CHANGELOG.md                 ← Historial de cambios
├── LICENSE                      ← CC BY-SA 4.0
│
├── docs/
│   ├── fase-0/
│   │   └── 00_especificaciones_base.md
│   ├── fase-1/
│   │   ├── electronica/
│   │   │   └── 01_skr_klipper.md
│   │   ├── extrusor/
│   │   │   └── 02_sharkfin_bmg.md
│   │   └── toolhead/
│   │       └── 03_chc_volcano_crtouch.md
│   ├── fase-2/
│   │   └── 04_guias_lineales.md
│   ├── fase-3/
│   │   └── 05_corexy_t250.md
│   └── img/
│       └── banner-ugr-a20m.png
│
├── hardware/
│   ├── bom/
│   │   └── BOM_fase1.md         ← Lista de materiales con precios y links
│   ├── prints/                  ← STLs impresos para el proyecto
│   └── electronica/             ← Esquemas de conexión
│
├── firmware/
│   ├── klipper/
│   │   ├── config/
│   │   │   └── printer.cfg      ← Configuración Klipper para A20M
│   │   └── macros/
│   │       └── macros.cfg       ← Macros personalizadas
│   └── marlin/                  ← Configuración Marlin (referencia)
│
└── photos/
    ├── estado-inicial/          ← Fotos antes de modificaciones
    ├── fase-1/                  ← Fotos del proceso fase 1
    └── fase-2/                  ← Fotos del proceso fase 2
```

---

## 📦 Bill of Materials — Resumen Fase 1

> Documento completo: [`hardware/bom/BOM_fase1.md`](hardware/bom/BOM_fase1.md)

| Componente | Referencia | Precio aprox. |
|------------|------------|--------------|
| Placa BTT SKR Mini E3 V3.0 | AliExpress | ~25 € |
| Orange Pi Zero 3 (1 GB) | AliExpress | ~25 € |
| MicroSD SanDisk 32 GB | Amazon | ~8 € |
| Extrusor Sharkfin (STL) | KayosMaker GitHub | Gratis |
| Toolhead Mini Stealth v2 (STL) | atrushing GitHub | Gratis |
| Motor NEMA 17 pancake | AliExpress | ~5 € |
| BMG Clone (engranajes) | AliExpress | ~5 € |
| Hotend CHC V6 Volcano | AliExpress | ~12 € |
| Ventiladores 4010 24V ×2 (capa) | AliExpress | ~3 € |
| Ventilador 2510 24V ×1 (hotend) | AliExpress | ~5 € |
| CR-Touch autonivelador | AliExpress | ~12 € |
| Insertos M3 ×5 | AliExpress | ~1 € |
| Tornillería variada | AliExpress | ~3 € |
| **Total estimado** | | **~104 €** |

---

## 🔗 Recursos y referencias clave

### Hardware
- [Sharkfin Extruder (KayosMaker)](https://github.com/KayosMaker/Sharkfin_Extruder) — Extrusor direct drive
- [Mini Stealth v2 (atrushing)](https://github.com/atrushing/Mini_Stealth) — Shroud toolhead estilo Voron Stealthburner
- [Adaptador Bambu hotend a V6 (Cults3D)](https://cults3d.com/es/modelo-3d/herramientas/bambu-lab-s-hotend-adapter-to-v6-size) — Si fuera necesario para el hotend

### Firmware
- [Klipper (Klipper3d.org)](https://www.klipper3d.org/)
- [Fluidd (fluidd.xyz)](https://fluidd.xyz/)
- [Mainsail (docs.mainsail.xyz)](https://docs.mainsail.xyz/)
- [KIAUH — instalador Klipper](https://github.com/dw-0/kiauh)

### Comunidad Voron
- [Voron Design](https://vorondesign.com/)
- [Voron Discord](https://discord.gg/voron)

---

## 📸 Documentación fotográfica

Cada fase incluirá:
- 📷 Fotografías antes/durante/después
- 📐 Archivos STL/STEP de piezas impresas
- 📋 BOM detallada con precios y enlaces
- ⚙️ Configuraciones de firmware comentadas
- 📊 Comparativas de rendimiento (velocidad, calidad, ruido)

---

## 👤 Créditos

**Autor:** Álvaro González Jiménez  
**Email:** alvarogj1@correo.ugr.es  
**Proyecto apoyado por:** Universidad de Granada (UGR) — 2025  

**Inspiración técnica:**
- Comunidad [Voron Design](https://vorondesign.com/)
- Comunidad maker y grupos de impresión 3D UGR

---

## 📄 Licencia

Este proyecto se distribuye bajo licencia **[CC BY-SA 4.0](LICENSE)** — uso libre con atribución y misma licencia.

---

> *"La investigación aplicada es el puente entre la curiosidad y la innovación."*  
> — Proyecto UGR-A20M, Universidad de Granada
