# 🔧 Guía de mantenimiento — UGR-A20M

Calendario de mantenimiento preventivo para mantener la impresora en óptimas condiciones.

---

## Antes de cada impresión

- [ ] Verificar que la cama está limpia (IPA al 90% si hay restos de filamento o grasa)
- [ ] Comprobar visualmente que la boquilla no tiene residuos carbonizados
- [ ] Verificar que el filamento no está enredado en la bobina
- [ ] Confirmar que el CR-Touch despliega y recoge correctamente (primer homing)

---

## Cada 20–30 horas de impresión

### Mecánica
- [ ] **Lubricar las varillas Z** — aplicar una fina capa de grasa de litio blanca en los husillos T8. Mover el eje Z arriba y abajo varias veces para distribuir
- [ ] **Verificar la tensión de las correas X e Y** — la correa debe sonar como una cuerda de guitarra al pulsarla (~50 Hz). Si está floja, tensarla
- [ ] **Limpiar los rodamientos lineales** — pasar un trapo limpio por las barras lisas (o por las guías MGN12H en Fase 2) para retirar el polvo de filamento

### Electrónica
- [ ] **Verificar que todos los conectores están firmes** — especialmente el del hotend y el termistor, que están sometidos a vibración
- [ ] **Revisar el cable del toolhead** — buscar signos de desgaste por roce con el chasis

---

## Cada 50–100 horas de impresión

### Boquilla
- [ ] **Inspeccionar la boquilla** — buscar signos de desgaste o residuos carbonizados en la punta
- [ ] **Hacer un cold pull** para limpiar el interior del hotend:

  **Procedimiento de cold pull:**
  1. Calentar el hotend a **200 °C** (PLA) o **230 °C** (PETG/ABS)
  2. Purgar manualmente ~20 mm de filamento desde Fluidd
  3. Bajar la temperatura a **90 °C** (PLA) o **110 °C** (PETG/ABS) **sin mover el filamento**
  4. Cuando alcance la temperatura, tirar del filamento hacia arriba con un movimiento **firme, continuo y recto** — sin girar
  5. El filamento saldrá con la forma exacta del interior del hotend, arrastrando los residuos
  6. Si la punta sale limpia y con forma cónica → hotend limpio
  7. Si sale con restos oscuros o irregularidades → repetir desde el paso 1 con filamento de PLA blanco o transparente (se ven mejor los residuos)
  8. Repetir hasta que salga limpio

### Calibración
- [ ] **Ejecutar `SCREWS_TILT_CALCULATE`** — la cama puede haberse movido por las vibraciones
- [ ] **Regenerar el mesh** (`GENERATE_MESH`) si la cama se ha manipulado o cambiado de temperatura

### Limpieza general
- [ ] **Limpiar el interior del chasis** — retirar el polvo de filamento acumulado con aire comprimido o aspirador
- [ ] **Revisar el ventilador del hotend (2510)** — limpiar las aspas de polvo. Un ventilador bloqueado puede causar atascos de calor (heat creep)

---

## Cada 200–300 horas de impresión

### Boquilla
- [ ] **Sustituir la boquilla de latón** si se han impreso más de 100 h con materiales abrasivos o si se aprecian cambios en el diámetro de la extrusión
- Procedimiento de cambio de boquilla:
  1. Ejecutar `NOZZLE_CHANGE` para calentar y aparcar el cabezal
  2. Con llave de 7 mm, aflojar la boquilla caliente (280 °C para CHC V6 Volcano)
  3. Instalar la nueva boquilla y apretar **en caliente** (nunca en frío — el bloque se dilata)
  4. Recalibrar el z_offset tras el cambio (`CALIBRATE_Z_OFFSET`)

### Lubricación profunda
- [ ] **Lubricar los rodamientos del extrusor (BMG)** — una gota de aceite de máquina de coser en el eje del engranaje conducido
- [ ] **Lubricar los ejes de los ventiladores** si hay ruido — una gota de aceite en el eje

### Tornillería
- [ ] **Repasar todos los tornillos del toolhead** — el Sharkfin y el Mini Stealth están sometidos a vibración constante; usar Loctite azul (desmontable) en tornillos que se aflojen repetidamente

