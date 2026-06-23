# 🔩 Fase 1 — Extrusor Directo Sharkfin + BMG Clone

---

## 🎯 Por qué extrusión directa

La Geeetech A20M usa sistema **Bowden** (motor separado del hotend), lo que provoca:
- Retracciones largas (5-8 mm) → stringing
- Latencia en la respuesta del flujo → peor calidad
- Problemas con filamentos flexibles (TPU)

Con extrusión directa, el motor está directamente sobre el hotend:
- Retracciones cortas (0.5-2 mm)
- Mayor control del flujo
- Compatible con flexibles

---

## 🔧 Componentes del extrusor

### Extrusor: Sharkfin (KayosMaker)

El Sharkfin es un extrusor diseñado específicamente para impresoras Voron y compatibles. Usa engranajes BMG con una relación de reducción de ~3.5:1.

- **STL:** [https://github.com/KayosMaker/Sharkfin_Extruder](https://github.com/KayosMaker/Sharkfin_Extruder)
- **Motor:** NEMA 17 pancake (20 mm de profundidad)
- **Engranajes:** BMG Clone (Bondtech-like)

### Lista de piezas

| Pieza | Cantidad | Referencia |
|-------|----------|------------|
| Cuerpo Sharkfin (impreso) | 1 | ABS/ASA, 40% relleno |
| Latch Sharkfin (impreso) | 1 | ABS/ASA, 40% relleno |
| Motor NEMA 17 pancake 20mm | 1 | [AliExpress](https://es.aliexpress.com/item/1005005933469472.html) |
| Kit BMG Clone | 1 | [AliExpress](https://es.aliexpress.com/item/1005003423850142.html) |
| Insertos M3 calor | 5 | [AliExpress](https://es.aliexpress.com/item/1005008285787978.html) |
| Arandela M5 × 0.5mm | 1 | — |
| M3×25 SHCS | 1 | — |
| M3×16 BHCS | 2 | — |
| M3×10 BHCS | 2 | — |
| M3×8 BHCS | 3 | — |

---

## 🖨️ Impresión de las piezas

### Parámetros recomendados

| Parámetro | Valor |
|-----------|-------|
| Material | ABS o ASA |
| Temperatura boquilla | 250°C (ABS) / 255°C (ASA) |
| Temperatura cama | 100°C (ABS) / 90°C (ASA) |
| Relleno | 40% cúbico |
| Perímetros | 4 |
| Capas sólidas sup/inf | 5 |
| Velocidad | 50 mm/s |
| Refrigeración | 0% (ABS) / 30% (ASA) |
| Soporte | No requerido |

> ⚠️ **El ABS/ASA es necesario** por la proximidad al hotend. PLA se deformaría.

---

## 🔨 Montaje

### Paso 1: Insertar insertos de calor

Con un soldador a ~200°C, insertar los 5 insertos M3 en los agujeros correspondientes del cuerpo Sharkfin. Dejar enfriar completamente.

### Paso 2: Montar engranajes BMG

Seguir las instrucciones del kit BMG:
1. Instalar el engranaje conductor en el eje del motor
2. Instalar el engranaje conducido en su eje con rodamientos

### Paso 3: Instalar motor NEMA 17

Fijar el motor pancake al cuerpo del Sharkfin con tornillos M3×8.

### Paso 4: Instalar arandela M5

La arandela M5 de 0.5mm sirve como espaciador para el eje del filamento. Imprescindible para alineación correcta.

### Paso 5: Ajustar tensión

El Sharkfin tiene un mecanismo de tensión ajustable. Ajustar hasta que el engranaje agarre el filamento firmemente sin doblarlo.

---

## ⚙️ Calibración del extrusor (E-steps / rotation_distance)

### Procedimiento

1. Calentar el hotend a 200°C
2. Medir 100 mm de filamento desde la entrada del extrusor y marcar
3. Ejecutar en Klipper:
   ```
   G91
   G1 E100 F300
   ```
4. Medir cuánto filamento se ha movido realmente
5. Calcular nuevo `rotation_distance`:
   ```
   nuevo_rd = viejo_rd × distancia_real / 100
   ```
6. Repetir hasta obtener <1% de error

### Valores de referencia para Sharkfin + BMG

- `rotation_distance` inicial: **22.67**
- Relación de reducción: **3.5:1**
- Motor 200 pasos, 16 micropasos → 3200 pasos/vuelta

---

## 📊 Comparativa esperada (Bowden vs Direct Drive)

| Parámetro | Bowden original | Direct Drive (Sharkfin) |
|-----------|----------------|------------------------|
| Retracción | 5-8 mm | 0.5-1.5 mm |
| Stringing | Alto | Bajo |
| Calidad puentes | Media | Alta |
| Flexibles | No compatible | Compatible |
| Velocidad max. | ~80 mm/s | ~150 mm/s |
| Inercia | Baja | Media (más peso toolhead) |
