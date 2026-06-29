# Marlin — Referencia histórica

Esta carpeta está reservada para guardar la **configuración original de Marlin** de la Geeetech A20M con placa GT2560 v3, como referencia histórica del punto de partida del proyecto.

**La impresora actualmente corre Klipper.** Los archivos de esta carpeta no se usan activamente.

---

## Por qué conservar la configuración de Marlin

- Referencia para comparar valores de calibración (pasos/mm, PID, offsets)
- Punto de retorno si fuera necesario revertir a la configuración original
- Documentación del estado inicial para la memoria del proyecto

---

## Cómo obtener la configuración Marlin original

Si no se guardó la configuración antes de flashear Klipper, se puede recuperar desde:

1. **Repositorio oficial Geeetech:**  
   [github.com/Geeetech3D/Marlin](https://github.com/Geeetech3D/Marlin) — buscar la rama correspondiente a la A20M

2. **Foro Geeetech:**  
   [forum.geeetech.com](https://forum.geeetech.com) — sección Geeetech A20M

3. **Valores de referencia del Marlin stock (A20M):**

| Parámetro | Valor original |
|-----------|---------------|
| X steps/mm | 80 |
| Y steps/mm | 80 |
| Z steps/mm | 400 |
| E steps/mm | 96 (extrusor Bowden original — **no usar para el Sharkfin**, calibrar `rotation_distance` desde cero) |
| PID hotend Kp | 22.20 |
| PID hotend Ki | 1.08 |
| PID hotend Kd | 114.00 |
| PID cama Kp | 54.00 |
| PID cama Ki | 0.77 |
| PID cama Kd | 950.00 |
| Velocidad homing | 50 mm/s |
| Retracción | 6 mm a 45 mm/s |

> Estos valores son de referencia. Los valores reales de Klipper se calibran independientemente y se guardan en el bloque `SAVE_CONFIG` de `printer.cfg`.
