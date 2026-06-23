# 🖨️ Fase 1 — Toolhead: Mini Stealth + CHC V6 Volcano + CR-Touch

---

## 🎯 ¿Qué es el Mini Stealth?

<cite index="2-1">El Mini Stealth v2 es una versión reducida del Voron Stealthburner, aproximadamente 5/8 del tamaño del original y considerablemente más ligero. Monta el extrusor y el hotend en una pieza central (core), y los ventiladores, ventilador de hotend y LEDs en un shroud que desliza sobre el core. Esto facilita mucho el montaje y mantenimiento: el extrusor se puede retirar completamente mientras el core queda instalado en la impresora.</cite>

<cite index="1-1">Usa un par de ventiladores sopladores 4010 para refrigeración de capa y un ventilador 3010/2510 para el hotend. Los sopladores incluyen guías de aire pegadas que aumentan el caudal de aire aproximadamente un 20% respecto al Mini Stealth v1.</cite>

### ¿Por qué el Mini Stealth para este proyecto?

- Diseño inspirado en Voron, coherente con la filosofía del proyecto UGR-A20M
- Shroud separado del core → mantenimiento sin desmontar todo
- <cite index="1-1">Hay 90 shrouds diferentes agrupados por tipo de extrusor, cada uno en cuatro variantes: básico, ZeroClick, y versiones con soporte de sonda izquierda/derecha</cite>
- Compatible con CR-Touch mediante brackets de montaje de sonda (versiones probe-mount)
- LEDs de estado incorporados

---

## 🔧 Componentes del toolhead

### Ventiladores

