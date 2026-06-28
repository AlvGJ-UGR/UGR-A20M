# 🧵 Guía de materiales — UGR-A20M

Materiales compatibles con la build UGR-A20M: extrusor directo Sharkfin + hotend CHC V6 Volcano (hasta 285 °C) + cama caliente hasta 120 °C.

Los **parámetros de slicer** (temperaturas, velocidades, retracción) están en [`docs/slicer_settings.md`](slicer_settings.md). Esta guía se centra en **cuándo usar cada material, cómo prepararlo y qué precauciones tomar**.

---

## Tabla de compatibilidad

| Material | Compatible | Temp. hotend | Temp. cama | Dificultad | Requisito especial |
|----------|:----------:|-------------|-----------|------------|-------------------|
| **PLA** | ✅ | 200–220 °C | 55–65 °C | Baja | — |
| **PLA+** | ✅ | 210–230 °C | 55–65 °C | Baja | — |
| **SILK PLA** | ✅ | 215–230 °C | 55–60 °C | Baja | — |
| **WOOD PLA** | ✅ | 200–220 °C | 55–60 °C | Baja | Boquilla ≥ 0.4 mm |
| **PETG** | ✅ | 230–245 °C | 75–85 °C | Baja-media | No cristal desnudo |
| **ABS** | ✅ | 240–255 °C | 100–110 °C | Media | Recinto cerrado |
| **ASA** | ✅ | 245–260 °C | 90–105 °C | Media | Recinto cerrado |
| **TPU** | ✅ | 220–240 °C | 30–45 °C | Media | Solo direct drive |
| **Nylon (PA)** | ⚠️ | 250–270 °C | 70–90 °C | Alta | Secar siempre |
| **PC** | ⚠️ | 260–280 °C | 100–120 °C | Muy alta | Límite del Volcano |
| **CF-PLA / CF-PETG** | ⚠️ | Normal | Normal | Media | Boquilla hardened |
| **GF / metal-fill** | ⚠️ | Normal | Normal | Media | Boquilla ruby |
| **Resina** | ❌ | — | — | — | No compatible FDM |

> ⚠️ **Materiales abrasivos** (CF, GF, metal-fill): la boquilla de latón se desgasta en horas. Usar boquilla de acero endurecido o ruby antes de imprimir.

---

## PLA

El material de referencia. Fácil de imprimir, ecológico (base vegetal) y buena calidad superficial.

**Úsalo para:** prototipos, piezas decorativas, modelos, maquetas.  
**Evítalo en:** entornos > 55 °C (interior de coche, cerca del hotend en operación).  
**Superficie de adhesión:** PEI, cristal liso, cinta azul. Libera bien en frío.

---

## PETG

El mejor equilibrio resistencia/facilidad para piezas funcionales. Más resistente que PLA al calor y al impacto, sin la dificultad del ABS.

**Úsalo para:** piezas funcionales de uso general, exterior, contenedores de alimentos o líquidos.  
**Evítalo en:** aplicaciones que necesiten rigidez extrema (es algo más flexible que el PLA).  
**Superficie de adhesión:** PEI texturizado, cristal + laca fina. **Nunca cristal desnudo** — se adhiere tan fuerte que puede romperse al retirar la pieza.

---

## ABS

Buena resistencia mecánica y química. La dificultad proviene de la contracción al enfriarse que provoca warping y delaminación.

**Úsalo para:** carcasas, piezas del propio proyecto (extrusor Sharkfin, Mini Stealth), temperatura de trabajo hasta 90–100 °C.  
**Evítalo sin:** recinto cerrado y cama correctamente calibrada.  
**Superficie de adhesión:** PEI, kapton + ABS-juice. Recinto a ≥ 45 °C.  
**ABS-juice:** disolver restos de ABS en acetona (5 g/100 ml). Aplicar una capa fina en la cama caliente.  
**Vapores:** el ABS emite vapores al imprimir. Ventilar la zona o usar filtro de carbono activo.

---

## ASA

Prácticamente idéntico al ABS en propiedades mecánicas, pero con mejor resistencia a la radiación UV y a la intemperie. Es el material elegido para las piezas del proyecto.

