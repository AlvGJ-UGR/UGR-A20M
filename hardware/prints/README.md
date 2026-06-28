# 🖨️ Registro de piezas impresas — UGR-A20M

Registro de todas las piezas impresas para el proyecto, con parámetros, resultado y observaciones.

---

## 📊 Estado general

| Total piezas | Impresas | Pendientes | Fallidas |
|:------------:|:--------:|:----------:|:--------:|
| 13 | 0 | 13 | 0 |

> Actualizar este contador cada vez que se complete o falle una pieza.

---

## 🔩 Extrusor — Sharkfin + BMG

| # | Pieza | Fuente | Material | Temp. boquilla | Temp. cama | Relleno | Perímetros | Fecha | Resultado | Notas |
|---|-------|--------|----------|---------------|-----------|---------|-----------|-------|-----------|-------|
| 1 | Sharkfin Body | [GitHub](https://github.com/KayosMaker/Sharkfin_Extruder) | ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Imprimir en la orientación indicada en el repo |
| 2 | Sharkfin Latch | [GitHub](https://github.com/KayosMaker/Sharkfin_Extruder) | ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Misma orientación que el body |

---

## 🖨️ Toolhead — Mini Stealth v2

| # | Pieza | Fuente | Material | Temp. boquilla | Temp. cama | Relleno | Perímetros | Fecha | Resultado | Notas |
|---|-------|--------|----------|---------------|-----------|---------|-----------|-------|-----------|-------|
| 3 | Core (grupo extrusor) | [GitHub](https://github.com/atrushing/Mini_Stealth) | ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Usar core del grupo Orbiter/BMG — perfil similar al Sharkfin |
| 4 | Shroud (probe-mount) | [GitHub](https://github.com/atrushing/Mini_Stealth) | ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Versión con soporte CR-Touch derecho o izquierdo según medición |
| 5 | Motor Bridge | [GitHub](https://github.com/atrushing/Mini_Stealth) | ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Gestión de cables del motor |
| 6 | Cable Door | [GitHub](https://github.com/atrushing/Mini_Stealth) | ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Cierre posterior del core |
| 7 | Strain Relief | [GitHub](https://github.com/atrushing/Mini_Stealth) | ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Alivio de tensión del mazo de cables |
| 8 | Probe Bracket (CR-Touch) | [GitHub](https://github.com/atrushing/Mini_Stealth) | ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Soporte lateral para CR-Touch |

---

## 🔧 Adaptadores

| # | Pieza | Fuente | Material | Temp. boquilla | Temp. cama | Relleno | Perímetros | Fecha | Resultado | Notas |
|---|-------|--------|----------|---------------|-----------|---------|-----------|-------|-----------|-------|
| 9 | Adaptador Bambu → V6 | [Cults3D](https://cults3d.com/es/modelo-3d/herramientas/bambu-lab-s-hotend-adapter-to-v6-size) | ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Solo si el mount del hotend no encaja directamente |

---

## 🔜 Fase 2 — Guías lineales MGN12H

> Buscar adaptadores existentes antes de diseñar: [Printables — A20M MGN12](https://www.printables.com/search/models?q=geeetech+a20+mgn12) · [Ender 3 MGN12 X axis](https://www.printables.com/search/models?q=ender+3+mgn12+x+axis) (geometría similar, posiblemente adaptable)

| # | Pieza | Función | Material | Temp. boquilla | Temp. cama | Relleno | Perímetros | Fecha | Resultado | Notas |
|---|-------|---------|----------|---------------|-----------|---------|-----------|-------|-----------|-------|
| 10 | Adaptador carro X → Mini Stealth | Conecta el carro MGN12H con el toolhead | ABS/ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Verificar en Printables; si no existe, adaptar modelo de Ender 3 |
| 11 | Soporte cama izquierdo (Y) | Fija la cama al carro Y izquierdo | ABS/ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Medir distancia carro → superficie de cama antes de diseñar |
| 12 | Soporte cama derecho (Y) | Fija la cama al carro Y derecho | ABS/ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Simétrico al izquierdo; deben ser coplanares |
| 13 | Tensor de correa X (si necesario) | Mantiene tensión de correa tras el cambio de carro | ABS/ASA | 255 °C | 95 °C | 40% gyroid | 4 | — | ⏳ Pendiente | Probar primero el tensor original antes de imprimir uno nuevo |

---

## 📋 Cómo actualizar este registro

Cuando imprimas una pieza, rellena todas las columnas y cambia el estado:

| Icono | Significado |
|-------|-------------|
| ⏳ Pendiente | Aún no impresa |
| 🟡 En progreso | Imprimiéndose ahora |
| ✅ OK | Impresa y validada |
| ❌ Fallida | Fallo durante la impresión |
| 🔁 Reimpresión | Impresa pero requiere mejora |

**Ejemplo de fila completada:**
```
| 1 | Sharkfin Body | GitHub | ASA rojo | 255°C | 90°C | 40% gyroid | 4 | 2025-05-10 | ✅ OK | 2ª iteración, 1ª falló en capa 30 por warping |
```

---

## 📌 Parámetros de impresión

Los parámetros de temperatura, velocidad y retracción para ABS y ASA están en [`docs/slicer_settings.md`](../../docs/slicer_settings.md).

**Resumen para las piezas de este proyecto (ASA recomendado):**

| Parámetro | Valor |
|-----------|-------|
| Material recomendado | **ASA** (resistencia UV + calor) |
| Temperatura boquilla | 250–260 °C |
| Temperatura cama | 90–100 °C |
| Recinto cerrado | Imprescindible |
| Relleno | 40% gyroid |
| Perímetros | 4 |
| Capas sólidas sup/inf | 5 |
| Retracción (direct drive) | 0.8–1.2 mm |
| Refrigeración | 0–20% máx. |

> Imprimir en recinto cerrado para evitar warping. Si se usa ABS en lugar de ASA, desactivar completamente la refrigeración.
