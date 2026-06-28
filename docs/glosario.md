# 📖 Glosario técnico — UGR-A20M

Definiciones de los términos técnicos usados en la documentación del proyecto, orientadas a estudiantes y makers sin experiencia previa en impresión 3D avanzada.

---

## A

**ADXL345**  
Acelerómetro digital de 3 ejes que se conecta a la placa para medir las vibraciones de la impresora. Se usa para calibrar el Input Shaping automáticamente con el comando `SHAPER_CALIBRATE`.

**ABS-juice**  
Solución de restos de ABS disueltos en acetona (~5 g por 100 ml). Se aplica sobre la cama caliente como adhesivo para piezas de ABS/ASA, mejorando la adherencia y reduciendo el warping.

**Armbian**  
Distribución Linux basada en Debian/Ubuntu optimizada para ordenadores de placa única (SBC) como la Orange Pi Zero 3. Es el sistema operativo que ejecuta Klipper en este proyecto.

---

## B

**Bed mesh / Mesh de nivelación**  
Mapa de la superficie de la cama generado midiendo múltiples puntos con el CR-Touch. Klipper usa este mapa para compensar en tiempo real las imperfecciones de la cama durante la impresión. En este proyecto se usa una malla 5×5 (25 puntos).

**BMG Clone**  
Réplica de los engranajes Bondtech BMG (Bondtech Mini Geared). Ofrecen una relación de reducción de ~3.5:1 entre el motor y el filamento, permitiendo usar un motor más pequeño (pancake) con mayor fuerza de agarre.

**Bowden**  
Sistema de extrusión donde el motor está separado del hotend por un tubo PTFE de longitud variable. La A20M original usa este sistema con ~40 cm de tubo, lo que provoca stringing y dificulta la impresión de flexibles.

**Brim**  
Extensión plana que se añade alrededor de la base de la pieza en el slicer para aumentar la superficie de contacto con la cama y prevenir el warping. Se recomienda para ABS/ASA sin recinto cerrado.

---

## C

**Carro X**  
Pieza que desliza por las guías o barras del eje X y sobre la que se fija el toolhead (extrusor + hotend + ventiladores). En la Fase 2, se sustituye el carro original por un adaptador compatible con las guías MGN12H.

**CHC V6 Volcano**  
Hotend de alto caudal compatible con el patrón de montaje E3D V6. El bloque calefactor "Volcano" es más grande que el estándar, permitiendo fundir más filamento por unidad de tiempo y alcanzar hasta 285–300 °C.

**Cold pull**  
Técnica de limpieza del interior del hotend: se calienta el hotend, se carga filamento, se enfría hasta ~90 °C y se extrae el filamento con un tirón firme. El filamento sale con la forma del interior del hotend, arrastrando los residuos carbonizados.

