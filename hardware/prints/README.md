# 🖨️ Registro de piezas impresas — UGR-A20M

Registro de todas las piezas impresas para el proyecto, con parámetros, resultado y observaciones.

---

## 📊 Estado general

| Total piezas | Impresas | Pendientes | Fallidas |
|:------------:|:--------:|:----------:|:--------:|
| 13 | 0 | 13 | 0 |

---

## 🔩 Extrusor — Sharkfin + BMG

| # | Pieza | Fuente | Material | Temp. boquilla | Temp. cama | Relleno | Perímetros | Fecha | Resultado | Notas |
|---|-------|--------|----------|---------------|-----------|---------|-----------|-------|-----------|-------|
| 1 | Sharkfin Body | [GitHub](https://github.com/KayosMaker/Sharkfin_Extruder) | — | — | — | 40% | 4 | — | ⏳ Pendiente | — |
| 2 | Sharkfin Latch | [GitHub](https://github.com/KayosMaker/Sharkfin_Extruder) | — | — | — | 40% | 4 | — | ⏳ Pendiente | — |

---

## 🖨️ Toolhead — Mini Stealth v2

| # | Pieza | Fuente | Material | Temp. boquilla | Temp. cama | Relleno | Perímetros | Fecha | Resultado | Notas |
|---|-------|--------|----------|---------------|-----------|---------|-----------|-------|-----------|-------|
| 3 | Core (grupo extrusor) | [GitHub](https://github.com/atrushing/Mini_Stealth) | — | — | — | 40% | 4 | — | ⏳ Pendiente | Verificar core compatible con Sharkfin |
| 4 | Shroud (probe-mount) | [GitHub](https://github.com/atrushing/Mini_Stealth) | — | — | — | 40% | 4 | — | ⏳ Pendiente | Versión con soporte CR-Touch |
| 5 | Motor Bridge | [GitHub](https://github.com/atrushing/Mini_Stealth) | — | — | — | 40% | 4 | — | ⏳ Pendiente | Gestión de cables del motor |
| 6 | Cable Door | [GitHub](https://github.com/atrushing/Mini_Stealth) | — | — | — | 40% | 4 | — | ⏳ Pendiente | Cierre posterior |
| 7 | Strain Relief | [GitHub](https://github.com/atrushing/Mini_Stealth) | — | — | — | 40% | 4 | — | ⏳ Pendiente | Alivio de tensión de cables |
| 8 | Probe Bracket (CR-Touch) | [GitHub](https://github.com/atrushing/Mini_Stealth) | — | — | — | 40% | 4 | — | ⏳ Pendiente | Soporte lateral para CR-Touch |

---

## 🔧 Adaptadores

| # | Pieza | Fuente | Material | Temp. boquilla | Temp. cama | Relleno | Perímetros | Fecha | Resultado | Notas |
|---|-------|--------|----------|---------------|-----------|---------|-----------|-------|-----------|-------|
| 9 | Adaptador Bambu → V6 | [Cults3D](https://cults3d.com/es/modelo-3d/herramientas/bambu-lab-s-hotend-adapter-to-v6-size) | — | — | — | 40% | 4 | — | ⏳ Pendiente | Solo si necesario para el hotend |

---

## 🔜 Fase 2 — Guías lineales (pendiente de diseño)

| # | Pieza | Fuente | Material | Fecha | Resultado | Notas |
|---|-------|--------|----------|-------|-----------|-------|
| 10 | Soporte guía lineal X | Por definir | — | — | ⏳ Pendiente | — |
| 11 | Soporte guía lineal Y | Por definir | — | — | ⏳ Pendiente | — |
| 12 | Carro X (MGN12H) | Por definir | — | — | ⏳ Pendiente | — |
| 13 | Tensor correa X/Y | Por definir | — | — | ⏳ Pendiente | — |

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

## 📌 Parámetros de referencia para ABS/ASA

Estos son los parámetros base recomendados para todas las piezas del proyecto. Ajustar según el material y marca concretos.

| Parámetro | ABS | ASA |
|-----------|-----|-----|
| Temperatura boquilla | 240–250°C | 250–260°C |
| Temperatura cama | 100–105°C | 90–100°C |
| Temperatura recinto | 45–50°C | 40–45°C |
| Refrigeración de capa | 0% | 15–30% máx. |
| Velocidad | 40–60 mm/s | 40–60 mm/s |
| Primera capa | 20 mm/s | 20 mm/s |
| Relleno | 40% gyroid o cúbico | 40% gyroid o cúbico |
| Perímetros | 4 | 4 |
| Capas sólidas sup/inf | 5 | 5 |
| Retracción (direct drive) | 0.8–1.2 mm | 0.8–1.2 mm |

> ⚠️ Imprimir en recinto cerrado para evitar warping, especialmente con ABS.
