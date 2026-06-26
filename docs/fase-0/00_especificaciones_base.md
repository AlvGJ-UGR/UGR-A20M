# 📋 Fase 0 — Geeetech A20M: estado original y motivación

---

## Descripción de la máquina base

La **Geeetech A20M** es una impresora FDM cartesiana de gama media fabricada por Shenzhen Geeetech Technology. Su característica diferencial es el sistema de **mezcla de colores**: dos extrusores Bowden alimentan un único hotend con mezclador, permitiendo imprimir gradientes y combinaciones de dos filamentos.

Para este proyecto, la funcionalidad de doble color se descarta — el hotend mixing se sustituye por un hotend estándar de alto caudal (CHC V6 Volcano) con extrusor directo. El objetivo es maximizar la calidad y velocidad de impresión monocolor.

---

## Especificaciones técnicas originales

| Parámetro | Valor |
|-----------|-------|
| **Modelo** | Geeetech A20M |
| **Fabricante** | Shenzhen Geeetech Technology Co., Ltd. |
| **Tipo** | FDM (Fused Deposition Modeling) |
| **Cinemática** | Cartesiana — eje Z independiente, XY en cabezal |
| **Sistema de extrusión** | Bowden dual mixing (2 motores, 1 hotend) |
| **Volumen de impresión** | 255 × 255 × 255 mm |
| **Resolución de capa** | 0.1–0.4 mm |
| **Diámetro de filamento** | 1.75 mm |
| **Temperatura hotend máx.** | 250 °C |
| **Temperatura cama máx.** | 100 °C |
| **Velocidad máx. (fabricante)** | 100 mm/s (en la práctica ~60 mm/s estable) |
| **Precisión posicionamiento X/Y** | 0.1 mm |
| **Precisión posicionamiento Z** | 0.0025 mm |
| **Fuente de alimentación** | 24V DC, 15A — 360W |
| **Conectividad** | SD Card, USB serie |
| **Pantalla** | LCD 12864 gráfico con encoder rotativo |
| **Dimensiones (máquina)** | 487 × 465 × 516 mm |
| **Peso** | ~9 kg |
| **Precio original** | ~200–250 € |

---

## Electrónica original

| Componente | Especificación | Limitaciones |
|------------|---------------|-------------|
| **Placa controladora** | Geeetech GT2560 v3 (ATmega2560, 8-bit, 16 MHz) | Potencia de cálculo insuficiente para Klipper avanzado |
| **Drivers de motores** | A4988 integrados | Ruidosos, sin UART, sin StealthChop |
| **Firmware** | Marlin 1.x personalizado por Geeetech | Código cerrado, difícil de actualizar |
| **Pantalla** | LCD 12864 con encoder | Sin interfaz web, sin control remoto |
| **Conectividad** | SD Card + USB serie | Sin WiFi, sin red |
| **Hotend** | Dual mixing J-Head | Temperatura máx. 250 °C, caudal limitado |
| **Sensor de nivelación** | Ninguno (nivelación manual con 4 tornillos) | Tedioso, impreciso |
| **Ventilación** | 1× 40mm hotend, 1× 40mm capa | Refrigeración de capa unilateral |

---

## Problemas identificados que motivan el proyecto

### 🔊 Ruido excesivo
Los drivers A4988 operan en modo full-step o microstepping sin interpolación, generando un ruido característico a frecuencias audibles molestas. Los TMC2209 con StealthChop reducen el ruido de los motores hasta casi imperceptible.

### 🐢 Velocidad práctica limitada
A pesar de que el fabricante indica 100 mm/s, la combinación de Bowden largo + placa 8-bit + firmware Marlin 1.x limita la velocidad práctica estable a ~60 mm/s antes de aparecer artefactos. Con Klipper + Input Shaping se espera alcanzar 150–200 mm/s.

