# 📸 Registro fotográfico — UGR-A20M

Documentación visual del proceso de modificación. Las fotos son tan importantes como el texto: permiten verificar el estado real de la máquina, detectar errores de montaje y comparar resultados antes/después.

---

## Estructura de carpetas

```
photos/
├── estado-inicial/    ← Fotos ANTES de tocar nada — imprescindibles
├── fase-1/            ← Proceso completo de la Fase 1
└── fase-2/            ← Proceso completo de la Fase 2
```

---

## Convención de nombres

```
YYYY-MM-DD_descripcion-en-minusculas-con-guiones.jpg
```

**Ejemplos correctos:**
```
2025-04-10_vista-frontal-original.jpg
2025-05-03_skr-mini-e3-instalada.jpg
2025-05-10_sharkfin-body-impreso-asa-rojo.jpg
2025-05-18_mini-stealth-montado-completo.jpg
2025-05-20_primera-impresion-fase1-benchy.jpg
```

**Formato recomendado:** JPG, 1920×1080 px mínimo. Usar luz natural o buena iluminación artificial. Fondo neutro si es posible.

---

## Checklist estado inicial (`estado-inicial/`)

Fotografiar **antes de desmontar o modificar cualquier cosa**. Estas fotos son el punto de referencia para todas las comparativas.

### Vista general de la máquina
- [ ] Vista frontal completa (ángulo 3/4 izquierda)
- [ ] Vista lateral derecha
- [ ] Vista trasera (electrónica y cables)
- [ ] Vista desde arriba

### Electrónica original
- [ ] Placa GT2560 v3 completa con todos los conectores
- [ ] Detalle de los drivers A4988
- [ ] Pantalla LCD y encoder
- [ ] Interior del chasis con el cableado original

### Sistema de extrusión original
- [ ] Extrusores Bowden (los dos motores en el chasis)
- [ ] Tubo PTFE completo desde extrusor hasta hotend
- [ ] Hotend mixing original (J-Head) desmontado y montado
- [ ] Zona del toolhead completa

### Calibración de referencia (benchmark inicial)
- [ ] Impresión de un Benchy con configuración de fábrica
- [ ] Cubo de calibración 20×20×20 mm
- [ ] Foto de la pantalla mostrando temperatura durante impresión
- [ ] Medición dimensional del cubo con calibre (anotar valores)
- [ ] Foto del nivel de ruido con app de decibelios durante impresión

---

## Checklist Fase 1 (`fase-1/`)

### 1a — Electrónica
- [ ] SKR Mini E3 V3 en el embalaje (antes de instalar)
- [ ] Orange Pi Zero 3 con la microSD
- [ ] Proceso de montaje de la SKR en el chasis
- [ ] Conexionado de motores (antes y después)
- [ ] Conexionado del CR-Touch al conector BLTouch
- [ ] Electrónica completa instalada (vista general)
- [ ] Fluidd funcionando en el navegador (primera vez)

### 1b — Extrusor Sharkfin
- [ ] Piezas impresas en ABS/ASA antes de montar
- [ ] Kit BMG Clone desempaquetado
- [ ] Motor NEMA 17 pancake junto al motor original (comparativa de tamaño)
- [ ] Proceso de inserción de insertos de calor
- [ ] Engranajes BMG montados en el cuerpo Sharkfin
- [ ] Extrusor Sharkfin completamente montado
- [ ] Detalle del latch y mecanismo de tensión

### 1c — Toolhead Mini Stealth v2
- [ ] Piezas del Mini Stealth v2 impresas (core, shroud, accesorios)
- [ ] Hotend CHC V6 Volcano desempaquetado
- [ ] Ventiladores 4010 y 2510 junto a los originales (comparativa)
- [ ] CR-Touch y su bracket
- [ ] Core con hotend instalado
- [ ] Shroud montado sobre el core
- [ ] Toolhead completo (Sharkfin + Mini Stealth + CR-Touch) en el carro X
- [ ] Vista del carro X desde abajo (geometría del nozzle y sonda)

### Resultados Fase 1
- [ ] Primera impresión completa con la nueva configuración
- [ ] Benchy Fase 1 junto al Benchy original (comparativa)
- [ ] Cubo de calibración 20×20×20 mm (medición con calibre)
- [ ] Captura de pantalla del mesh de nivelación en Fluidd
- [ ] Foto del nivel de ruido durante impresión (comparativa con stock)

---

## Checklist Fase 2 (`fase-2/`)

### Guías lineales MGN12H
- [ ] Guías MGN12H desembaladas (×3)
- [ ] Comparativa: barra lisa 8 mm vs guía MGN12H (tamaño y peso)
- [ ] Proceso de montaje de la guía en el eje X
- [ ] Alineación de las dos guías en el eje Y (con nivel o comparador)
- [ ] Carro X completo con toolhead montado sobre MGN12H
- [ ] Vista del eje Y con las dos guías instaladas

### Resultados Fase 2
- [ ] Benchy Fase 2 junto a los anteriores (comparativa de tres)
- [ ] Test de velocidad alta (200+ mm/s)
- [ ] Medición de juego lateral antes y después (con reloj comparador si es posible)

---

## Fotos de referencia para la Fase 3 (benchmarks)

Al completar cada fase, hacer siempre estas tres fotos en las mismas condiciones (misma iluminación, mismo ángulo, misma cámara) para que la comparativa sea válida:

| # | Foto | Propósito |
|---|------|-----------|
| A | Benchy desde el lado izquierdo | Calidad general de superficies |
| B | Benchy desde la proa | Calidad de voladizos y puentes |
| C | Cubo 20×20×20 con calibre | Precisión dimensional |
| D | Torre de stringing | Retracción y PA calibrados |
| E | Captura de Fluidd con el mesh | Estado de la nivelación |
