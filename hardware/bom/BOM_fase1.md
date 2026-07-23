# 📦 Bill of Materials — Fase 1

**Proyecto:** UGR-A20M  
**Fase:** 1 — Electrónica + Extrusor Directo + Toolhead Mini Stealth  
**Última actualización:** 2025-04

---

## 🖥️ Electrónica principal

| # | Componente | Especificación | Enlace | Precio aprox. |
|---|------------|---------------|--------|--------------|
| 1 | Placa base | BTT SKR Mini E3 V3.0 (STM32G0B1, 32-bit, TMC2209 integrados) | [AliExpress](https://es.aliexpress.com/item/1005003521537547.html?isdl=y&aff_fsk=_DdG0l5v&src=Globerada&aff_platform=aff_feeds&gatewayAdapt=glo2esp&aff_short_key=_DdG0l5v&pdp_npi=4%40dis%21EUR%2132.08%2127.59%21%21%21%21%21%40%2112000057683004771%21afff%21%21%21&dp=globerada_css-6a61e1ff7e486)| ~25 € |
| 2 | SBC | Orange Pi Zero 3 — 1 GB RAM (Klipper host) | [AliExpress](https://es.aliexpress.com/item/1005005785695181.html?spm=a2g0o.detail.pcDetailTopMoreOtherSeller.1.3909EK60EK60bl&gps-id=pcDetailTopMoreOtherSeller&scm=1007.40050.354490.0&scm_id=1007.40050.354490.0&scm-url=1007.40050.354490.0&pvid=5cf8132f-c88f-45c6-9edd-e048b550c64b&_t=gps-id%3ApcDetailTopMoreOtherSeller%2Cscm-url%3A1007.40050.354490.0%2Cpvid%3A5cf8132f-c88f-45c6-9edd-e048b550c64b%2Ctpp_buckets%3A668%232846%238114%231999&pdp_ext_f=%7B%22order%22%3A%22664%22%2C%22spu_best_type%22%3A%22price%22%2C%22eval%22%3A%221%22%2C%22sceneId%22%3A%2230050%22%2C%22fromPage%22%3A%22recommend%22%7D&pdp_npi=6%40dis%21EUR%2130.79%2130.79%21%21%2134.34%2134.34%21%400b88abba17847998920101397e11b0%2112000034349280765%21rec%21ES%21%21ABXZ%211%210%21n_tag%3A-29910%3Bd%3A8bf554f9%3Bm03_new_user%3A-29895&utparam-url=scene%3ApcDetailTopMoreOtherSeller%7Cquery_from%3A%7Cx_object_id%3A1005005785695181%7C_p_origin_prod%3A) | ~25 € |
| 3 | MicroSD | SanDisk 32 GB, mínimo 16 GB, Class 10 | [Amazon ES](https://www.amazon.es/SanDisk-Tarjeta-microSDXC-Adaptador-Rendimiento/dp/B0B7NXBM6P) | ~8 € |

**Subtotal: ~58 €**

---

## 🔩 Extrusor — Sharkfin + BMG Clone

Extrusor de extrusión directa open-source de KayosMaker. Relación de reducción ~3.5:1 con engranajes BMG.

| # | Componente | Enlace | Precio aprox. |
|---|------------|--------|--------------|
| 1 | STL Sharkfin Extruder | [GitHub KayosMaker](https://github.com/KayosMaker/Sharkfin_Extruder) | Gratis |
| 2 | Motor NEMA 17 pancake 20mm, ~1A | [AliExpress](https://es.aliexpress.com/item/1005005933469472.html) | ~2–5 € |
| 3 | BMG Clone — kit engranajes doble | [AliExpress](https://es.aliexpress.com/item/1005003423850142.html) | ~5 € |
| 4 | Insertos termofijados M3 ×5 | [AliExpress](https://es.aliexpress.com/item/1005008285787978.html) | ~1 € |
| 5 | Arandela M5 × 0.5 mm, ×1 | — | <1 € |

### Tornillería extrusor

| Referencia | Cant. | Enlace |
|------------|-------|--------|
| M3×25 SHCS | 1 | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) |
| M3×16 BHCS | 2 | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) |
| M3×10 BHCS | 2 | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) |
| M3×8 BHCS  | 3 | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) |

> Material de impresión: **ABS o ASA** (resistencia mínima 90 °C). Ver parámetros en [`hardware/prints/README.md`](../prints/README.md).

**Subtotal: ~14 €**

---

## 🖨️ Toolhead — Mini Stealth v2 + CHC V6 Volcano + CR-Touch

Shroud estilo Voron Stealthburner (~5/8 del tamaño original), con refrigeración dual de capa y soporte integrado para sonda.

| # | Componente | Enlace | Precio aprox. |
|---|------------|--------|--------------|
| 1 | STL Mini Stealth v2 (core + shroud + accesorios) | [GitHub atrushing](https://github.com/atrushing/Mini_Stealth) | Gratis |
| 2 | Hotend CHC V6 Volcano, 24V, NTC 100k | [AliExpress](https://es.aliexpress.com/item/1005003849153931.html) | ~12 € |
| 3 | Ventiladores 4010 24V radial soplador ×2 (refrigeración capa) | [AliExpress](https://es.aliexpress.com/item/1005003371996395.html) | ~3 € |
| 4 | Ventilador 2510 24V axial ×1 (refrigeración hotend) | [AliExpress](https://es.aliexpress.com/item/1005006831848917.html) | ~5 € |
| 5 | Extensores cable JST ventilador | [AliExpress](https://es.aliexpress.com/item/1005005491577017.html) | ~2 € |
| 6 | CR-Touch original Creality | [AliExpress](https://es.aliexpress.com/item/1005009035812836.html) | ~12 € |

### Tornillería toolhead

| Referencia | Cant. | Uso | Enlace |
|------------|-------|-----|--------|
| M3×40 BHCS | 2 | Fijar toolhead al carro X | [AliExpress](https://es.aliexpress.com/item/1005009901230624.html) |
| M2.5×8 BHCS | 2 | Montaje hotend al core | [AliExpress](https://es.aliexpress.com/item/4001072025844.html) |
| M2.5×6 BHCS | 2 | Montaje hotend | [AliExpress](https://es.aliexpress.com/item/4001072025844.html) |
| M3×8 BHCS | 2 | Fijar extrusor al core | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) |
| M3×6 BHCS | 2 | Puerta de cables | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) |
| M2.5×6 FHCS | 2 | Bracket CR-Touch (avellanado) | [AliExpress](https://es.aliexpress.com/item/4001072025844.html) |

**Subtotal: ~34 €**

---

## 📊 Resumen de costes

| Subsistema | Coste |
|------------|-------|
| Electrónica (SKR Mini E3 V3 + Orange Pi Zero 3 + SD) | ~58 € |
| Extrusor (Sharkfin + BMG + NEMA 17 pancake) | ~14 € |
| Toolhead (Mini Stealth + CHC Volcano + ventiladores + CR-Touch) | ~34 € |
| **TOTAL FASE 1** | **~106 €** |

> Precios orientativos AliExpress / Amazon España (2025). No incluye filamento ABS/ASA (~200 g ≈ 4 €).

---

## 🖨️ Piezas a imprimir

Todas las piezas deben imprimirse en **ABS o ASA**. Ver parámetros detallados en [`hardware/prints/README.md`](../prints/README.md).

| Pieza | Fuente | Notas |
|-------|--------|-------|
| Sharkfin Body | [GitHub](https://github.com/KayosMaker/Sharkfin_Extruder) | Cuerpo principal |
| Sharkfin Latch | [GitHub](https://github.com/KayosMaker/Sharkfin_Extruder) | Palanca de tensión |
| Mini Stealth — Core | [GitHub](https://github.com/atrushing/Mini_Stealth) | Elegir core compatible con el grupo de extrusor |
| Mini Stealth — Shroud (probe-mount) | [GitHub](https://github.com/atrushing/Mini_Stealth) | Versión con soporte CR-Touch |
| Mini Stealth — Motor Bridge | [GitHub](https://github.com/atrushing/Mini_Stealth) | Gestión de cables del motor |
| Mini Stealth — Cable Door | [GitHub](https://github.com/atrushing/Mini_Stealth) | Cierre posterior |
| Mini Stealth — Strain Relief | [GitHub](https://github.com/atrushing/Mini_Stealth) | Alivio de tensión |
| Probe Bracket (CR-Touch) | [GitHub](https://github.com/atrushing/Mini_Stealth) | Soporte lateral CR-Touch |
| Adaptador Bambu → V6 (si necesario) | [Cults3D](https://cults3d.com/es/modelo-3d/herramientas/bambu-lab-s-hotend-adapter-to-v6-size) | Para compatibilidad de hotend |