**Úsalo para:** piezas de exterior, exposición solar prolongada, sustituto del ABS en entornos UV.  
**Superficie de adhesión:** PEI, kapton. Igual de exigente que el ABS respecto al recinto.

---

## TPU (flexible)

Elástico, resistente al desgaste y a los aceites. **Solo imprimible con extrusión directa** — una de las ventajas clave de este proyecto frente al Bowden original.

**Úsalo para:** fundas, juntas, agarraderas, piezas que absorban impactos.  
**Velocidad:** máximo 30–40 mm/s. El TPU no tolera cambios bruscos de velocidad.  
**Retracción:** mínima (0.5–1.0 mm). Demasiada retracción provoca atascos en material flexible.

---

## Nylon (PA)

Excelente resistencia mecánica y química. El talón de Aquiles es su higroscopicidad: absorbe humedad del ambiente en horas.

**Úsalo para:** engranajes, poleas, piezas de alta carga mecánica.  
**Secar siempre:** 8–12 h a 70 °C antes de imprimir. El nylon húmedo produce burbujas, capas débiles y vapor visible en la boquilla.  
**Superficie de adhesión:** garolita, PEI a alta temperatura.

---

## PC (Policarbonato)

El material más exigente de esta lista. Muy alta resistencia al impacto y temperatura de trabajo hasta 120 °C.

**Úsalo para:** protecciones de impacto, piezas structurales críticas.  
**Temperatura:** al límite del CHC V6 Volcano (260–280 °C). Verificar que el hotend aguanta antes de imprimir.  
**Recinto:** imprescindible a ≥ 60 °C. Sin recinto el warping es severo.

---

## Materiales abrasivos (CF, GF, metal-fill)

Cualquier material con relleno de fibra de carbono, fibra de vidrio o partículas metálicas destruye la boquilla de latón en pocas horas.

| Material | Vida boquilla latón | Solución |
|----------|---------------------|---------|
| CF-PLA / CF-PETG | 10–30 h | Boquilla hardened steel |
| GF-Nylon | < 10 h | Boquilla hardened steel |
| Metal-fill | < 5 h | Boquilla ruby |

Las boquillas hardened steel para CHC V6 están disponibles en AliExpress por ~3–5 €. La boquilla ruby es la mejor opción pero cuesta ~30–50 €.

---

## Secado de filamento

Síntomas de filamento húmedo: crepitado en la boquilla, burbujas en el filamento extruido, stringing excesivo, capas débiles, vapor visible.

| Material | Temperatura de secado | Tiempo mínimo |
|----------|-----------------------|--------------|
| PLA | 45–50 °C | 4 h |
| PETG | 55–65 °C | 4 h |
| ABS / ASA | 60–80 °C | 4 h |
| TPU | 50–60 °C | 4 h |
| Nylon (PA) | 70–80 °C | **8–12 h** |
| PC | 80–100 °C | 6 h |

**Equipos:** deshidratador de alimentos (más recomendado, temperatura precisa), caja de filamento con calefactor (Polymaker PolyDryer, SUNLU FilaDryer), u horno doméstico verificando temperatura con termómetro externo.

---

## Superficies de cama

| Superficie | Mejor para | Adherencia | Liberación en frío |
|------------|-----------|------------|-------------------|
| Cristal templado liso | PLA, ABS+laca | Media | Excelente |
| PEI texturizado | PLA, PETG, ABS, ASA, TPU | Alta | Muy buena |
| PEI liso | PETG, Nylon | Alta | Buena |
| Kapton + ABS-juice | ABS, ASA | Muy alta | Regular |

---

## Boquillas recomendadas por material

| Boquilla | Material | Precio aprox. | Cuándo usar |
|----------|---------|--------------|-------------|
| Latón 0.4 mm | Estándar | ~1 € | PLA, PETG, ABS, ASA, TPU |
| Latón 0.6 mm | Alto caudal | ~1 € | Cualquier material no abrasivo |
| Hardened steel 0.4 mm | Abrasivos | ~3–5 € | CF, GF, metal-fill |
| Ruby 0.4 mm | Muy abrasivos | ~30–50 € | Metal-fill, CF intensivo |
