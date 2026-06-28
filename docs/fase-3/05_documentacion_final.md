# 📊 Fase 3 — Documentación final y publicación

**Estado:** 🔜 Planificada — iniciar tras completar y validar la Fase 2

---

## Objetivo

Cerrar el proyecto con una documentación de calidad que permita a cualquier persona reproducir la build, comparar resultados reales antes/después y generar un informe formal para la Universidad de Granada.

---

## 3.1 Comparativas de rendimiento

Benchmarks antes/después de cada fase con metodología reproducible. El objetivo es medir las mismas métricas siempre en las mismas condiciones.

### Métricas a registrar

| Métrica | Herramienta | Unidad | Condiciones |
|---------|-------------|--------|-------------|
| Velocidad máxima estable | OrcaSlicer — Speed Benchy | mm/s | PLA, 0.2 mm capa |
| Calidad de esquinas (ringing) | Cubo de ringing | Subjetivo 1–10 | PLA, 100 mm/s |
| Stringing | Torre de stringing | Hilos contados | PLA, 200 °C |
| Adhesión primera capa | Visual + % de despegue | % | PLA, z_offset calibrado |
| Ruido en operación | App de decibelios (móvil a 30 cm) | dB(A) | 60 mm/s, sin ventilador capa |
| Tiempo calentamiento hotend | Cronómetro | segundos | De 25 °C a 200 °C |
| Precisión dimensional X | Calibre sobre cubo 20×20×20 | mm | PLA, 0.2 mm, 20% |
| Precisión dimensional Y | Calibre sobre cubo 20×20×20 | mm | PLA, 0.2 mm, 20% |
| Precisión dimensional Z | Calibre sobre cubo 20×20×20 | mm | PLA, 0.2 mm, 20% |

### Tabla de resultados (rellenar al completar cada fase)

| Métrica | Stock (Fase 0) | Fase 1 | Fase 2 | Mejora total |
|---------|---------------|--------|--------|-------------|
| Velocidad máx. estable | ~60 mm/s | — | — | — |
| Ruido operación | — dB(A) | — dB(A) | — dB(A) | — |
| Tiempo calentamiento | — s | — s | — s | — |
| Dim. X (objetivo 20.00) | — mm | — mm | — mm | — |
| Dim. Y (objetivo 20.00) | — mm | — mm | — mm | — |
| Dim. Z (objetivo 20.00) | — mm | — mm | — mm | — |

### Modelos de test a imprimir

