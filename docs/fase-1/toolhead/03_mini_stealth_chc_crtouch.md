# 🏎️ Fase 1c — Toolhead: Mini Stealth v2 + CHC V6 Volcano + CR-Touch

---

## ¿Qué es el Mini Stealth v2?

El Mini Stealth v2 es una versión reducida del Voron Stealthburner, aproximadamente 5/8 del tamaño del original y considerablemente más ligero. Su arquitectura es modular: el extrusor y el hotend se montan en una pieza central llamada **core**, y el shroud (carcasa exterior con ventiladores y LEDs) desliza sobre él. Esto permite retirar el extrusor completo sin desmontar el toolhead de la impresora.

Usa dos ventiladores sopladores **4010** para refrigeración de capa con guías de aire integradas, y un ventilador **2510** para el hotend. El repo oficial cuenta con más de 90 shrouds organizados por tipo de extrusor, con variantes básica, ZeroClick y **probe-mount** (soporte de sonda izquierdo o derecho).

**Repo oficial:** [github.com/atrushing/Mini_Stealth](https://github.com/atrushing/Mini_Stealth)

---

## 🔧 Componentes

| Componente | Especificación | Cant. | Enlace | Precio |
|------------|---------------|-------|--------|--------|
| Ventilador capa | 4010 24V radial soplador | 2 | [AliExpress](https://es.aliexpress.com/item/1005003371996395.html) | ~3 € |
| Ventilador hotend | 2510 24V axial | 1 | [AliExpress](https://es.aliexpress.com/item/1005006831848917.html) | ~5 € |
| Extensores JST | Para cables de ventilador | 1 set | [AliExpress](https://es.aliexpress.com/item/1005005491577017.html) | ~2 € |
| CHC V6 Volcano | Alto caudal, 24V, NTC 100k, boquilla 0.4 mm | 1 | [AliExpress](https://es.aliexpress.com/item/1005003849153931.html) | ~12 € |
| CR-Touch | Original Creality, señal 5V | 1 | [AliExpress](https://es.aliexpress.com/item/1005009035812836.html) | ~12 € |

### Tornillería

| Referencia | Cant. | Tipo | Uso |
|------------|-------|------|-----|
| M3×40 BHCS | 2 | Cabeza cilíndrica | Fijar toolhead al carro X |
| M2.5×8 BHCS | 2 | Cabeza cilíndrica | Montaje hotend al core |
| M2.5×6 BHCS | 2 | Cabeza cilíndrica | Fijación secundaria hotend |
| M3×8 BHCS | 2 | Cabeza cilíndrica | Fijar extrusor Sharkfin al core |
| M3×6 BHCS | 2 | Cabeza cilíndrica | Puerta de cables |
| M2.5×6 FHCS | 2 | Cabeza avellanada | Bracket CR-Touch |

---

## 🖨️ Piezas a imprimir

> Parámetros completos en [`hardware/prints/README.md`](../../../hardware/prints/README.md) — todas en **ASA, 255 °C / 95 °C, 40% gyroid, 4 perímetros**.

### Elección del core — compatibilidad con Sharkfin

El Sharkfin no figura en la lista oficial de extrusores del Mini Stealth v2. La arquitectura del Sharkfin (motor pancake + engranajes BMG laterales) es más próxima al grupo **Orbiter v1.5 / BMG** que al Sherpa Micro. Usar el core de ese grupo como punto de partida:

1. En el repo de Mini Stealth v2, navegar a la carpeta del grupo **Orbiter** o **BMG**
2. Descargar el core STL y comparar visualmente el perfil de la placa de montaje con el Sharkfin
3. Si el patrón de tornillos M3 coincide → imprimir directamente
4. Si no coincide → imprimir el adaptador de placa incluido en el repo (cada grupo tiene uno)

### Lista de STLs necesarios

| Pieza | Carpeta en repo | Variante a elegir |
|-------|----------------|-------------------|
| Core | `Orbiter_v1.5/` o `BMG/` | Estándar (sin ZeroClick) |
| Shroud | `shrouds/` | **probe-mount** — derecho o izquierdo según medición del offset |
| Motor Bridge | Misma carpeta del core | — |
| Cable Door | `common/` | — |
| Strain Relief | `common/` | — |
| Probe Bracket | `probe_mounts/CR-Touch/` | Versión específica para CR-Touch |

> **¿Soporte de sonda izquierdo o derecho?** Con el Sharkfin montado en el carro X de la A20M, el CR-Touch queda a la **izquierda** del nozzle cuando la impresora está vista de frente. Elegir la variante **left probe-mount**.

---

## 🔨 Montaje

### Paso 1 — Core: insertos y hotend

1. Insertar los insertos de calor M3 con soldador a ~200 °C. Dejar enfriar completamente antes de continuar.
2. Instalar el cartucho calefactor y el termistor NTC 100k en el bloque del CHC V6 Volcano. El cartucho debe quedar en el lado **contrario** a los LEDs del core para evitar sobrecalentarlos.
3. Insertar el hotend en el core y fijar con dos tornillos M2.5×8 BHCS.
4. Insertar el tubo PTFE corto (~10 mm) entre el hotend y la entrada del extrusor.
5. Montar el probe bracket del CR-Touch con dos tornillos M2.5×6 FHCS avellanados.

### Paso 2 — Extrusor Sharkfin

Pre-ensamblar el Sharkfin completamente (ver [`docs/fase-1/extrusor/02_sharkfin_bmg.md`](../extrusor/02_sharkfin_bmg.md)) antes de instalar en el core. Fijar con dos tornillos M3×8 BHCS: empezar por el lado del latch y luego alinear el tornillo ciego.

### Paso 3 — Gestión de cables

Reunir todos los cables del toolhead (motor, termistor, calentador, ventiladores, CR-Touch) con una brida cerca de la base del latch del extrusor. Una segunda brida los sujeta al motor bridge. Dejar **~20 mm de holgura** en los cables para permitir el movimiento del eje X sin tensión.

### Paso 4 — Shroud

1. Instalar los dos ventiladores 4010 en el shroud con sus cables orientados hacia el interior.
2. Instalar el ventilador 2510 en la ranura del hotend del core.
3. Deslizar el shroud sobre el core por las guías laterales hasta que encaje con un clic. Opcional: añadir imanes de 2×6 mm en los puntos previstos para mayor retención.

### Paso 5 — Instalar en el carro X

Fijar el toolhead al carro X con dos tornillos M3×40 BHCS. Verificar que el toolhead queda perpendicular al eje X antes de apretar definitivamente — una desviación de 1° se traduce en varios décimas de error en la primera capa.

---

## ⚙️ Medir los offsets del CR-Touch

Los offsets definen la distancia entre el pin del CR-Touch y el centro del nozzle. Medir **con el toolhead instalado en el carro X** antes de calibrar el z_offset.

### Procedimiento con calibre

```
Vista desde arriba del toolhead:

        │←── x_offset ──→│
        │                │
  [CR-Touch]         [Nozzle]
        │                │
        └────────────────┘
              y_offset
         (distancia en profundidad)
```

1. Con la impresora apagada y el toolhead en el centro del eje X, medir con calibre:
   - **x_offset**: distancia horizontal entre el eje del pin del CR-Touch y el eje del nozzle. Si el CR-Touch está a la izquierda del nozzle → valor **negativo**
   - **y_offset**: distancia en profundidad entre el pin del CR-Touch y el nozzle. Si el CR-Touch está por detrás del nozzle → valor **negativo**

2. Actualizar en `printer.cfg`:
   ```ini
   [bltouch]
   x_offset: -44    # ← tu valor medido (negativo si sonda a la izquierda)
   y_offset: -9     # ← tu valor medido (negativo si sonda por detrás)
   ```

3. Verificar que `mesh_min` y `mesh_max` en `[bed_mesh]` compensan los offsets para que la sonda no salga de la cama durante el mesh:
   ```ini
   [bed_mesh]
   mesh_min: 15, 15          # (0 + |x_offset| + margen, 0 + |y_offset| + margen)
   mesh_max: 210, 245        # (255 - margen, 255 - |y_offset| - margen)
   ```

> Los valores `-44` y `-9` son **estimados** para la posición izquierda del Mini Stealth v2. Siempre medir físicamente — varían según la variante de shroud impresa.

---

## ⚙️ Configuración Klipper

```ini
# Ventilador hotend 2510 — activo automáticamente cuando hotend > 50 °C
[heater_fan hotend_fan]
pin: PC7
heater: extruder
heater_temp: 50.0
fan_speed: 1.0

# Ventiladores de capa 4010 ×2 en paralelo — controlados por el slicer
[fan]
pin: PC6
kick_start_time: 0.5   # arranque suave para ventiladores 24V
```

Los dos 4010 se conectan en paralelo al conector FAN1 de la SKR (ver [`hardware/electronica/esquema_conexiones.md`](../../../hardware/electronica/esquema_conexiones.md)).

---

## 📊 Stock vs Mini Stealth v2 + Sharkfin

| Característica | Toolhead stock A20M | Mini Stealth v2 + Sharkfin |
|---------------|---------------------|---------------------------|
| Tipo extrusión | Bowden (~40 cm PTFE) | Directa (~3.5:1) |
| Retracción necesaria | 5–8 mm | 0.5–1.5 mm |
| Refrigeración capa | 1× 40 mm radial lateral | 2× 4010 sopladores (dual simétrico) |
| Refrigeración hotend | 1× 40 mm axial | 1× 2510 axial |
| Soporte autonivelado | No | Sí (bracket integrado) |
| LEDs de estado | No | Sí (opcional) |
| Mantenimiento | Desmontaje completo | Shroud deslizable, extrusor separable |
| Compatibilidad TPU | No | Sí |

---

## 🔗 Referencias

- [Mini Stealth v2 — GitHub (atrushing)](https://github.com/atrushing/Mini_Stealth)
- [CHC V6 Volcano — AliExpress](https://es.aliexpress.com/item/1005003849153931.html)
- [CR-Touch — AliExpress](https://es.aliexpress.com/item/1005009035812836.html)
- [Adaptador Bambu hotend → V6 (Cults3D)](https://cults3d.com/es/modelo-3d/herramientas/bambu-lab-s-hotend-adapter-to-v6-size) — si el mount no coincide directamente