---

## Cada 500+ horas o cuando sea necesario

### Tubo PTFE
- [ ] **Inspeccionar el tubo PTFE** entre el extrusor y el hotend — buscar decoloración amarillenta, deformaciones o grietas. A 260 °C+ el PTFE puede degradarse y emitir vapores. Sustituir si hay dudas
- Tubo de repuesto: PTFE de calidad alimentaria, diámetro interno 2 mm, externo 4 mm

### Rodamientos
- [ ] **Verificar los rodamientos del carro X e Y** — si hay juego o ruido inusual, sustituir
- En la Fase 2 con guías MGN12H: lubricar con grasa de litio cada 200–300 h

### Termistor y calentador
- [ ] **Verificar la integridad de los cables del termistor** — son muy frágiles y el calor los endurece con el tiempo. Si hay lecturas erráticas, sustituir
- [ ] **Revisar el cartucho calefactor** — buscar signos de quemado en la conexión. Sustituir si la resistencia medida se desvía > 10% del valor nominal

---

## Calibración periódica recomendada

| Acción | Frecuencia | Macro |
|--------|-----------|-------|
| Recalibrar z_offset | Tras cada cambio de boquilla o cristal | `CALIBRATE_Z_OFFSET` |
| Regenerar mesh | Tras manipular la cama o cambio de temperatura | `GENERATE_MESH` |
| Recalibrar rotation_distance | Si hay cambios en la extrusión | Manual (ver guía calibración Paso 2) |
| Recalibrar PID hotend | Tras cambiar el calentador o termistor | `CALIBRATE_PID_HOTEND` |
| Recalibrar Pressure Advance | Al cambiar de marca de filamento | `PRESSURE_ADVANCE_TOWER` |
| Calibrar Input Shaping | Tras modificaciones estructurales | `CALIBRATE_INPUT_SHAPING` |

---

## Consumibles y repuestos recomendados tener en stock

| Consumible | Cantidad | Precio aprox. | Enlace |
|------------|----------|--------------|--------|
| Boquilla latón 0.4 mm CHC V6 | ×5 | ~3 € el pack | [AliExpress](https://es.aliexpress.com/w/wholesale-v6-nozzle-0.4mm.html) |
| Boquilla latón 0.6 mm CHC V6 | ×2 | ~2 € el pack | [AliExpress](https://es.aliexpress.com/w/wholesale-v6-nozzle-0.6mm.html) |
| Tubo PTFE 2×4 mm (50 cm) | ×2 | ~1 € c/u | [AliExpress](https://es.aliexpress.com/w/wholesale-ptfe-tube-2mm.html) |
| Termistor NTC 100k (Generic 3950) | ×2 | ~1 € c/u | [AliExpress](https://es.aliexpress.com/w/wholesale-ntc-100k-thermistor.html) |
| Cartucho calefactor 24V 40W | ×2 | ~2 € c/u | [AliExpress](https://es.aliexpress.com/w/wholesale-heater-cartridge-24v-40w.html) |
| Grasa de litio blanca (Super Lube) | 1 bote | ~8 € | [Amazon ES](https://www.amazon.es/s?k=super+lube+grasa+litio) |
| Ventilador 2510 24V (hotend) | ×1 | ~5 € | [AliExpress](https://es.aliexpress.com/item/1005006831848917.html) |
| Ventilador 4010 24V (capa) | ×2 | ~3 € el par | [AliExpress](https://es.aliexpress.com/item/1005003371996395.html) |
| Insertos M3 calor ×20 | ×1 bolsa | ~1 € | [AliExpress](https://es.aliexpress.com/item/1005008285787978.html) |
| **Total stock de repuestos** | | **~26 €** | |

---

## Log de mantenimiento

Llevar un registro básico ayuda a identificar patrones de desgaste y planificar sustituciones.

| Fecha | Horas acum. | Acción realizada | Notas |
|-------|------------|-----------------|-------|
| — | 0 h | Instalación inicial | — |
| | | | |
| | | | |

> Actualizar este log tras cada sesión de mantenimiento significativa.