| Modelo | Propósito | Fuente | Imprimir en |
|--------|-----------|--------|-------------|
| Cubo 20×20×20 mm | Precisión dimensional | [Printables #5765](https://www.printables.com/model/5765) | Todas las fases |
| Benchy | Benchmark general | [3DBenchy.com](https://www.3dbenchy.com/) | Todas las fases |
| Torre de temperatura | Temperatura óptima por material | [Printables #4166](https://www.printables.com/model/4166) | Fase 1 |
| Torre de stringing | Retracción y PA | [Printables #45769](https://www.printables.com/model/45769) | Fase 1 |
| Overhang test | Ángulos máximos sin soporte | [Printables #4548](https://www.printables.com/model/4548) | Fase 1 |
| Ringing tower | Verificar Input Shaping | [Printables #4301](https://www.printables.com/model/4301) | Tras calibrar IS |

---

## 3.2 Galería fotográfica completa

Ver checklist detallado en [`photos/README.md`](../../photos/README.md).

**Resumen de fotos clave** para la comparativa final:

```
photos/
├── estado-inicial/
│   ├── YYYY-MM-DD_vista-frontal-original.jpg
│   ├── YYYY-MM-DD_placa-gt2560.jpg
│   ├── YYYY-MM-DD_extrusor-bowden-original.jpg
│   └── YYYY-MM-DD_benchy-stock.jpg
├── fase-1/
│   ├── YYYY-MM-DD_electronica-skr-instalada.jpg
│   ├── YYYY-MM-DD_sharkfin-montado.jpg
│   ├── YYYY-MM-DD_mini-stealth-completo.jpg
│   ├── YYYY-MM-DD_crtouch-instalado.jpg
│   └── YYYY-MM-DD_benchy-fase1.jpg
└── fase-2/
    ├── YYYY-MM-DD_guias-mgn12h-eje-x.jpg
    ├── YYYY-MM-DD_guias-mgn12h-eje-y.jpg
    └── YYYY-MM-DD_benchy-fase2.jpg
```

---

## 3.3 GitHub Pages

La web del proyecto ya está creada y operativa en:

**→ [https://alvgj-ugr.github.io/UGR-A20M/](https://alvgj-ugr.github.io/UGR-A20M/)**

Para activarla en el repositorio de GitHub:

1. Ir a **Settings → Pages**
2. Source: `Deploy from a branch`
3. Branch: `main` · Folder: `/docs`
4. Guardar

La página `docs/index.html` ya está lista y todos sus links apuntan al repositorio de GitHub.

---

## 3.4 Informe PDF para la UGR

Documento formal para entregar a la Universidad de Granada. Estructura propuesta:

### Contenido del informe

| Sección | Contenido | Páginas aprox. |
|---------|-----------|---------------|
| Portada | Logo UGR, título, autor, fecha | 1 |
| Resumen ejecutivo | Objetivos, metodología, resultados clave | 1 |
| Introducción | Motivación, estado del arte en impresión 3D maker | 2–3 |
| Fase 0 — Análisis inicial | Specs A20M, problemas identificados | 2 |
| Fase 1 — Modernización | Electrónica, extrusor, toolhead, calibración | 6–8 |
| Fase 2 — Estructura | Guías lineales MGN12H | 3–4 |
| Resultados y comparativas | Tablas y fotos antes/después | 3–4 |
| Conclusiones | Logros, limitaciones, trabajo futuro | 1–2 |
| Presupuesto total | BOM consolidada Fase 1 + Fase 2 | 1 |
| Referencias | Repositorios, documentación, comunidades | 1 |

**Total estimado: 20–25 páginas**

### Generación del PDF

**Opción A — Pandoc (automático desde Markdown):**
```bash
# Instalar dependencias
sudo apt install pandoc texlive-xetex texlive-lang-spanish fonts-liberation

# Generar PDF desde todos los documentos en orden
pandoc \
  docs/fase-0/00_especificaciones_base.md \
  docs/fase-1/electronica/01_skr_klipper.md \
  docs/fase-1/extrusor/02_sharkfin_bmg.md \
  docs/fase-1/toolhead/03_mini_stealth_chc_crtouch.md \
  docs/guia_calibracion.md \
  docs/fase-2/04_guias_lineales.md \
  docs/slicer_settings.md \
  docs/mantenimiento.md \
  --output informe-ugr-a20m.pdf \
  --pdf-engine=xelatex \
  --toc \
  --toc-depth=2 \
  --metadata title="Proyecto UGR-A20M: Modernización de impresora 3D Geeetech A20M" \
  --metadata author="Álvaro González Jiménez — Universidad de Granada" \
  --metadata date="2025" \
  --metadata lang=es \
  -V geometry:margin=2.5cm \
  -V fontsize=11pt \
  -V mainfont="Liberation Serif" \
  -V monofont="Liberation Mono" \
  -V colorlinks=true \
  -V linkcolor=NavyBlue
```

> Si hay imágenes en los documentos, ejecutar el comando desde la raíz del repositorio para que las rutas relativas se resuelvan correctamente.

**Opción B — Overleaf con plantilla UGR:**
- Usar la [plantilla LaTeX oficial de la UGR](https://www.ugr.es/universidad/servicios/comunicacion-informacion/imagen-corporativa)
- Copiar el contenido de los `.md` y formatear manualmente

---

## 3.5 Release final en GitHub

Al completar el proyecto, publicar el Release `v2.0.0`:

1. GitHub → **Releases → Draft a new release**
2. Tag: `v2.0.0`
3. Título: `UGR-A20M v2.0.0 — Build completa (Fase 1 + Fase 2)`
4. Adjuntar como assets:
   - `printer.cfg` con valores reales calibrados
   - `macros.cfg` final
   - `informe-ugr-a20m.pdf`
5. Descripción con:
   - Resumen de lo conseguido
   - Tabla de métricas clave (velocidad, ruido, precisión)
   - Fotos del antes/después

---

## Checklist Fase 3

### Benchmarks
- [ ] Métricas stock (Fase 0) registradas con metodología documentada
- [ ] Métricas Fase 1 registradas con misma metodología
- [ ] Métricas Fase 2 registradas con misma metodología
- [ ] Tabla comparativa completa actualizada en este documento

### Fotografías
- [ ] Checklist de `photos/README.md` completado para estado inicial
- [ ] Checklist de `photos/README.md` completado para Fase 1
- [ ] Checklist de `photos/README.md` completado para Fase 2

### Web
- [ ] GitHub Pages activado (Settings → Pages → `/docs`)
- [ ] Web accesible en `https://alvgj-ugr.github.io/UGR-A20M/`
- [ ] Todos los links del `index.html` verificados

### Firmware
- [ ] `printer.cfg` actualizado con valores reales de calibración (no placeholders)
- [ ] `rotation_distance` calibrado y verificado (< 1% error)
- [ ] PID hotend y cama calibrados y guardados en SAVE_CONFIG
- [ ] `z_offset` calibrado y guardado
- [ ] `x_offset` / `y_offset` CR-Touch medidos y actualizados
- [ ] `pressure_advance` calibrado
- [ ] Input Shaping calibrado (opcional, requiere ADXL345)

### Documentación
- [ ] Tabla de resultados de benchmarks rellenada en este documento
- [ ] `CHANGELOG.md` cerrado con versión `v2.0.0`
- [ ] Informe PDF generado y revisado
- [ ] Topics del repositorio GitHub actualizados: `3d-printing`, `klipper`, `voron`, `ugr`, `geeetech`, `maker`

### Publicación
- [ ] Release `v2.0.0` publicado en GitHub con PDF adjunto
- [ ] Repositorio anunciado en foros/grupos relevantes (opcional)
