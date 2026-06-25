# 🖨️ Fase 1c — Toolhead: Mini Stealth v2 + CHC V6 Volcano + CR-Touch

---

## ¿Qué es el Mini Stealth v2?

El Mini Stealth v2 es una versión reducida del Voron Stealthburner, aproximadamente 5/8 del tamaño del original y considerablemente más ligero. Su arquitectura es modular: el extrusor y el hotend se montan en una pieza central llamada **core**, y el shroud (carcasa exterior con ventiladores y LEDs) desliza sobre él. Esto permite retirar el extrusor completo sin desmontar el toolhead de la impresora.

Usa dos ventiladores sopladores **4010** para refrigeración de capa con guías de aire integradas, y un ventilador **2510** para el hotend. El repo oficial cuenta con más de 90 shrouds diferentes, organizados por tipo de extrusor y con variantes básica, ZeroClick y **probe-mount** (con soporte de sonda izquierdo o derecho) — esta última es la que necesitamos para el CR-Touch.

### Ventajas para este proyecto

- Diseño coherente con la filosofía Voron del proyecto UGR-A20M
- Shroud desmontable → mantenimiento rápido sin desmontar el toolhead
- Refrigeración de capa dual y simétrica (mejora respecto al stock)
- Bracket de sonda integrado en el shroud → no requiere adaptadores externos
- LEDs de estado opcionales

---

## 🔧 Lista de componentes

### Ventiladores

