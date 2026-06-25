# 📋 Fase 0 — Especificaciones de la Geeetech A20M original

---

## Especificaciones oficiales del fabricante

| Parámetro | Valor |
|-----------|-------|
| **Modelo** | Geeetech A20M |
| **Tipo** | FDM (Fused Deposition Modeling) |
| **Cinemática** | Cartesiana (Bowden) |
| **Volumen impresión** | 255 × 255 × 255 mm |
| **Resolución capas** | 0.1 – 0.4 mm |
| **Diámetro filamento** | 1.75 mm |
| **Materiales** | PLA, ABS, Wood, Carbon, Copper, Gradient |
| **Velocidad máx.** | 100 mm/s (fabricante) |
| **Precisión posicionamiento** | X/Y: 0.1 mm, Z: 0.0025 mm |
| **Temperatura hotend** | ≤ 250 °C |
| **Temperatura cama** | ≤ 100 °C |
| **Fuente alimentación** | 24V DC, 15A (360W) |
| **Conectividad** | SD Card, USB |
| **Dimensiones máquina** | 487 × 465 × 516 mm |
| **Peso** | ~9 kg |

## Electrónica original

| Componente | Especificación |
|------------|---------------|
| **Placa controladora** | Geeetech GT2560 v3 (8-bit, ATmega2560) |
| **Drivers motores** | A4988 integrados |
| **Firmware** | Marlin 1.x personalizado Geeetech |
| **Pantalla** | LCD 12864 con encoder |
| **Hotend** | Dual mixing (2 entradas, 1 salida) |
| **Ventilación** | 1× 40mm hotend, 1× 40mm capa |

## Problemas conocidos de la máquina base

- Drivers A4988 ruidosos y poco eficientes (vs TMC2209)
- Placa 8-bit: velocidades de procesamiento limitadas para Klipper
- Sistema Bowden: stringing elevado, sin soporte para flexibles
- Sin nivelación automática de serie
- Firmware cerrado, difícil de modificar
- Conector hotend propenso a fallos

## Estado inicial del proyecto

> Pendiente: añadir fotografías del estado inicial en `photos/estado-inicial/`

- [ ] Foto frontal de la máquina
- [ ] Foto de la placa GT2560
- [ ] Foto del hotend y extrusor Bowden original
- [ ] Foto de la pantalla y controles
- [ ] Prueba de impresión inicial (benchmarking)