**Conventional Commits**  
Especificación estándar para mensajes de commit de Git: `tipo(ámbito): descripción`. Tipos usados en este proyecto: `feat` (nueva funcionalidad), `fix` (corrección), `docs` (documentación), `chore` (mantenimiento). Ver [conventionalcommits.org](https://www.conventionalcommits.org/). Usados en el flujo descrito en `CONTRIBUTING.md`.

**CR-Touch**  
Sensor de autonivelado fabricado por Creality. Funciona mediante un pin metálico retráctil servo-accionado que toca la cama en múltiples puntos para generar el bed mesh. Compatible con el protocolo BLTouch.

**CoreXY**  
Cinemática de impresora 3D donde dos motores mueven el cabezal en X e Y simultáneamente mediante un sistema de correas cruzadas. Permite mayor velocidad y precisión que la cartesiana clásica. Este proyecto **no** implementa CoreXY.

---

## D

**Direct drive (extrusión directa)**  
Sistema donde el motor del extrusor está montado directamente sobre el hotend, sin tubo Bowden intermedio. Permite retracciones más cortas (0.5–1.5 mm vs 5–8 mm en Bowden), mejor control del flujo y compatibilidad con materiales flexibles como el TPU.

---

## E

**E-steps**  
En Marlin, el número de pasos del motor necesarios para extruir 1 mm de filamento. En Klipper el concepto equivalente es `rotation_distance` — la distancia recorrida por vuelta completa del motor. Los E-steps originales de la A20M (96 steps/mm para el extrusor Bowden) no se trasladan directamente a Klipper; hay que calibrar `rotation_distance` desde cero siguiendo el procedimiento del Paso 2 de `guia_calibracion.md`.

**Extrusor**  
Conjunto mecánico que empuja el filamento hacia el hotend. En este proyecto: extrusor Sharkfin con engranajes BMG Clone, motor NEMA 17 pancake y relación de reducción ~3.5:1.

---

## F

**Fluidd**  
Interfaz web para controlar Klipper desde cualquier navegador. Se instala en la Orange Pi y permite ver temperaturas, mover ejes, iniciar impresiones y ver el log en tiempo real sin necesidad de pantalla LCD.

**FDM (Fused Deposition Modeling)**  
Tecnología de impresión 3D donde se funde un filamento termoplástico y se deposita capa a capa para formar la pieza. Es la tecnología usada en la Geeetech A20M y en la gran mayoría de impresoras domésticas.

---

## G

**gear_ratio**  
Parámetro de Klipper que define la relación de transmisión de los engranajes del extrusor. Para el BMG Clone se usa `50:17`, lo que significa que por cada 50 pasos del motor el filamento avanza 17/50 de vuelta del engranaje conductor.

**Ghosting / Ringing**  
Artefacto visual que aparece como ondas o ecos en las paredes verticales de la pieza, especialmente después de una esquina. Es causado por las vibraciones del chasis de la impresora. Se corrige calibrando el Input Shaping.

**G-code**  
Lenguaje de instrucciones que usan las impresoras 3D. Contiene comandos como `G28` (homing), `G1` (mover), `M104` (temperatura hotend). El slicer genera el G-code y Klipper lo interpreta.

---

## H

**Heat creep**  
Problema donde el calor del hotend sube por el tubo de ruptura térmica hasta la zona fría, fundiendo el filamento en un lugar incorrecto y provocando atascos. Se previene con el ventilador de hotend activo siempre que el hotend supere 50 °C.

**Homing**  
Proceso de llevar los ejes de la impresora a su posición de referencia (endstops). El comando `G28` ejecuta el homing. En el eje Z, el homing usa el CR-Touch en lugar del endstop mecánico original.

**Hotend**  
Conjunto que funde el filamento: bloque de calor (con el cartucho calefactor), bloque de ruptura térmica (disipa calor), radiador (disipa más calor) y boquilla (da forma al filamento fundido).

---

## I

**Input Shaping**  
Algoritmo de Klipper que compensa las vibraciones del chasis generando contravibaciones que las cancelan. Permite imprimir más rápido sin ghosting. Requiere calibración con un acelerómetro ADXL345.

---

## J

**JST**  
Familia de conectores eléctricos muy usada en electrónica de impresoras 3D. Los conectores JST-XH (2.54 mm paso) se usan para motores y termistores; los JST-PH (2 mm) para sensores como el CR-Touch.

---

## K

**KIAUH (Klipper Installation And Update Helper)**  
Script de bash que automatiza la instalación y actualización de Klipper, Moonraker, Fluidd y Mainsail en sistemas Linux. Es el método de instalación recomendado para este proyecto.

**Klipper**  
Firmware de impresora 3D que divide el procesamiento: el cálculo cinemático se ejecuta en el ordenador SBC (Orange Pi) y los comandos de motor en tiempo real se envían a la placa (SKR Mini E3 V3). Esto permite velocidades y algoritmos imposibles en firmware de 8 bits como Marlin.

---

## L

**LM8UU**  
Rodamiento lineal de bolas para barras de 8 mm de diámetro. Son los rodamientos que usa la Geeetech A20M original en los ejes X e Y. Se sustituyen por guías MGN12H en la Fase 2.

---

## M

**Mainsail**  
Alternativa a Fluidd como interfaz web para Klipper. Ambas son equivalentes en funcionalidad; este proyecto usa Fluidd por ser más ligera para la Orange Pi Zero 3 (1 GB RAM).

**MCU (Microcontroller Unit)**  
En el contexto de Klipper, el MCU es la placa controladora (SKR Mini E3 V3) que ejecuta el código de bajo nivel para controlar motores, calentadores y sensores en tiempo real.

**MGN12H**  
Guía lineal de recirculación de bolas de la serie MGN. El número 12 indica el ancho en mm; la H indica el tipo de carro (ancho, mayor superficie de contacto y rigidez). Se usan en la Fase 2 para sustituir las barras lisas.

**Moonraker**  
API REST que actúa de intermediario entre Klipper y las interfaces web (Fluidd, Mainsail). Gestiona la cola de impresión, los archivos G-code, las actualizaciones y la comunicación con el frontend.

---

## N

**NEMA 17**  
Estándar de tamaño para motores paso a paso: el número indica las dimensiones del flange frontal (17 = 1.7 pulgadas ≈ 42 mm). El **pancake** NEMA 17 es una versión más corta (20 mm de profundidad vs 40–48 mm del estándar), más ligero y por eso se usa en el extrusor Sharkfin.

**NTC 100k**  
Tipo de termistor (Negative Temperature Coefficient) de 100.000 ohmios a 25 °C. Es el termistor incluido en el CHC V6 Volcano. El tipo exacto para Klipper es `Generic 3950`.

---

## P

**Pressure Advance (PA)**  
Algoritmo de Klipper que compensa el retraso del hotend al cambiar de velocidad. Cuando la impresora acelera, Klipper añade una pequeña extrusión extra; cuando decelera, retrae un poco. Mejora la calidad de las esquinas y reduce el stringing. Equivalente al Linear Advance de Marlin.

**PTFE**  
Politetrafluoroetileno (teflón). Se usa como recubrimiento interno del tubo que guía el filamento entre el extrusor y el hotend. En extrusión directa, el tubo PTFE es muy corto (~10 mm).

---

## R

**Rotation distance**  
Parámetro de Klipper que define la distancia lineal (en mm) que recorre el filamento por cada vuelta completa del motor del extrusor. Se calibra midiendo cuánto filamento se extruye realmente al pedir 100 mm.

**run_current**  
Corriente en amperios que suministra el driver TMC2209 al motor en operación. Un valor demasiado bajo provoca pérdida de pasos; demasiado alto calienta el motor innecesariamente. Para el extrusor Sharkfin se usa 0.65 A.

---

## S

**SBC (Single Board Computer)**  
Ordenador completo en una sola placa de circuito impreso. En este proyecto se usa la **Orange Pi Zero 3** (1 GB RAM, Cortex-A53 @1.5 GHz) como ordenador anfitrión que ejecuta Klipper, Moonraker y Fluidd.

**Sharkfin**  
Extrusor open-source diseñado por KayosMaker para impresoras Voron. Usa engranajes BMG Clone con relación ~3.5:1 y es compatible con motores NEMA 17 pancake. Elegido en este proyecto por su relación calidad/peso/coste.

**SKR Mini E3 V3.0**  
Placa controladora de 32 bits de BigTreeTech con chip STM32G0B1, 4 drivers TMC2209 integrados y factor de forma similar al de placas Creality. Sustituye a la GT2560 v3 original de la A20M.

**Slicer**  
Software que convierte un modelo 3D (STL/3MF) en G-code para la impresora. Los más usados en este proyecto son **OrcaSlicer**, **PrusaSlicer** y **Bambu Studio**.

**StealthChop**  
Modo de operación silencioso de los drivers TMC2209. Usa interpolación para suavizar el movimiento del motor y reducir el ruido a niveles casi imperceptibles, especialmente en los ejes X e Y a baja velocidad.

**Stringing**  
Hilos finos de plástico que se forman entre partes separadas de la pieza cuando el nozzle se mueve sin extruir. Se reduce con una retracción correcta y con Pressure Advance calibrado.

---

## T

**T-nut**  
Tuerca especial con perfil en T que se inserta en la ranura de los perfiles de aluminio extruido (2020, 2040) y permite fijar accesorios sin perforar el perfil. Se usan para montar las guías MGN12H en la Fase 2.

**TMC2209**  
Driver de motor paso a paso de Trinamic. Soporta UART (configuración por software), StealthChop (modo silencioso) y SpreadCycle (modo de alta precisión). Los 4 drivers de la SKR Mini E3 V3 son TMC2209 integrados.

**Toolhead**  
Conjunto completo que se desplaza en el eje X: extrusor + hotend + ventiladores + sonda de nivelación. En este proyecto el toolhead es el Mini Stealth v2 con el extrusor Sharkfin.

**TPU**  
Poliuretano termoplástico. Material flexible y elástico. Solo es viable con extrusión directa — en sistemas Bowden el TPU se dobla dentro del tubo PTFE y provoca atascos.

---

## U

**UART**  
Protocolo de comunicación serie que usa el driver TMC2209 para recibir configuración desde el MCU. Permite ajustar la corriente, el modo de operación y leer el estado del driver sin cambiar hardware, simplemente editando `printer.cfg`.

---

## V

**Voron**  
Comunidad open-source de diseño de impresoras 3D de alta calidad y rendimiento. Sus diseños (Voron 2.4, Trident, 0.2) son referentes en la comunidad maker. El Mini Stealth v2 y el extrusor Sharkfin están inspirados en los toolheads Voron.

---

## W

**Warping**  
Deformación de las piezas de ABS/ASA durante la impresión: los bordes se levantan de la cama debido a la contracción del material al enfriarse. Se previene con recinto cerrado, cama caliente a temperatura correcta y brim.

---

## Z

**z_offset**  
Distancia entre la posición que el CR-Touch reporta como "cama" y la altura real a la que el nozzle toca la cama. Se calibra con `PROBE_CALIBRATE` y el método del papel. Un z_offset incorrecto arruina la primera capa.

**Z-hop**  
Movimiento vertical del eje Z antes de un viaje sin extrusión, para evitar que el nozzle roce la pieza. Con direct drive y PA bien calibrado, el z_hop puede reducirse al mínimo (0.1–0.2 mm).