| Componente | Especificación | Cant. | Enlace | Precio |
|------------|---------------|-------|--------|--------|
| Ventilador capa | 4010 24V radial soplador | 2 | [AliExpress](https://es.aliexpress.com/item/1005003371996395.html) | ~3 € |
| Ventilador hotend | 2510 24V axial | 1 | [AliExpress](https://es.aliexpress.com/item/1005006831848917.html) | ~5 € |
| Extensores JST | Para cables de ventilador | 1 set | [AliExpress](https://es.aliexpress.com/item/1005005491577017.html) | ~2 € |

### Hotend

| Componente | Especificación | Enlace | Precio |
|------------|---------------|--------|--------|
| CHC V6 Volcano | Alto caudal, 24V, NTC 100k, boquilla 0.4 mm | [AliExpress](https://es.aliexpress.com/item/1005003849153931.html) | ~12 € |

El CHC V6 Volcano usa el mismo patrón de montaje que el E3D V6, compatible con la mayoría de cores del Mini Stealth. Si fuera necesario, existe un [adaptador Bambu → V6](https://cults3d.com/es/modelo-3d/herramientas/bambu-lab-s-hotend-adapter-to-v6-size) imprimible.

### Autonivelado

| Componente | Especificación | Enlace | Precio |
|------------|---------------|--------|--------|
| CR-Touch | Original Creality, señal 5V | [AliExpress](https://es.aliexpress.com/item/1005009035812836.html) | ~12 € |

### Tornillería

| Referencia | Cant. | Tipo | Uso |
|------------|-------|------|-----|
| M3×40 BHCS | 2 | Cabeza cilíndrica | Fijar toolhead al carro X |
| M2.5×8 BHCS | 2 | Cabeza cilíndrica | Montaje hotend al core |
| M2.5×6 BHCS | 2 | Cabeza cilíndrica | Montaje hotend |
| M3×8 BHCS | 2 | Cabeza cilíndrica | Fijar extrusor Sharkfin al core |
| M3×6 BHCS | 2 | Cabeza cilíndrica | Puerta de cables |
| M2.5×6 FHCS | 2 | Cabeza avellanada | Bracket CR-Touch |

---

## 🖨️ Piezas a imprimir

> Ver parámetros de impresión detallados en [`hardware/prints/README.md`](../../../hardware/prints/README.md)

| Pieza | Carpeta en repo | Notas |
|-------|----------------|-------|
| Core | Grupo de extrusor compatible | Verificar compatibilidad con Sharkfin; intentar con el grupo BMG/Sherpa Micro |
| Shroud — versión probe-mount | `shrouds/` | Elegir variante con soporte de sonda (izquierda o derecha según medición) |
| Motor Bridge | Misma carpeta del core | Gestión de cables del motor |
| Cable Door | Común | Cierre posterior |
| Strain Relief | Común | Alivio de tensión de cables |
| Probe Bracket (CR-Touch) | `probe_mounts/` | Soporte específico para CR-Touch |

> ⚠️ **Nota de compatibilidad:** El Sharkfin no figura en la lista oficial de extrusores del Mini Stealth v2. Antes de imprimir el core, verificar en el repo qué grupo de extrusor tiene un perfil más cercano al Sharkfin (probablemente el grupo BMG o Sherpa Micro). Si fuera necesario, un adaptador de placa puede resolver la diferencia de mounting pattern.

---

## 🔨 Proceso de montaje

### Paso 1 — Preparar el core

1. Insertar insertos de calor M3 en el core con un soldador a ~200 °C. Dejar enfriar.
2. Instalar el hotend CHC V6 Volcano con tornillos M2.5×6 BHCS. Colocar el cartucho calefactor en el lado contrario a los LEDs para evitar sobrecalentarlos.
3. No olvidar el tubo PTFE entre el hotend y la entrada del extrusor.
4. Montar el bracket del CR-Touch con tornillos M2.5×6 FHCS.

### Paso 2 — Montar el extrusor Sharkfin

Pre-ensamblar el extrusor completamente antes de instalarlo en el core. Usar dos tornillos M3×8 BHCS. Conviene poner ambos tornillos en el extrusor antes de acercarlo al core: empezar por el lado del latch y luego alinear el tornillo ciego del lado contrario.

### Paso 3 — Gestión de cables

Reunir todos los cables del toolhead con una brida junto a la base del latch del extrusor. Usar una segunda brida para sujetar el conjunto al motor bridge. Dejar un poco de holgura en los cables del motor para permitir el movimiento del eje X.

### Paso 4 — Ensamblar el shroud

1. Instalar los dos ventiladores 4010 en el shroud y conectar sus cables.
2. Instalar el ventilador 2510 en el hotend.
3. Deslizar el shroud sobre el core por las ranuras guía hasta que encaje. Se pueden añadir imanes (2×6 mm) en los puntos previstos para mejorar la retención.

### Paso 5 — Instalar en el carro X

Fijar el toolhead completo al carro X con dos tornillos M3×40 BHCS. Comprobar que el toolhead queda nivelado y firme antes de continuar.

---

## ⚙️ Configuración Klipper

### Offsets del CR-Touch

Medir físicamente con calibre la distancia del pin del CR-Touch al centro del nozzle:

```ini
[bltouch]
x_offset: -44    # Negativo = sonda a la izquierda del nozzle
y_offset: -9     # Negativo = sonda por detrás del nozzle
```

Actualizar estos valores en `printer.cfg` antes de ejecutar `PROBE_CALIBRATE`.

### Ventiladores

```ini
# Ventilador hotend 2510 — activo automáticamente cuando hotend > 50 °C
[heater_fan hotend_fan]
pin: PC7
heater: extruder
heater_temp: 50.0

# Ventiladores de capa 4010 ×2 — controlados por el slicer
[fan]
pin: PC6
```

Los dos ventiladores de capa se conectan en paralelo al mismo pin (FAN1 en la SKR Mini E3 V3), por lo que una sola sección `[fan]` los controla ambos.

---

## 📊 Stock vs Mini Stealth v2

| Característica | Toolhead stock A20M | Mini Stealth v2 + Sharkfin |
|---------------|---------------------|-----------------------------|
| Tipo extrusión | Bowden | Directa (~3.5:1) |
| Refrigeración capa | 1× 40 mm radial | 2× 4010 sopladores (dual simétrico) |
| Refrigeración hotend | 1× 40 mm axial | 1× 2510 axial |
| Soporte autonivelado | No | Sí (bracket integrado en shroud) |
| LEDs de estado | No | Sí (opcional) |
| Mantenimiento | Desmontaje completo | Shroud deslizable, extrusor separable |
| Compatibilidad flexibles | No (Bowden) | Sí (extrusión directa) |

---

## 🔗 Referencias

- [Mini Stealth v2 — GitHub (atrushing)](https://github.com/atrushing/Mini_Stealth)
- [CHC V6 Volcano — AliExpress](https://es.aliexpress.com/item/1005003849153931.html)
- [CR-Touch — AliExpress](https://es.aliexpress.com/item/1005009035812836.html)
- [Adaptador Bambu hotend → V6 (Cults3D)](https://cults3d.com/es/modelo-3d/herramientas/bambu-lab-s-hotend-adapter-to-v6-size)
