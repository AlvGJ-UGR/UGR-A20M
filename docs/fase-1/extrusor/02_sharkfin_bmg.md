# 🔩 Fase 1b — Extrusor directo Sharkfin + BMG Clone

---

## 🎯 Por qué extrusión directa

La Geeetech A20M usa sistema **Bowden**: el motor del extrusor está separado del hotend por un tubo PTFE de ~40 cm. Esto provoca problemas que la extrusión directa resuelve:

| Problema Bowden | Causa | Solución con direct drive |
|----------------|-------|--------------------------|
| Stringing excesivo | Retracción larga necesaria (5–8 mm) | Retracción corta (0.5–1.5 mm) |
| Blob en reanudación | Inercia del filamento en el tubo | Respuesta inmediata del extrusor |
| Incompatibilidad con flexibles | TPU se dobla en el tubo | Motor directamente sobre el hotend |
| Calidad de puentes baja | Flujo difícil de controlar | Control preciso con direct drive |

---

## 🔧 Componentes

### Extrusor Sharkfin (KayosMaker)

Diseño open-source pensado para impresoras Voron. Usa engranajes BMG con relación de reducción ~3.5:1, lo que da gran fuerza de agarre con un motor pancake ligero.

- **STL:** [github.com/KayosMaker/Sharkfin_Extruder](https://github.com/KayosMaker/Sharkfin_Extruder)
- **Motor:** NEMA 17 pancake (20 mm de profundidad) — más ligero que un NEMA 17 estándar
- **Engranajes:** BMG Clone (Bondtech-like)

### Lista de materiales

| Pieza | Cant. | Enlace | Precio |
|-------|-------|--------|--------|
| Cuerpo Sharkfin (impreso en ABS/ASA) | 1 | [GitHub](https://github.com/KayosMaker/Sharkfin_Extruder) | Gratis |
| Latch Sharkfin (impreso en ABS/ASA) | 1 | [GitHub](https://github.com/KayosMaker/Sharkfin_Extruder) | Gratis |
| Motor NEMA 17 pancake 20 mm | 1 | [AliExpress](https://es.aliexpress.com/item/1005005933469472.html) | ~5 € |
| Kit BMG Clone | 1 | [AliExpress](https://es.aliexpress.com/item/1005003423850142.html) | ~5 € |
| Insertos termofijados M3 ×5 | 5 | [AliExpress](https://es.aliexpress.com/item/1005008285787978.html) | ~1 € |
| Arandela M5 × 0.5 mm | 1 | — | <1 € |
| M3×25 SHCS | 1 | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) | — |
| M3×16 BHCS | 2 | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) | — |
| M3×10 BHCS | 2 | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) | — |
| M3×8 BHCS | 3 | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) | — |

---

## 🖨️ Impresión de las piezas

Las piezas deben imprimirse en **ASA** (primera opción) o **ABS** — la proximidad al hotend durante la operación hace que el PLA se deforme por encima de 55 °C.

Parámetros recomendados: **ASA 255 °C / cama 95 °C / 40% gyroid / 4 perímetros / sin refrigeración**. Ver parámetros completos en [`hardware/prints/README.md`](../../../hardware/prints/README.md) y perfiles de slicer en [`docs/slicer_settings.md`](../../slicer_settings.md).

> Imprimir en recinto cerrado. Sin recinto el warping en las piezas largas (body del Sharkfin) es casi inevitable con ABS.

---

## 🔨 Montaje paso a paso

### Paso 1 — Insertar insertos de calor

Calentar el soldador a 200–210 °C. Colocar cada inserto M3 en su agujero correspondiente y presionar suavemente con el soldador hasta que quede a ras. **Dejar enfriar completamente antes de continuar.**

Hay 5 insertos en el cuerpo Sharkfin: 2 para fijar el motor, 2 para fijar al toolhead y 1 para el latch.

### Paso 2 — Montar los engranajes BMG

El kit BMG incluye dos engranajes, dos ejes, rodamientos y una tuerca de tensión.

1. **Antes de montar**, verificar que el eje del motor NEMA 17 pancake tiene un **flat** (cara plana mecanizada). Algunos motores baratos de AliExpress no lo traen de fábrica — sin flat, el tornillo de fijación del engranaje no agarra y el engranaje patina sobre el eje. Si falta el flat, devolver el motor o limarlo manualmente con cuidado
2. Instalar el engranaje **conductor** (el pequeño, con ranura para el filamento) en el eje del motor, alineando el tornillo prisionero con el flat — usar la llave Allen incluida para fijarlo con firmeza
3. Instalar el engranaje **conducido** en su eje con los rodamientos a presión
4. Verificar que ambos engranajes engranan correctamente antes de continuar

### Paso 3 — Instalar el motor NEMA 17

Fijar el motor pancake al cuerpo del Sharkfin con 2× M3×8 BHCS. El motor debe quedar perfectamente alineado con el cuerpo para que los engranajes encajen sin holgura ni rozamiento excesivo.

### Paso 4 — Instalar la arandela M5

La arandela M5 de 0.5 mm actúa como espaciador en el eje del filamento, garantizando la alineación correcta entre los dos engranajes. **No omitir este paso** — sin la arandela, el filamento no entra recto y el extrusor falla.

### Paso 5 — Ensamblar el latch y ajustar tensión

1. Montar el latch con el tornillo M3×25 SHCS
2. Ajustar la tensión del latch: el engranaje debe agarrar el filamento firmemente al presionarlo manualmente, pero sin aplastarlo
3. Comprobar que el filamento entra y sale del extrusor con un tirón suave y uniforme

---

## ⚙️ Calibración del extrusor en Klipper

La `rotation_distance` determina cuánto filamento mueve el extrusor por cada vuelta del motor. Un valor incorrecto causa sub o sobre-extrusión.

> Este proceso también está documentado en [`docs/guia_calibracion.md`](../../guia_calibracion.md) — Paso 2.

### Procedimiento

> Usar **PLA** para esta calibración — es el material más predecible y fácil de marcar con rotulador. Una vez calibrado el `rotation_distance`, es válido para todos los materiales (no depende del tipo de filamento, solo de la geometría del extrusor).

1. Calentar el hotend a 200 °C desde Fluidd
2. Cargar filamento hasta que salga un hilo continuo por la boquilla
3. Cortar el filamento a ras de la entrada del extrusor con un cúter
4. Con un rotulador, **marcar el filamento a exactamente 100 mm** de la entrada
5. En la consola de Klipper:
   ```
   G91
   G1 E100 F150
   G92 E0
   G90
   ```
   > Usar F150 (velocidad lenta) para evitar que el extrusor patine durante la medición.
6. Medir la distancia desde la entrada del extrusor hasta la marca — si el extrusor es preciso, debería haber desaparecido dentro de él
7. Medir el **filamento sobrante** desde la marca hasta la entrada:
   - Si quedan 5 mm fuera → se extrujo 95 mm en vez de 100 → sub-extrusión
   - Si la marca está 5 mm dentro → se extrujo 105 mm → sobre-extrusión
8. Calcular el nuevo valor:
   ```
   rotation_distance_nuevo = rotation_distance_actual × distancia_real / 100
   ```
9. Actualizar en `printer.cfg` y repetir hasta error < 1 %

### Valores de referencia

| Parámetro | Valor |
|-----------|-------|
| `rotation_distance` inicial | 22.67 |
| `gear_ratio` | 50:17 |
| Micropasos | 16 |
| Relación de reducción efectiva | ~3.5:1 |

### Ejemplo de cálculo

```
# Situación: pedimos 100 mm, pero solo se mueven 95 mm reales
rotation_distance_nuevo = 22.67 × 95 / 100 = 21.54

# Actualizar en printer.cfg:
rotation_distance: 21.54
```

---

## 🛠️ Solución de problemas

| Síntoma | Causa probable | Solución |
|---------|---------------|----------|
| Filamento no entra al extrusor | Arandela M5 omitida o mal alineada | Verificar posición de la arandela; realinear |
| Extrusor patina (click-click) | Tensión del latch insuficiente | Aumentar tensión del tornillo del latch |
| Extrusor patina al alta velocidad | `run_current` bajo en TMC2209 | Subir `run_current` en `[tmc2209 extruder]` de 0.65 a 0.70–0.75 |
| Sobre-extrusión constante | `rotation_distance` demasiado bajo | Repetir la prueba de 100 mm del procedimiento de calibración; si el error es > 1%, recalcular y actualizar |
| Sub-extrusión constante | `rotation_distance` demasiado alto | Misma prueba de 100 mm; verificar también que la boquilla no esté parcialmente obstruida (hacer cold pull) antes de tocar `rotation_distance` |
| Motor extrusor muy caliente (> 60 °C) | `run_current` demasiado alto | Reducir `run_current` a 0.60 |
| Engranajes ruidan | Engranaje conductor mal fijado al eje del motor, sucio o mal alineado | Verificar que el tornillo de fijación del engranaje conductor está apretado contra el plano del eje (flat); limpiar con aire comprimido; verificar alineación motor-cuerpo |

---

## 📊 Bowden original vs Sharkfin direct drive

| Parámetro | Bowden A20M | Sharkfin direct drive |
|-----------|-------------|----------------------|
| Retracción | 5–8 mm | 0.5–1.5 mm |
| Stringing | Alto | Bajo |
| Calidad de puentes | Media | Alta |
| Compatibilidad TPU/flexibles | ✗ | ✓ |
| Velocidad máx. práctica | ~80 mm/s | ~150 mm/s |
| Inercia del toolhead | Baja | Media (motor en cabezal) |
| Complejidad de calibración | Media | Baja (PA más sencillo) |

---

## 🔗 Referencias

- [Sharkfin Extruder — KayosMaker GitHub](https://github.com/KayosMaker/Sharkfin_Extruder)
- [Klipper — Calibración de rotation_distance](https://www.klipper3d.org/Rotation_Distance.html)
- [Klipper — Pressure Advance](https://www.klipper3d.org/Pressure_Advance.html)
- [Comunidad Voron — extrusores recomendados](https://vorondesign.com/)