### 🧵 Stringing y calidad en Bowden
El tubo PTFE de ~40 cm entre el motor y el hotend introduce retardos de flujo que se traducen en stringing, blobs en reanudaciones y dificultad para imprimir flexibles. La conversión a extrusión directa elimina estos problemas.

### 🎯 Sin nivelación automática
La nivelación manual de 4 tornillos es imprecisa y debe repetirse frecuentemente. El CR-Touch con mesh 5×5 compensa automáticamente las variaciones de la cama en cada impresión.

### 🌐 Sin control remoto
La impresora solo puede controlarse localmente (SD card o USB). Klipper con Fluidd permite control completo desde cualquier dispositivo en la misma red.

### 🌡️ Temperatura máxima limitada
El hotend original llega a 250 °C, suficiente para PLA y ABS pero insuficiente para materiales técnicos como PA (Nylon), PC o PEI. El CHC V6 Volcano alcanza 285–300 °C.

---

## Estado físico al inicio del proyecto

> Completar con fotografías en `photos/estado-inicial/` antes de iniciar las modificaciones.

### Checklist de documentación inicial

- [ ] Foto frontal de la máquina (ángulo 3/4)
- [ ] Foto de la placa GT2560 y conexionado
- [ ] Foto del hotend mixing y extrusores Bowden originales
- [ ] Foto de la pantalla LCD y controles
- [ ] Impresión de referencia: Benchy con configuración de fábrica
- [ ] Registro de temperatura de hotend durante impresión (oscilaciones)
- [ ] Medición de ruido en operación (dB con app de móvil)
- [ ] Medición dimensional de cubo 20×20×20 impreso en stock

### Parámetros de referencia del slicer original (Marlin stock)

| Parámetro | Valor stock |
|-----------|-------------|
| Velocidad impresión | 60 mm/s |
| Velocidad primera capa | 20 mm/s |
| Retracción | 6 mm a 45 mm/s |
| Temperatura PLA | 200 °C / cama 60 °C |
| Temperatura ABS | 240 °C / cama 100 °C |

Estos valores sirven como referencia de partida para comparar el rendimiento tras cada fase de mejora.

---

## Decisiones de diseño del proyecto

### Por qué Klipper en lugar de Marlin 2.x

Marlin 2.x sería la opción más sencilla (misma placa), pero Klipper ofrece ventajas que justifican el cambio de hardware:

- **Input Shaping**: compensación activa de resonancias — imposible en Marlin sin hardware específico
- **Pressure Advance**: equivalente al Linear Advance de Marlin, pero más preciso y fácil de calibrar
- **Velocidad de procesamiento**: Klipper delega el procesamiento de G-code a la Orange Pi (ARM Cortex-A53), dejando la placa solo para el control en tiempo real
- **Interfaz web (Fluidd)**: monitorización y control desde cualquier dispositivo sin software adicional
- **Configuración en texto plano**: `printer.cfg` editable desde cualquier editor, versionable en Git

### Por qué SKR Mini E3 V3 y no una placa más potente

La SKR Mini E3 V3 es la elección más eficiente para este proyecto por varios motivos:
- TMC2209 integrados (no requiere drivers externos)
- Factor de forma compacto — cabe en el mismo espacio que la GT2560
- 32-bit STM32G0B1 — suficiente para Klipper (el procesamiento pesado va en la Orange Pi)
- Precio competitivo (~25 €)
- Comunidad enorme y configuraciones de referencia disponibles

### Por qué Orange Pi Zero 3 y no Raspberry Pi

La escasez y el precio elevado de las Raspberry Pi 4 en 2024–2025 hizo de la Orange Pi Zero 3 una alternativa sólida:
- Precio más bajo (~25 € vs ~60–70 € RPi 4)
- Rendimiento suficiente para Klipper + Moonraker + Fluidd (Cortex-A53 @1.5 GHz, 1 GB RAM)
- Armbian ofrece soporte estable para Debian/Ubuntu
- USB OTG disponible para la conexión con la SKR
