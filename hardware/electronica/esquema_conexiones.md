# ⚡ Esquema de conexiones — SKR Mini E3 V3.0

**Proyecto:** UGR-A20M  
**Placa:** BTT SKR Mini E3 V3.0  
**Referencia pinout oficial:** [GitHub BigTreeTech](https://github.com/bigtreetech/BIGTREETECH-SKR-mini-E3/tree/master/hardware/BTT%20SKR%20MINI%20E3%20V3.0)

> ⚠️ Desconectar siempre la impresora de la corriente antes de manipular la electrónica.

---

## Mapa de conexiones completo

```
┌─────────────────────────────────────────────────────────────────┐
│                    BTT SKR Mini E3 V3.0                         │
│                                                                 │
│  MOTORES                      CALENTADORES / SENSORES           │
│  ──────                       ──────────────────────           │
│  X-MOT  ──► Motor eje X       HE0   ──► Calentador hotend       │
│  Y-MOT  ──► Motor eje Y       HB    ──► Calentador cama (24V)   │
│  Z-MOT  ──► Motor eje Z       TH0   ──► Termistor hotend        │
│  E0-MOT ──► Motor extrusor    THB   ──► Termistor cama          │
│                                                                 │
│  ENDSTOPS                     VENTILADORES                      │
│  ────────                     ────────────                      │
│  X-STOP ──► Endstop X (NC)    FAN0  ──► Ventilador hotend 2510  │
│  Y-STOP ──► Endstop Y (NC)    FAN1  ──► Ventiladores capa 4010  │
│  (Z-STOP no usado — CR-Touch)                                   │
│                                                                 │
│  CR-TOUCH                     ALIMENTACIÓN                      │
│  ────────                     ─────────────                     │
│  BLTouch 5V    ──► CR-Touch 5V (+)    PWR IN ──► 24V DC PSU     │
│  BLTouch GND   ──► CR-Touch GND (-)  USB     ──► Orange Pi Zero3│
│  BLTouch SERVO ──► CR-Touch Señal amarillo                      │
│  BLTouch SENSOR──► CR-Touch Señal blanco                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Detalle por conector

### Motores paso a paso

Todos los motores usan conectores JST XH 2.54 de 4 pines.  
La SKR Mini E3 V3 lleva los drivers **TMC2209** integrados en la placa.

| Conector placa | Motor | Cable |
|---------------|-------|-------|
| X-MOT | NEMA 17 eje X | Original Geeetech A20M |
| Y-MOT | NEMA 17 eje Y | Original Geeetech A20M |
| Z-MOT | NEMA 17 eje Z | Original Geeetech A20M |
| E0-MOT | NEMA 17 pancake (Sharkfin) | Cable nuevo — ver longitud |

> ⚠️ Si un motor gira en dirección contraria, no invertir el cable físicamente: modificar el `dir_pin` en `printer.cfg` añadiendo o quitando el `!`.

### Endstops

La A20M usa endstops mecánicos de tipo **NC** (normalmente cerrado).

| Conector placa | Endstop | Notas |
|---------------|---------|-------|
| X-STOP | Endstop X (final de carrera) | Cables originales de la A20M |
| Y-STOP | Endstop Y (final de carrera) | Cables originales de la A20M |
| Z-STOP | **No usado** | Z-offset gestionado por CR-Touch |

### CR-Touch (autonivelado)

El conector BLTouch de la SKR Mini E3 V3 es de 5 pines. El CR-Touch usa los mismos pines que el BLTouch original.

| Pin conector SKR | Color cable CR-Touch | Función |
|-----------------|---------------------|---------|
| GND | Negro | Masa |
| +5V | Rojo | Alimentación 5V |
| PC14 (SENSOR) | Blanco | Señal del sensor (entrada) |
| PA1 (SERVO) | Amarillo | Control servo (salida) |
| — | Marrón | No conectar (algunas versiones) |

> El conector BLTouch está marcado en la placa. Conectar en el orden correcto: GND, 5V, SENSOR, SERVO.

### Calentadores

| Conector placa | Dispositivo | Voltaje | Potencia |
|---------------|-------------|---------|---------|
| HE0 | Cartucho calefactor hotend | 24V | ~40 W |
| HB | Cama caliente | 24V | ~200 W |

> La cama caliente de la Geeetech A20M puede ser de 220V AC o 24V DC según la versión. Verificar la etiqueta antes de conectar.

### Termistores

| Conector placa | Sensor | Tipo |
|---------------|--------|------|
| TH0 | Termistor hotend (CHC V6) | NTC 100k — Generic 3950 |
| THB | Termistor cama | NTC 100k — EPCOS B57560G104F |

### Ventiladores

| Conector placa | Ventilador | Tipo | Voltaje |
|---------------|-----------|------|---------|
| FAN0 (PC7) | Ventilador hotend 2510 | Siempre activo cuando T > 50 °C | 24V |
| FAN1 (PC6) | Ventiladores capa 4010 ×2 (en paralelo) | Controlado por slicer | 24V |

> Los dos ventiladores de capa del Mini Stealth se conectan en paralelo al conector FAN1. La SKR Mini E3 V3 puede suministrar hasta 1A por pin de ventilador; dos ventiladores 4010 de 24V consumen ~0.15A cada uno, dentro del límite.

### Comunicación Orange Pi ↔ SKR

| Conexión | Método |
|----------|--------|
| Orange Pi Zero 3 → SKR Mini E3 V3 | Cable USB-A a USB Micro-B |
| Identificación en Orange Pi | `/dev/serial/by-id/usb-Klipper_stm32g0b1xx_...` |

---

## Diagrama de flujo de energía

```
Fuente de alimentación 24V DC (360W)
        │
        ├──► SKR Mini E3 V3.0 (24V entrada)
        │       ├── Motores (TMC2209)
        │       ├── Calentador hotend (HE0)
        │       ├── Ventiladores FAN0, FAN1
        │       └── 5V regulados → CR-Touch, Orange Pi (USB)
        │
        └──► Cama caliente (HB — 24V directo, MOSFET externo en A20M)
```

---

## Verificación post-instalación

Antes de encender la impresora por primera vez, verificar:

- [ ] Polaridad de la fuente de alimentación correcta (rojo = +24V, negro = GND)
- [ ] Cables de motores bien fijados (ningún pin suelto)
- [ ] Termistores en los conectores correctos (TH0 = hotend, THB = cama)
- [ ] CR-Touch conectado con la polaridad correcta
- [ ] Cable USB entre la Orange Pi y la SKR conectado
- [ ] No hay cables pelados tocando la carcasa metálica (riesgo de cortocircuito)

Tras encender:

1. Verificar en Fluidd que las temperaturas del hotend y la cama son coherentes (~25 °C si está a temperatura ambiente)
2. Ejecutar `QUERY_ENDSTOPS` — deben aparecer como `open` (sin pulsar) o `triggered` (si están pulsados)
3. Ejecutar `G28 X` y verificar que el eje X se mueve hacia el endstop