| Componente | Especificación | Cantidad | Enlace | Precio |
|------------|---------------|----------|--------|--------|
| Ventilador soplador capa | 4010 24V radial | 2 | [AliExpress](https://es.aliexpress.com/item/1005003371996395.html) | ~3 € |
| Ventilador hotend | 2510 24V axial | 1 | [AliExpress](https://es.aliexpress.com/item/1005006831848917.html) | ~5 € |
| Extensores de cable JST | Para ventiladores | 1 set | [AliExpress](https://es.aliexpress.com/item/1005005491577017.html) | ~2 € |

### Hotend

| Componente | Especificación | Enlace | Precio |
|------------|---------------|--------|--------|
| CHC V6 Volcano | Alto caudal, 24V, NTC 100k | [AliExpress](https://es.aliexpress.com/item/1005003849153931.html) | ~12 € |

> El CHC V6 Volcano es compatible con el Mount estándar tipo E3D V6, que el Mini Stealth soporta en varias de sus configuraciones de core.

### Autonivelado

| Componente | Especificación | Enlace | Precio |
|------------|---------------|--------|--------|
| CR-Touch | Original Creality, 5V señal | [AliExpress](https://es.aliexpress.com/item/1005009035812836.html) | ~12 € |

> El Mini Stealth incluye variantes de shroud con soporte lateral para sonda (probe-mount left/right). <cite index="1-1">Estas versiones usan tornillos M2.5×6 de cabeza plana para fijar brackets que sujetan seis tipos diferentes de sonda.</cite>

### Tornillería toolhead

| Referencia | Cantidad | Tipo | Uso |
|------------|----------|------|-----|
| M3×40 BHCS | 2 | Allen cabeza cilíndrica | Fijar toolhead al carro X |
| M2.5×8 BHCS | 2 | Allen cabeza cilíndrica | Montaje hotend al core |
| M2.5×6 BHCS | 2 | Allen cabeza cilíndrica | Montaje hotend |
| M3×8 BHCS | 2 | Allen cabeza cilíndrica | Fijar extrusor Sharkfin al core |
| M3×6 BHCS | 2 | Allen cabeza cilíndrica | Puerta de cables |
| M2.5×6 FHCS | 2 | Tornillo avellanado | Bracket sonda CR-Touch |

---

## 🖨️ Piezas a imprimir

El Mini Stealth v2 tiene una arquitectura modular core + shroud. Hay que elegir las piezas correctas según el extrusor (Sharkfin/BMG) y el hotend (CHC V6 Volcano).

### Piezas necesarias

| Pieza STL | Carpeta en repo | Notas |
|-----------|----------------|-------|
| Core (pieza central) | `Sharkfin/` o extrusor compatible | Elegir el core para el grupo de extrusor correcto |
| Shroud (carcasa exterior) | Versión probe-mount (CR-Touch) | Elegir versión con soporte de sonda |
| Motor bridge | Misma carpeta de extrusor | Gestión de cables del motor |
| Cable door | Común a todos | Cierre posterior |
| Strain relief | Común a todos | Alivio de tensión de cables |
| Probe bracket (CR-Touch) | Carpeta probe mounts | Soporte para CR-Touch |

> **⚠️ Nota:** El Sharkfin no es uno de los 13 extrusores listados oficialmente en el Mini Stealth. Verificar en el repo si hay un core/adapter compatible, o usar el core del Sherpa Micro (perfil similar) con el adaptador de placa correspondiente. Alternativamente, el adaptador Bambulab → V6 puede facilitar el montaje del hotend.

### Parámetros de impresión

| Parámetro | Valor |
|-----------|-------|
| Material | ABS o ASA |
| Temperatura boquilla | 250°C (ABS) / 255°C (ASA) |
| Temperatura cama | 100°C (ABS) / 90°C (ASA) |
| Relleno | 40% cúbico o gyroid |
| Perímetros | 4 |
| Capas sólidas sup/inf | 5 |
| Soporte | No requerido (diseñado sin soportes) |
| Refrigeración | 0% (ABS) / 30% máx (ASA) |

---

## 🔨 Montaje — Proceso

### Paso 1: Preparar el core

1. Insertar insertos de calor M3 en el core (si los tiene, depende del modelo de core)
2. Instalar el hotend CHC V6 Volcano con tornillos M2.5×6:
   - <cite index="3-1">Instalar el cartucho calefactor alejado de los LEDs para evitar sobrecalentarlos. No olvidar el tubo PTFE.</cite>
3. Montar el bracket del CR-Touch con tornillos M2.5×6 FHCS

### Paso 2: Montar el extrusor (Sharkfin)

<cite index="3-1">Pre-ensamblar el extrusor antes de instalarlo en el shroud. Usar dos tornillos M3×8 BHCS para instalar el extrusor. Ayuda tener ambos tornillos en el extrusor antes de colocarlo. Empezar por el tornillo del lado del latch y luego alinear el tornillo ciego.</cite>

### Paso 3: Gestión de cables

<cite index="3-1">Reunir los cables con un brida junto a la base del latch del extrusor y luego usar otra brida para asegurar los cables al motor bridge. Dejar un poco de holgura en los cables del extrusor.</cite>

### Paso 4: Ensamblar el shroud

1. Instalar los ventiladores 4010 en el shroud
2. Deslizar el shroud sobre el core por las ranuras guía
3. <cite index="1-1">El shroud encaja en el core mediante un par de ranuras deslizantes y puede llevar imanes para mejorar la conexión según sea necesario.</cite>

### Paso 5: Instalar en el carro X

<cite index="5-1">Usar dos tornillos M3×40 BHCS para fijar el toolhead al carro X.</cite>

---

## ⚙️ Configuración Klipper para el toolhead

### Offsets del CR-Touch

Los offsets dependen de la posición exacta del bracket de sonda en el shroud. Medir físicamente con calibre:

```ini
[bltouch]
x_offset: -44    # ← Medir: distancia horizontal CR-Touch → nozzle
y_offset: -9     # ← Medir: distancia frontal CR-Touch → nozzle
```

> Valores negativos = la sonda está a la izquierda y detrás del nozzle (posición típica con bracket derecho).

### Configuración de ventiladores

```ini
# Ventilador hotend (2510) — siempre activo cuando hotend > 50°C
[heater_fan hotend_fan]
pin: PC7
heater: extruder
heater_temp: 50.0

# Ventiladores de capa (4010 ×2) — controlados por gcode
[fan]
pin: PC6
```

Si los dos ventiladores de capa van en el mismo pin (en paralelo, que es lo habitual), el `[fan]` anterior los controla a ambos. Si van en pines separados, se necesita un `[fan_generic]` adicional.

---

## 📊 Comparativa de toolheads

| Característica | Toolhead stock A20M | Mini Stealth + Sharkfin |
|---------------|---------------------|------------------------|
| Tipo extrusión | Bowden | Directa |
| Refrigeración capa | 1× 40mm radial | 2× 4010 sopladores |
| Distribución enfriamiento | Lateral | Dual, simétrica |
| LEDs de estado | No | Sí (opcional) |
| Soporte sonda auto-nivel | No | Sí (bracket integrado) |
| Peso aproximado | ~150 g | ~200-250 g |
| Mantenimiento | Difícil (todo integrado) | Fácil (shroud desmontable) |

---

## 🔗 Referencias

- [Mini Stealth v2 — GitHub (atrushing)](https://github.com/atrushing/Mini_Stealth)
- [Mini Stealth — TeamFDM (documentación v1)](https://www.teamfdm.com/files/file/657-mini-stealth-mini-sherpa/)
- [CHC V6 Volcano — AliExpress](https://es.aliexpress.com/item/1005003849153931.html)
- [Adaptador Bambu hotend → V6 (Cults3D)](https://cults3d.com/es/modelo-3d/herramientas/bambu-lab-s-hotend-adapter-to-v6-size)
