# 📊 Fase 3 — Cierre del proyecto

**Estado:** 🔜 Planificada — iniciar tras completar y validar la Fase 2

---

## Objetivo

Cerrar el proyecto midiendo lo que se ha conseguido realmente: benchmarks antes/después con metodología reproducible, galería fotográfica completa y publicación del release final en GitHub.

---

## 3.1 Benchmarks de rendimiento

Medir siempre en las mismas condiciones para que los resultados sean comparables entre fases.

### Condiciones estándar

- **Filamento:** PLA, temperatura de fábrica recomendada, bobina secada 4 h a 45 °C
- **Perfil de slicer:** el definido en `docs/slicer_settings.md` para PLA con boquilla 0.4 mm
- **Calibración:** Pressure Advance e Input Shaping calibrados antes de medir

### Métricas

| Métrica | Herramienta | Condiciones |
|---------|-------------|-------------|
| Velocidad máxima estable | Benchy a velocidad creciente hasta que aparezcan defectos | PLA, 0.2 mm capa |
| Ruido en operación | App de decibelios, micrófono a 30 cm | 60 mm/s, ventilador capa al 50% |
| Stringing | Torre de stringing estándar | PLA, 200 °C, retracción calibrada |
| Calidad de esquinas | Cubo de ringing | PLA, 100 mm/s |
| Precisión dimensional | Calibre sobre cubo 20×20×20 mm | PLA, 0.2 mm, 20% relleno |
| Tiempo calentamiento | Cronómetro, de 25 °C a 200 °C | Hotend en reposo |

### Tabla de resultados

| Métrica | Stock (Fase 0) | Fase 1 | Fase 2 | Δ total |
|---------|---------------|--------|--------|---------|
| Velocidad máx. estable | ~60 mm/s | — | — | — |
| Ruido | — dB(A) | — dB(A) | — dB(A) | — |
| Dim. X (obj. 20.00 mm) | — mm | — mm | — mm | — |
| Dim. Y (obj. 20.00 mm) | — mm | — mm | — mm | — |
| Dim. Z (obj. 20.00 mm) | — mm | — mm | — mm | — |

### Modelos de test

| Modelo | Propósito | Fuente |
|--------|-----------|--------|
| Cubo 20×20×20 mm | Precisión dimensional | [Printables #5765](https://www.printables.com/model/5765) |
| Benchy | Benchmark general y velocidad | [3DBenchy.com](https://www.3dbenchy.com/) |
| Torre de temperatura | Temperatura óptima por material | [Printables #4166](https://www.printables.com/model/4166) |
| Torre de stringing | Calibrar retracción y PA | [Printables #45769](https://www.printables.com/model/45769) |
| Overhang test | Ángulos máximos sin soporte | [Printables #4548](https://www.printables.com/model/4548) |
| Ringing tower | Verificar Input Shaping | [Printables #4301](https://www.printables.com/model/4301) |

> Guardar todas las piezas de test impresas físicamente, con etiqueta de fecha y fase. Son la evidencia tangible de la mejora.

---

## 3.2 Galería fotográfica

Ver checklist completo en [`photos/README.md`](../../photos/README.md).

**Fotografías imprescindibles para la comparativa:**

```
photos/
├── estado-inicial/
│   ├── YYYY-MM-DD_vista-general-original.jpg
│   ├── YYYY-MM-DD_placa-gt2560.jpg
│   └── YYYY-MM-DD_benchy-stock.jpg          ← benchmark visual inicial
├── fase-1/
│   ├── YYYY-MM-DD_skr-mini-instalada.jpg
│   ├── YYYY-MM-DD_sharkfin-montado.jpg
│   ├── YYYY-MM-DD_mini-stealth-completo.jpg
│   └── YYYY-MM-DD_benchy-fase1.jpg          ← benchmark visual fase 1
└── fase-2/
    ├── YYYY-MM-DD_guias-mgn12h-instaladas.jpg
    └── YYYY-MM-DD_benchy-fase2.jpg          ← benchmark visual fase 2
```

Fotografiar los benchies siempre desde el mismo ángulo, con la misma iluminación y fondo neutro para que la comparativa sea visualmente válida.

---

## 3.3 Release final en GitHub

Al completar el proyecto, publicar el release `v2.0.0` en GitHub:

1. **GitHub → Releases → Draft a new release**
2. Tag: `v2.0.0` · Título: `UGR-A20M v2.0.0 — Build completa`
3. Adjuntar el `printer.cfg` con **valores reales calibrados** (no los placeholders del repo)
4. Descripción con la tabla de benchmarks rellena y las fotos antes/después

---

## Checklist de cierre

### Benchmarks
- [ ] Métricas stock (Fase 0) registradas
- [ ] Métricas Fase 1 registradas con la misma metodología
- [ ] Métricas Fase 2 registradas con la misma metodología
- [ ] Tabla de resultados rellenada en este documento

### Fotografías
- [ ] Galería de estado inicial completa
- [ ] Galería Fase 1 completa
- [ ] Galería Fase 2 completa

### Firmware
- [ ] `printer.cfg` con valores reales: `rotation_distance`, PID hotend, PID cama, `z_offset`, offsets CR-Touch, `pressure_advance`
- [ ] Input Shaping calibrado (si se instaló ADXL345)
- [ ] `CHANGELOG.md` cerrado en versión `v2.0.0`

### Publicación
- [ ] Topics del repo actualizados: `3d-printing`, `klipper`, `voron`, `ugr`, `geeetech`, `maker`
- [ ] Release `v2.0.0` publicado con `printer.cfg` real adjunto
