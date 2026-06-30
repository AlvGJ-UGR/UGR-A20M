# ⚡ Esquema de conexiones — SKR Mini E3 V3.0

**Proyecto:** UGR-A20M  
**Placa:** BTT SKR Mini E3 V3.0 (STM32G0B1)  
**Referencia pinout oficial:** [GitHub BigTreeTech](https://github.com/bigtreetech/BIGTREETECH-SKR-mini-E3/tree/master/hardware/BTT%20SKR%20MINI%20E3%20V3.0)

> ⚠️ **Desconectar siempre la impresora de la corriente antes de manipular cualquier conector o cable.**

---

## Vista general de conexiones

```
                    BTT SKR Mini E3 V3.0
    ┌────────────────────────────────────────────────────┐
    │                                                    │
    │  MOTORES (JST XH 2.54, 4 pines)                   │
    │  X-MOT  ──►  Motor eje X    (cable original A20M)  │
    │  Y-MOT  ──►  Motor eje Y    (cable original A20M)  │
    │  Z-MOT  ──►  Motor eje Z    (cable original A20M)  │
    │  E0-MOT ──►  Motor Sharkfin (cable nuevo ~60 cm)   │
    │                                                    │
    │  ENDSTOPS (JST XH 2.54, 3 pines)                  │
    │  X-STOP ──►  Endstop X  (NC, cable original)       │
    │  Y-STOP ──►  Endstop Y  (NC, cable original)       │
    │  Z-STOP     Sin usar — Z gestionado por CR-Touch   │
    │                                                    │
    │  CALENTADORES (Molex 2 pines)                      │
    │  HE0    ──►  Cartucho calefactor hotend  24V ~40W  │
    │  HB     ──►  Cama caliente               24V ~200W │
    │                                                    │
    │  TERMISTORES (JST XH 2.54, 2 pines)               │
    │  TH0    ──►  Termistor hotend (CHC V6)             │
    │  THB    ──►  Termistor cama                        │
    │                                                    │
    │  VENTILADORES (JST XH 2.54, 2 pines)              │
    │  FAN0   ──►  Ventilador hotend 2510 24V            │
    │  FAN1   ──►  Ventiladores capa 4010 24V ×2         │
    │                                                    │
    │  CR-TOUCH (JST PH 2.0, 5 pines)                   │
    │  BLTouch ──►  GND · 5V · SENSOR(PC14) · SERVO(PA1)│
    │                                                    │
    │  ALIMENTACIÓN                                      │
    │  PWR IN ──►  PSU 24V DC 360W                       │
    │  USB    ──►  Orange Pi Zero 3 (cable USB-A → USB-B)│
    │                                                    │
    └────────────────────────────────────────────────────┘
```

---

## Motores paso a paso

Todos los motores usan **conectores JST XH 2.54 mm de 4 pines**. Los drivers TMC2209 están integrados en la placa — no hay módulos externos que instalar.

| Conector | Motor | Cable | Longitud recomendada |
|----------|-------|-------|----------------------|
| X-MOT | NEMA 17 eje X | Original A20M | — (usar el original) |
| Y-MOT | NEMA 17 eje Y | Original A20M | — |
| Z-MOT | NEMA 17 eje Z | Original A20M | — |
| E0-MOT | NEMA 17 pancake (Sharkfin) | **Cable nuevo** | ~55–65 cm desde la placa hasta el toolhead |

### Orden de pines del conector JST XH (motor)

El orden estándar para motores NEMA 17 bipolares es:

```
Pin 1 ── A+  (bobina A, polo positivo)
Pin 2 ── A−  (bobina A, polo negativo)
Pin 3 ── B+  (bobina B, polo positivo)
Pin 4 ── B−  (bobina B, polo negativo)
```

> Si el motor gira al revés, **no invertir el conector físicamente**. Editar `printer.cfg` añadiendo o quitando `!` en el `dir_pin` del motor afectado. Invertir físicamente el conector puede dañar el driver.

### Conector libre del segundo extrusor

La Geeetech A20M original tiene dos motores de extrusor (sistema dual mixing). Al instalar el Sharkfin, solo se usa uno. El segundo motor Bowden y su conector quedan libres — **desconectarlos y guardarlos**. No hace falta configurar nada en Klipper para el motor desconectado.

---

## Endstops

La A20M usa finales de carrera mecánicos de tipo **NC** (normalmente cerrado). Usar los cables originales de la impresora.

| Conector | Endstop | Estado con Klipper |
|----------|---------|-------------------|
| X-STOP | Final de carrera eje X | Activo — homing X |
| Y-STOP | Final de carrera eje Y | Activo — homing Y |
| Z-STOP | Final de carrera eje Z | **Sin usar** — el CR-Touch gestiona el homing Z |

Para verificar que los endstops funcionan, ejecutar en Klipper:
```
QUERY_ENDSTOPS
```
Sin pulsar: `open`. Pulsando manualmente el endstop: `triggered`.

---

## CR-Touch

El conector BLTouch de la SKR Mini E3 V3 acepta directamente el CR-Touch original de Creality. El conector es **JST PH 2.0 mm de 5 pines**.

| Orden en conector SKR | Color cable CR-Touch | Pin MCU | Función |
|----------------------|----------------------|---------|---------|
| 1 | **Negro** | GND | Masa |
| 2 | **Rojo** | +5V | Alimentación |
| 3 | **Blanco** | PC14 | Señal del sensor (entrada digital) |
| 4 | **Amarillo** | PA1 | Control del servo (salida PWM) |
| 5 | Marrón (algunas versiones) | — | No conectar |

> ⚠️ El orden de los pines importa. Conectar al revés puede dañar el CR-Touch o la placa. Verificar el marcado de la placa antes de conectar.

**Prueba del CR-Touch** tras conectar (desde la consola de Klipper):
```
BLTOUCH_DEBUG COMMAND=pin_down    # despliega la sonda
BLTOUCH_DEBUG COMMAND=pin_up      # recoge la sonda
BLTOUCH_DEBUG COMMAND=self_test   # test de auto-diagnóstico
```

---

## Calentadores

| Conector | Dispositivo | Tensión | Potencia | Tipo de conector |
|----------|------------|---------|---------|-----------------|
| HE0 | Cartucho calefactor hotend (CHC V6) | 24V | ~40 W (~1.7 A) | Molex 2 pines |
| HB | Cama caliente | 24V | ~150–200 W (~6.3–8.3 A) | Molex 2 pines |

> ⚠️ **Amperaje de la cama cerca del límite del MOSFET.** El MOSFET de la cama en la SKR Mini E3 V3 soporta hasta ~11 A según la revisión de la placa, pero con la cama original de la A20M (~200W ≈ 8.3 A) el margen es ajustado. Verificar que el conector HB no se calienta tras los primeros minutos de uso continuado; si se calienta de forma notable, instalar un MOSFET externo de potencia entre la PSU y la cama (recomendado para cualquier cama > 150 W de forma preventiva).

> ⚠️ La Geeetech A20M existe en versiones con cama de 24V DC y 220V AC. **Verificar la etiqueta de la cama** antes de conectar. Este proyecto usa exclusivamente la versión de 24V DC. Si la cama es de 220V AC, NO conectar al HB de la SKR — requiere un SSR (Solid State Relay) externo, lo que está fuera del alcance de este proyecto.

---

## Termistores

| Conector | Sensor | Tipo en `printer.cfg` |
|----------|--------|----------------------|
| TH0 | Termistor hotend — CHC V6 Volcano | `Generic 3950` |
| THB | Termistor cama caliente | `EPCOS 100K B57560G104F` |

Usar los termistores originales de la A20M para la cama. El termistor del CHC V6 Volcano viene incluido con el hotend.

**Verificación:** con la impresora fría, ambos termistores deben leer aproximadamente la temperatura ambiente (±5 °C). Una lectura de 0 °C indica circuito abierto; −14 °C indica cable roto o desconectado.

---

## Ventiladores

| Conector | Ventilador | Tensión | Corriente | Notas |
|----------|-----------|---------|----------|-------|
| FAN0 (PC7) | Hotend 2510 axial | 24V | ~0.08 A | Controlado automáticamente: activo cuando hotend > 50 °C |
| FAN1 (PC6) | Capa 4010 radial ×2 **en paralelo** | 24V | ~0.15 A × 2 = 0.30 A total | Controlado por el slicer (M106/M107) |

La SKR Mini E3 V3 soporta hasta **1 A por pin de ventilador**. Los dos ventiladores 4010 en paralelo consumen 0.30 A en total — dentro del límite.

**Conexión en paralelo de los dos 4010:** el conector FAN1 de la SKR tiene 2 pines (+ y −). Usar un cable en Y con conector JST hembra de 2 pines en el lado de la placa y dos conectores JST macho de 2 pines en el lado de los ventiladores, respetando la polaridad en ambos (+ con +, − con −). No conectar un ventilador al conector FAN1 y "extender" el segundo desde los mismos pines sin un splitter — el contacto directo sobre el pin ya ocupado es poco fiable y puede causar falsos contactos.

---

## Comunicación SKR ↔ Orange Pi

| Elemento | Detalle |
|----------|---------|
| Cable | USB-A (Orange Pi) → USB Micro-B (SKR Mini E3 V3) |
| Longitud recomendada | ≤ 50 cm para evitar caídas de tensión |
| Calidad del cable | Usar cable con hilos de datos (no solo carga). Un cable solo de carga no funcionará |
| Identificación en la OPi | `ls /dev/serial/by-id/` → debe aparecer `usb-Klipper_stm32g0b1xx_...` |

Si la SKR no aparece en `/dev/serial/by-id/`, verificar:
1. El cable tiene hilos de datos
2. El firmware de Klipper se flasheó correctamente (el archivo debe llamarse `firmware.cur` en la SD)
3. `ls /dev/ttyACM*` — si aparece, es problema del serial en `printer.cfg`

---

## Flujo de alimentación

```
PSU 24V DC (360 W)
    │
    ├─► SKR Mini E3 V3.0 (entrada 24V)
    │       ├─► Motores X, Y, Z, E0  (vía TMC2209)
    │       ├─► Calentador hotend HE0  (24V, MOSFET interno)
    │       ├─► Ventiladores FAN0, FAN1  (24V, MOSFET interno)
    │       ├─► Regulador 5V interno ──► CR-Touch
    │       └─► Puerto USB ──► Orange Pi Zero 3 (alimentación y datos)
    │
    └─► Cama caliente HB  (24V directo, MOSFET externo en la A20M)
```

> La Orange Pi se alimenta por el USB de la SKR (~0.5–1 A a 5V). Si la OPi se reinicia sola durante impresiones largas, puede ser insuficiente: añadir una fuente 5V externa para la OPi.

---

## Checklist pre-encendido

Verificar antes del primer arranque. Un error aquí puede dañar la electrónica.

- [ ] Polaridad de la PSU correcta en el conector de la SKR (rojo = +24V, negro = GND)
- [ ] Ningún cable pelado toca la carcasa metálica o el bastidor
- [ ] TH0 = termistor hotend, THB = termistor cama (no intercambiados)
- [ ] HE0 = calentador hotend, HB = cama caliente (no intercambiados)
- [ ] CR-Touch en el conector BLTouch con el orden correcto (GND · 5V · SENSOR · SERVO)
- [ ] Cable USB entre SKR y Orange Pi conectado en ambos extremos
- [ ] La microSD con el firmware de Klipper retirada de la SKR (o el archivo renombrado a `firmware.cur`)

**Tras el primer encendido:**

1. `QUERY_ENDSTOPS` → X e Y deben aparecer como `open`
2. Las temperaturas de hotend y cama deben leer ~temperatura ambiente
3. `BLTOUCH_DEBUG COMMAND=pin_down` → la sonda del CR-Touch debe desplegarse
4. `G28 X` → el eje X debe moverse hacia el endstop y detenerse
