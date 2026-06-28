# ⚡ Fase 1a — Actualización electrónica

**BTT SKR Mini E3 V3.0 + Orange Pi Zero 3 + Klipper + Fluidd**

---

## 🎯 Objetivo

Sustituir la placa original **GT2560 v3 de 8 bits** y su firmware Marlin por una cadena moderna:

| Capa | Original | Nuevo |
|------|----------|-------|
| Placa controladora | GT2560 v3 (ATmega2560, 8-bit) | BTT SKR Mini E3 V3.0 (STM32G0B1, 32-bit) |
| Drivers motores | A4988 (ruidosos, sin UART) | TMC2209 integrados (silenciosos, StealthChop) |
| Ordenador anfitrión | Ninguno (SD + USB) | Orange Pi Zero 3 — 1 GB RAM |
| Firmware | Marlin 1.x | Klipper |
| Interfaz | LCD local | Fluidd (web, cualquier dispositivo) |

---

## 📦 Componentes

| Componente | Enlace | Precio |
|------------|--------|--------|
| BTT SKR Mini E3 V3.0 | [AliExpress](https://es.aliexpress.com/item/1005007912548824.html) | ~25 € |
| Orange Pi Zero 3 (1 GB) | [AliExpress](https://es.aliexpress.com/item/1005006047845950.html) | ~25 € |
| MicroSD SanDisk 32 GB | [Amazon ES](https://www.amazon.es/SanDisk-Tarjeta-microSDXC-Adaptador-Rendimiento/dp/B0B7NXBM6P) | ~8 € |

---

## 🔧 Proceso de instalación

### Parte 1 — Preparar la Orange Pi Zero 3

#### 1.1 Grabar Armbian en la microSD

1. Descargar la imagen **Armbian** para Orange Pi Zero 3:  
   → [armbian.com/orange-pi-zero3](https://www.armbian.com/orange-pi-zero3/)  
   Elegir **Armbian Bookworm** (basado en Debian 12) — versión **minimal**.

2. Grabar en la microSD con [Balena Etcher](https://etcher.balena.io/) o desde terminal:
   ```bash
   # Linux/macOS — sustituir /dev/sdX por el dispositivo correcto
   sudo dd if=Armbian_*.img of=/dev/sdX bs=4M status=progress conv=fsync
   ```

3. Insertar la microSD en la Orange Pi Zero 3 y conectar por Ethernet o WiFi.

#### 1.2 Primer arranque y configuración inicial

Conectar por SSH (usuario `root`, contraseña `1234` — se pedirá cambio en el primer acceso):

```bash
ssh root@<IP_de_la_opi>
```

> Encontrar la IP en el router o con `nmap -sn 192.168.1.0/24 | grep -i orange`.

El asistente de primer arranque hace lo siguiente — responder a cada prompt:
1. **Nueva contraseña root** — elegir una contraseña segura (se usará para SSH)
2. **Shell para root** — dejar bash (opción por defecto)
3. **Crear usuario normal** — crear un usuario con nombre propio (p. ej. `alvaro`); este usuario se usará para Klipper
4. **Contraseña del usuario** — diferente a la de root
5. **Zona horaria** — seleccionar `Europe/Madrid` o la correspondiente

Al terminar el asistente, la sesión SSH continuará como root.

#### 1.3 Configuración de red WiFi (opcional)

```bash
nmtui
```

Seleccionar "Activate a connection" → elegir la red WiFi → introducir contraseña.  
Tras conectar, verificar con `ip addr` y apuntar la IP para acceder sin Ethernet.

#### 1.4 Actualizar el sistema

```bash
apt update && apt upgrade -y
```

---

### Parte 2 — Instalar Klipper, Moonraker y Fluidd con KIAUH

[KIAUH](https://github.com/dw-0/kiauh) es el instalador oficial más cómodo para todo el stack Klipper.

```bash
# Instalar git si no está presente
apt install git -y

# Clonar KIAUH
git clone https://github.com/dw-0/kiauh.git ~/kiauh

# Ejecutar
cd ~/kiauh && ./kiauh.sh
```

Desde el menú de KIAUH, instalar en este orden:

| Paso | Opción KIAUH | Tiempo aprox. |
|------|-------------|--------------|
| 1 | **Klipper** | ~5 min |
| 2 | **Moonraker** | ~3 min |
| 3 | **Fluidd** | ~2 min |

> No instalar Mainsail y Fluidd simultáneamente — elegir uno. Fluidd es más ligero para la Orange Pi Zero 3.

---

### Parte 3 — Compilar y flashear Klipper en la SKR Mini E3 V3

#### 3.1 Compilar el firmware

```bash
cd ~/klipper
make menuconfig
```

Seleccionar exactamente estas opciones:

```
[*] Enable extra low-level configuration options
    Micro-controller Architecture  ---> STMicroelectronics STM32
    Processor model                ---> STM32G0B1
    Bootloader offset              ---> 8KiB bootloader
    Clock Reference                ---> 8 MHz crystal
    Communication interface        ---> USB (on PA11/PA12)
```

Salir y guardar. Compilar:

```bash
make -j4
```

El firmware generado estará en `~/klipper/out/klipper.bin`.

#### 3.2 Flashear la SKR Mini E3 V3

1. Formatear una microSD en **FAT32** (no exFAT)
2. Copiar el firmware y **renombrarlo** a `firmware.bin`:
   ```bash
   cp ~/klipper/out/klipper.bin /media/usuario/SD/firmware.bin
   ```
3. Insertar la microSD en la SKR Mini E3 V3 **con la impresora apagada**
4. Encender la impresora — la SKR flasheará automáticamente (LED parpadea ~10 s)
5. Al terminar, el archivo se renombra a `firmware.cur` en la SD — confirma que el flash fue exitoso
6. Retirar la microSD de la SKR

#### 3.3 Obtener el serial del MCU

Con la SKR conectada a la Orange Pi por USB:

```bash
ls /dev/serial/by-id/
```

La salida será algo como:
```
usb-Klipper_stm32g0b1xx_2B0044000B50304158373520-if00
```

Copiar esta ruta completa — se necesita para `printer.cfg`.

---

### Parte 4 — Instalar la SKR Mini E3 V3.0 en la impresora

> ⚠️ **Desconectar la impresora de la corriente antes de cualquier manipulación eléctrica.**

#### 4.1 Retirar la placa GT2560

1. Fotografiar el conexionado original antes de desmontar (referencia útil)
2. Etiquetar cada conector si es necesario
3. Retirar la placa GT2560 y sus soportes

#### 4.2 Montar la SKR Mini E3 V3

La SKR Mini E3 V3 tiene el mismo factor de forma que muchas placas Creality (32×100 mm, 4 orificios M3 a 85×25 mm). Verificar que los soportes del chasis de la A20M coinciden antes de instalar.

Si los orificios no coinciden exactamente, hay dos opciones:
- Usar bridas de nylon para sujetar temporalmente la placa mientras se verifica que funciona
- Imprimir un soporte adaptador: buscar en [Printables — SKR Mini E3 mount](https://www.printables.com/search/models?q=skr+mini+e3+mount) o diseñar uno con las medidas del chasis original

#### 4.3 Conectar todos los periféricos

Seguir el esquema completo en [`hardware/electronica/esquema_conexiones.md`](../../../hardware/electronica/esquema_conexiones.md).

Orden recomendado:

1. Motores X, Y, Z, E0
2. Endstops X e Y
3. Termistores (TH0 = hotend, THB = cama)
4. Calentadores (HE0 = hotend, HB = cama)
5. Ventiladores (FAN0 = hotend 2510, FAN1 = capa 4010×2)
6. CR-Touch (conector BLTouch de 5 pines)
7. Cable USB → Orange Pi Zero 3

---

### Parte 5 — Configurar Klipper

#### 5.1 Copiar el printer.cfg

Desde la Orange Pi (o directamente desde Fluidd):

```bash
# Copiar el config del proyecto al directorio de Klipper
cp /ruta/al/proyecto/firmware/klipper/config/printer.cfg ~/printer_data/config/
cp /ruta/al/proyecto/firmware/klipper/macros/macros.cfg ~/printer_data/config/
```

O subir directamente desde la interfaz web de Fluidd: **Configuration → Upload file**.

#### 5.2 Editar el serial

En `printer.cfg`, actualizar la línea `serial:` con el valor obtenido en el paso 3.3:

```ini
[mcu]
serial: /dev/serial/by-id/usb-Klipper_stm32g0b1xx_TU_SERIAL_AQUI
```

#### 5.3 Reiniciar Klipper

```bash
sudo systemctl restart klipper
```

O desde Fluidd: botón **Restart** en la esquina superior derecha.

#### 5.4 Acceder a Fluidd

Abrir en el navegador: `http://<IP_de_la_opi>`

Si Klipper arranca sin errores, aparecerá el dashboard con las temperaturas y controles de la impresora.

---

## ✅ Checklist de verificación

Completar en orden antes de hacer el primer homing:

- [ ] Fluidd accesible desde el navegador
- [ ] Klipper no muestra errores en el log (`FIRMWARE_RESTART` si aparece alguno)
- [ ] Temperatura del hotend coherente (~25 °C ambiente) en TH0
- [ ] Temperatura de la cama coherente (~25 °C ambiente) en THB
- [ ] `QUERY_ENDSTOPS` → X e Y aparecen como `open`
- [ ] Mover X +10 mm desde Fluidd → el carro se aleja del endstop
- [ ] Mover X −10 mm → el carro se acerca al endstop
- [ ] Repetir la verificación de dirección para Y y Z
  > Si un eje va al revés: **no invertir el conector físicamente**. En `printer.cfg`, añadir o quitar el `!` en el `dir_pin` del eje afectado (p. ej. `dir_pin: !PB12` → `dir_pin: PB12`) y hacer `FIRMWARE_RESTART`
- [ ] CR-Touch despliega y recoge la sonda (`BLTOUCH_DEBUG COMMAND=pin_down`)
- [ ] `G28` completo sin errores
- [ ] Ventilador hotend se activa al calentar el hotend por encima de 50 °C

---

## 🛠️ Solución de problemas

| Síntoma | Causa probable | Solución |
|---------|---------------|----------|
| Klipper muestra `Unable to connect to MCU` | Serial incorrecto o USB no reconocido | `ls /dev/serial/by-id/` y actualizar `printer.cfg` |
| Temperatura hotend muestra 0 °C o valor absurdo | Termistor en conector equivocado o desconectado | Verificar TH0; comprobar tipo de termistor en config |
| Motor X va en dirección contraria | `dir_pin` incorrecto | Añadir/quitar `!` en `dir_pin` de `stepper_x` |
| CR-Touch error al hacer homing | `z_offset` no calibrado o sonda defectuosa | Ejecutar `PROBE_CALIBRATE`; verificar conexión |
| Fluidd no carga en el navegador | Moonraker o Fluidd no arrancados | `sudo systemctl status moonraker fluidd` |
| SKR no flashea (LED no parpadea) | FAT32 incorrecto o nombre del archivo | Reformatear SD en FAT32, renombrar a `firmware.bin` exactamente |

---

## 🔗 Referencias

- [Klipper — Config Reference](https://www.klipper3d.org/Config_Reference.html)
- [Klipper — SKR Mini E3 V3 (config de ejemplo)](https://github.com/Klipper3d/klipper/blob/master/config/generic-bigtreetech-skr-mini-e3-v3.0.cfg)
- [BTT SKR Mini E3 V3 — Pinout y esquemas](https://github.com/bigtreetech/BIGTREETECH-SKR-mini-E3/tree/master/hardware/BTT%20SKR%20MINI%20E3%20V3.0)
- [KIAUH — Instalador Klipper](https://github.com/dw-0/kiauh)
- [Armbian para Orange Pi Zero 3](https://www.armbian.com/orange-pi-zero3/)
- [Fluidd](https://fluidd.xyz/) | [Mainsail](https://docs.mainsail.xyz/)
