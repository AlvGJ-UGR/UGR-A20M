# 📌 Pinout de referencia — BTT SKR Mini E3 V3.0

Referencia rápida de todos los pines disponibles en la SKR Mini E3 V3.0 y su uso en el proyecto UGR-A20M. Útil al añadir sensores, LEDs u otros accesorios.

**Referencia oficial:** [GitHub BigTreeTech — SKR Mini E3 V3 Schematic](https://github.com/bigtreetech/BIGTREETECH-SKR-mini-E3/tree/master/hardware/BTT%20SKR%20MINI%20E3%20V3.0)

---

## Pines usados por el proyecto

| Pin MCU | Función en `printer.cfg` | Conector físico | Estado |
|---------|--------------------------|----------------|--------|
| PB13 | `stepper_x step_pin` | X-MOT | ✅ En uso |
| PB12 | `stepper_x dir_pin` | X-MOT | ✅ En uso |
| PB14 | `stepper_x enable_pin` | X-MOT | ✅ En uso |
| PC0 | `endstop_pin` (X) | X-STOP | ✅ En uso |
| PB10 | `stepper_y step_pin` | Y-MOT | ✅ En uso |
| PB2 | `stepper_y dir_pin` | Y-MOT | ✅ En uso |
| PB11 | `stepper_y enable_pin` | Y-MOT | ✅ En uso |
| PC1 | `endstop_pin` (Y) | Y-STOP | ✅ En uso |
| PB0 | `stepper_z step_pin` | Z-MOT | ✅ En uso |
| PC5 | `stepper_z dir_pin` | Z-MOT | ✅ En uso |
| PB1 | `stepper_z enable_pin` | Z-MOT | ✅ En uso |
| PB3 | `stepper_e step_pin` | E0-MOT | ✅ En uso |
| PB4 | `stepper_e dir_pin` | E0-MOT | ✅ En uso |
| PD1 | `stepper_e enable_pin` | E0-MOT | ✅ En uso |
| PC8 | `heater_pin` (hotend) | HE0 | ✅ En uso |
| PA0 | `sensor_pin` TH0 | TH0 | ✅ En uso |
| PC9 | `heater_pin` (cama) | HB | ✅ En uso |
| PC4 | `sensor_pin` THB | THB | ✅ En uso |
| PC7 | `heater_fan pin` | FAN0 | ✅ En uso |
| PC6 | `fan pin` (capa) | FAN1 | ✅ En uso |
| PC14 | `bltouch sensor_pin` | BLTouch | ✅ En uso |
| PA1 | `bltouch control_pin` | BLTouch | ✅ En uso |
| PC11 | `uart_pin` (TMC UART bus) | Interno | ✅ En uso |
| PC10 | `tx_pin` (TMC UART bus) | Interno | ✅ En uso |
| PA11 | USB D− | USB | ✅ En uso |
| PA12 | USB D+ | USB | ✅ En uso |

---

## Pines disponibles para expansión

Estos pines están físicamente accesibles en la placa pero no están en uso en la configuración actual del proyecto.

| Pin MCU | Conector / Pad | Tipo | Uso potencial |
|---------|---------------|------|---------------|
| PC15 | EXP / pad libre | GPIO digital | **Sensor de filamento** (ver sección de configuración) |
| PA4 | EXP SPI | SPI CS | ADXL345 (acelerómetro Input Shaping) |
| PA5 | EXP SPI | SPI SCLK | ADXL345 |
| PA7 | EXP SPI | SPI MOSI | ADXL345 |
| PA6 | EXP SPI | SPI MISO | ADXL345 |
| PA2 | UART | TX | Puerto serie auxiliar |
| PA3 | UART | RX | Puerto serie auxiliar |
| PC2 | Libre | GPIO | LED de estado, relé, etc. |
| PC3 | Libre | GPIO | LED de estado, relé, etc. |

---

## UART de los drivers TMC2209

Los 4 drivers comparten un bus UART multiplexado. La dirección de cada driver se configura en `printer.cfg`:

| Driver | Motor | `uart_address` |
|--------|-------|---------------|
| TMC2209 #0 | Extrusor (E0) | `0` |
| TMC2209 #1 | Eje Z | `1` |
| TMC2209 #2 | Eje X | `2` |
| TMC2209 #3 | Eje Y | `3` |

```ini
# Ejemplo en printer.cfg:
[tmc2209 stepper_x]
uart_pin: PC11
tx_pin: PC10
uart_address: 2
```

---

## Sensor de filamento (PC15)

Para añadir un sensor de filamento en el futuro, conectar al pad PC15 y descomentar en `printer.cfg`:

```ini
[filament_switch_sensor runout_sensor]
switch_pin: ^PC15   # ^ = pull-up interno activado
pause_on_runout: False
runout_gcode: FILAMENT_RUNOUT
insert_gcode: M117 Filamento detectado
event_delay: 3.0
pause_delay: 0.5
```

El sensor típico es un microswitch de 3 pines (VCC · GND · SIGNAL). Conectar VCC a 3.3V o 5V del conector EXP, GND a GND y SIGNAL a PC15.

---

## ADXL345 para Input Shaping

El acelerómetro se conecta por SPI a los pines del conector EXP. Descomentar las secciones correspondientes en `printer.cfg` (sección 15 — Input Shaping):

```ini
[adxl345]
cs_pin: PA4
spi_software_sclk_pin: PA5
spi_software_mosi_pin: PA7
spi_software_miso_pin: PA6

[resonance_tester]
accel_chip: adxl345
probe_points: 127, 127, 20
```

Tras conectar, ejecutar `CALIBRATE_INPUT_SHAPING` desde Fluidd.

---

## FAN2 — Tercer canal de ventilador

La SKR Mini E3 V3 tiene un tercer canal de ventilador (**FAN2**) disponible. En este proyecto no se usa, pero puede aprovecharse para:

- Ventilador de la electrónica/PSU controlado por temperatura
- Ventilador de recinto cerrado
- Un segundo ventilador de hotend si el shroud lo requiere

```ini
# Ejemplo: ventilador de electrónica activado por temperatura MCU
[temperature_fan electronics_fan]
pin: PA8              # FAN2 pin
sensor_type: temperature_mcu
min_temp: 0
max_temp: 80
target_temp: 45.0
min_speed: 0.3
max_speed: 1.0
control: watermark
```

---

## Notas de voltaje

| Conector | Voltaje disponible |
|----------|-------------------|
| PWR IN | 24V DC (entrada PSU) |
| HE0, HB, FAN0, FAN1, FAN2 | 24V (directo de la PSU) |
| BLTouch (5V pin) | 5V regulado interno |
| EXP (lógica) | 3.3V |

> No conectar dispositivos de 5V a los pines de 24V ni viceversa. El CR-Touch opera a 5V para la lógica pero el control del servo puede operar a 3.3V — la SKR lo gestiona internamente.
