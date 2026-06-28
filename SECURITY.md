# Política de seguridad — UGR-A20M

## ⚠️ Advertencias de seguridad eléctrica y física

Este proyecto implica manipulación de electrónica de 24V DC y componentes a alta temperatura. Antes de seguir cualquier guía de este repositorio, leer detenidamente:

### Electricidad
- **Desconectar siempre** la impresora de la red eléctrica antes de manipular la electrónica, cables o conectores.
- La fuente de alimentación trabaja a **24V DC** y la cama caliente puede llegar a **200W**. Un cortocircuito puede dañar la placa o iniciar un incendio.
- Verificar la polaridad de todos los conectores antes de alimentar el sistema.
- No trabajar con la impresora encendida salvo cuando sea estrictamente necesario (como al verificar la dirección de los motores desde Fluidd).

### Temperatura
- El hotend CHC V6 Volcano puede alcanzar **285 °C**. No tocar nunca el bloque calefactor, el termistor ni la boquilla cuando la impresora esté caliente.
- La cama caliente puede alcanzar **120 °C**. Esperar a que enfríe por debajo de **40 °C** antes de retirar piezas o manipular la superficie.
- Las piezas impresas en **ABS/ASA** pueden deformarse si se exponen a calor excesivo durante la impresión o postprocesado.

### Mecánica
- Los motores NEMA 17 pueden moverse inesperadamente si Klipper está activo. Mantener las manos alejadas del área de movimiento al operar la impresora remotamente.
- Las guías lineales MGN12H (Fase 2) tienen aristas vivas. Manipularlas con cuidado.

---

## 🔒 Reportar vulnerabilidades de seguridad en el software

Este repositorio contiene configuraciones de Klipper y scripts bash. Si detectas un problema de seguridad en el código (por ejemplo, un script con permisos incorrectos o una configuración que expone la impresora en red), por favor:

1. **No abrir un Issue público** con detalles del problema.
2. Enviar un correo directamente al autor: **alvarogj1@correo.ugr.es**
3. Incluir: descripción del problema, pasos para reproducirlo y impacto potencial.

Se responderá lo antes posible — este es un proyecto personal sin SLA formal.

---

## 🌐 Seguridad de la red

Fluidd/Mainsail expone la impresora en la red local sin autenticación por defecto. Recomendaciones:

- **No exponer Fluidd directamente a Internet** sin autenticación adicional (VPN o reverse proxy con contraseña).
- Usar una red WiFi dedicada para la impresora o aislarla en una VLAN si es posible.
- Actualizar Klipper y Moonraker regularmente:
  ```bash
  cd ~/kiauh && ./kiauh.sh
  # Opción: Update
  ```

---

## Configuración de software probada

| Componente | Versión probada |
|------------|----------------|
| Klipper | ≥ 0.11 |
| Moonraker | ≥ 0.8 |
| Fluidd | ≥ 1.28 |
| Armbian (Orange Pi Zero 3) | Bookworm 24.x |
| BTT SKR Mini E3 V3 | Klipper compilado |
