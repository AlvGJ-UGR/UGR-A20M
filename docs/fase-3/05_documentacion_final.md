# 📊 Fase 3 — Documentación final y publicación

**Estado:** 🔜 Planificada (pendiente de completar Fases 1 y 2)

---

## Objetivo

Cerrar el proyecto con una documentación de calidad que permita a cualquier persona reproducir la build, publicar los resultados en GitHub Pages y generar un informe PDF para la Universidad de Granada.

---

## Contenidos a generar

### 3.1 Comparativas de rendimiento

Benchmarks antes/después de cada fase, con metodología reproducible.

#### Métricas a medir

| Métrica | Herramienta | Unidad |
|---------|-------------|--------|
| Velocidad máxima de impresión | OrcaSlicer speed test | mm/s |
| Calidad de esquinas (ringing) | Test de resonancia visual | Subjetivo 1–10 |
| Stringing | Torre de stringing | Hilos visibles |
| Adhesión primera capa | Visual + % de adhesión | % |
| Retracción óptima | Torre de retracción | mm |
| Ruido en operación | Aplicación móvil de decibelios | dB |
| Tiempo de calentamiento | Cronómetro | s |
| Precisión dimensional | Calibre sobre cubo 20×20×20 | mm |

#### Modelos de test recomendados

| Modelo | Propósito | Fuente |
|--------|-----------|--------|
| Cubo 20×20×20 mm | Precisión dimensional | [Printables](https://www.printables.com/model/5765) |
| Torre de temperatura | Temperatura óptima por material | [Printables](https://www.printables.com/model/4166) |
| Torre de stringing | Retracción óptima | [Printables](https://www.printables.com/model/45769) |
| Benchy | Benchmark general | [3DBenchy.com](https://www.3dbenchy.com/) |
| Overhang test | Ángulos máximos sin soporte | [Printables](https://www.printables.com/model/4548) |

---

### 3.2 Galería fotográfica completa

Completar el registro de `photos/` con:

```
photos/
├── estado-inicial/
│   ├── 2025-04-XX_vista-frontal.jpg
│   ├── 2025-04-XX_placa-gt2560.jpg
│   ├── 2025-04-XX_extrusor-bowden.jpg
│   └── 2025-04-XX_benchy-stock.jpg       ← Benchy impreso con config original
├── fase-1/
│   ├── 2025-05-XX_skr-mini-instalada.jpg
│   ├── 2025-05-XX_sharkfin-montado.jpg
│   ├── 2025-05-XX_mini-stealth-completo.jpg
│   ├── 2025-05-XX_crtouch-instalado.jpg
│   └── 2025-05-XX_primera-impresion-fase1.jpg
└── fase-2/
    ├── 2025-XX-XX_guias-mgn12h-x.jpg
    └── 2025-XX-XX_guias-mgn12h-y.jpg
```

---

### 3.3 GitHub Pages

Activar GitHub Pages para convertir el repositorio en una web de documentación navegable.

#### Activación

1. GitHub → Settings → Pages
2. Source: `Deploy from a branch`
3. Branch: `main`, carpeta: `/docs`
4. Guardar — la web estará en `https://alvgj-ugr.github.io/UGR-A20M/`

#### Archivo índice necesario

Crear `docs/index.md` con la portada del proyecto (a generar al completar Fase 2).

---

### 3.4 Informe PDF para la UGR

Generar un documento PDF formal con:

- Portada con logo UGR y datos del proyecto
- Resumen ejecutivo (1 página)
- Introducción y motivación
- Descripción de cada fase con resultados
- BOM consolidada con costes totales
- Comparativas antes/después
- Conclusiones y trabajo futuro
- Referencias bibliográficas

**Herramientas sugeridas:**
- Pandoc: `pandoc docs/**/*.md -o informe-ugr-a20m.pdf` (requiere LaTeX)
- Overleaf con plantilla UGR

---

### 3.5 Release final en GitHub

Al completar el proyecto, crear el Release `v2.0.0` en GitHub con:

- Tag: `v2.0.0`
- Título: `Proyecto UGR-A20M — Build completa`
- Adjuntar: `printer.cfg` final, `macros.cfg` final, e informe PDF
- Descripción con resumen de logros y métricas clave

---

## Checklist Fase 3

| Tarea | Estado |
|-------|--------|
| Benchmarks fase 1 completados (velocidad, calidad, ruido) | ⬜ |
| Benchmarks fase 2 completados (guías lineales) | ⬜ |
| Galería fotográfica completa (todas las fases) | ⬜ |
| `docs/index.md` creado para GitHub Pages | ⬜ |
| GitHub Pages activado | ⬜ |
| `printer.cfg` con valores reales de calibración | ⬜ |
| Informe PDF generado | ⬜ |
| Release v2.0.0 publicado en GitHub | ⬜ |
| Topics del repo actualizados en GitHub | ⬜ |
