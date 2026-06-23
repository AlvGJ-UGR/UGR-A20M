# ⚡ Fase 1 — Actualización Electrónica

**SKR Mini E3 V3.0 + Orange Pi Zero 3 + Klipper**

---

## 🎯 Objetivo

Sustituir la placa original **GT2560 v3 de 8 bits** y el firmware Marlin por:
- **BTT SKR Mini E3 V3.0** (32-bit, TMC2209 integrados)
- **Orange Pi Zero 3** (1 GB) como ordenador anfitrión
- **Klipper** como firmware principal
- **Fluidd** o **Mainsail** como interfaz web

---

## 🔧 Componentes necesarios

| Componente | Referencia | Precio |
|------------|------------|--------|
| BTT SKR Mini E3 V3.0 | [AliExpress](https://es.aliexpress.com/item/1005007912548824.html) | ~25 € |
| Orange Pi Zero 3 (1 GB) | [AliExpress](https://es.aliexpress.com/item/1005006047845950.html) | ~25 € |
| MicroSD SanDisk (32 GB+) | [Amazon](https://www.amazon.es/SanDisk-Tarjeta-microSDXC-Adaptador-Rendimiento/dp/B0B7NXBM6P) | ~8 € |

---

## 📋 Proceso de instalación

### 1. Preparar la Orange Pi Zero 3

1. Descargar **Armbian** para Orange Pi Zero 3:  
   [https://www.armbian.com/orange-pi-zero3/](https://www.armbian.com/orange-pi-zero3/)

2. Grabar imagen en la microSD con **Balena Etcher** o `dd`

3. Primer arranque: conectar por SSH  
   ```
   ssh root@<IP_de_la_opi>
   ```

4. Instalar **KIAUH** (instalador de Klipper):
   ```bash
   git clone https://github.com/dw-0/kiauh.git
   cd kiauh && ./kiauh.sh
   ```

5. Desde KIAUH instalar en orden:
   - Klipper
   - Moonraker
   - Fluidd (o Mainsail)

### 2. Compilar Klipper para SKR Mini E3 V3

```bash
cd ~/klipper
make menuconfig
```

Configuración para SKR Mini E3 V3.0:
- **Micro-controller:** STM32
- **Processor model:** STM32G0B1
- **Bootloader offset:** 8KiB
- **Communication:** USB (on PA11/PA12)

```bash
make
```

El archivo generado es `out/klipper.bin`. Renombrarlo a `firmware.bin` y copiarlo a la microSD de la SKR.

### 3. Instalar la SKR Mini E3 V3.0

> ⚠️ **IMPORTANTE: Desconectar la impresora de la corriente antes de cualquier manipulación eléctrica.**

1. Retirar la placa GT2560 original
2. Conectar motores en los mismos puertos (X, Y, Z, E0)
3. Conectar termistores (hotend → TH0, cama → THB)
4. Conectar calentadores (hotend → HE0, cama → HB)
5. Conectar ventiladores (hotend → FAN0, capa → FAN1)
6. Conectar endstops (X → X-STOP, Y → Y-STOP)
7. Conectar CR-Touch (ver sección siguiente)
8. Conectar Orange Pi por USB

### 4. Conexión CR-Touch

El CR-Touch se conecta a los pines dedicados de la SKR Mini E3 V3:

| Pin CR-Touch | Cable | Conector SKR |
|-------------|-------|-------------|
| GND | Negro | BLTouch GND |
| +5V | Rojo | BLTouch 5V |
| Signal (servo) | Amarillo | BLTouch SERVO |
| Sensor | Blanco | BLTouch SENSOR |

### 5. Configurar printer.cfg

Copiar el archivo `firmware/klipper/config/printer.cfg` a la Orange Pi:
```
~/printer_data/config/printer.cfg
```

**Ajustes críticos a personalizar:**
- `serial:` — buscar con `ls /dev/serial/by-id/`
- `x_offset`, `y_offset` del CR-Touch — medir físicamente
- `rotation_distance` del extrusor — calibrar tras instalación

---

## ✅ Verificación de funcionamiento

Tras instalar, verificar en orden desde la interfaz Fluidd/Mainsail:

- [ ] Temperatura del hotend y cama se leen correctamente
- [ ] Motores X, Y, Z responden en la dirección correcta
- [ ] Endstops X e Y funcionan (comprobar con `QUERY_ENDSTOPS`)
- [ ] CR-Touch despliega y recoge la sonda
- [ ] Homing completo funciona (`G28`)
- [ ] Mesh de nivelación se genera correctamente (`BED_MESH_CALIBRATE`)

---

## 🔗 Referencias

- [Documentación oficial Klipper](https://www.klipper3d.org/Config_Reference.html)
- [SKR Mini E3 V3 Pinout](https://github.com/bigtreetech/BIGTREETECH-SKR-mini-E3)
- [KIAUH Installer](https://github.com/dw-0/kiauh)
- [Fluidd](https://fluidd.xyz/) | [Mainsail](https://docs.mainsail.xyz/)
