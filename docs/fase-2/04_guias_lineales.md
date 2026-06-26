# 🔧 Fase 2 — Guías lineales MGN12H en X e Y

**Estado:** 🔜 Planificada — iniciar tras completar y validar la Fase 1

---

## 🎯 Objetivo

Sustituir las **barras lisas de 8 mm** y los rodamientos lineales LM8UU originales de la Geeetech A20M por **guías lineales MGN12H** en los ejes X e Y. El resultado es una cinemática más rígida, con menos juego y mejor comportamiento a alta velocidad.

---

## ¿Por qué guías lineales?

Las barras lisas de la A20M presentan dos limitaciones principales: el juego lateral de los rodamientos LM8UU aumenta con el uso, y el eje X lleva dos barras paralelas que añaden peso al conjunto móvil. Las guías MGN12H resuelven ambos problemas.

| Característica | Barras lisas LM8UU (stock) | Guías MGN12H |
|---------------|---------------------------|--------------|
| Juego lateral | 0.1–0.3 mm (aumenta con uso) | < 0.05 mm |
| Rigidez torsional | Baja — 2 barras paralelas necesarias | Alta — 1 guía es suficiente en X |
| Fricción | Variable (lubricación irregular) | Baja y consistente (bolas recirculantes) |
| Peso del eje X | ~800 g (2 barras + carro + soportes) | ~250 g (1 guía + carro MGN12H) |
| Mantenimiento | Lubricación cada 50–100 h | Cada 200–300 h |
| Vida útil | 1.000–2.000 h | > 10.000 h |
| Coste de reemplazo | Bajo | Medio |

---

## 📐 Configuración elegida

### Eje X — 1× MGN12H

Se sustituyen las 2 barras lisas de 8 mm por **una única guía MGN12H de 300 mm**, montada centralmente en el perfil del eje X. El toolhead (Mini Stealth v2) se fija directamente al carro MGN12H mediante un adaptador impreso.

| Parámetro | Valor |
|-----------|-------|
| Tipo de guía | MGN12H (carro H = ancho, mayor superficie de contacto) |
| Longitud | 300 mm |
| Carros | 1× |
| Posición de montaje | Centro del perfil de aluminio del eje X |

### Eje Y — 2× MGN12H

Se sustituyen las 2 barras lisas de 8 mm del eje Y por **dos guías MGN12H de 300 mm**, una a cada lado de la cama. La cama se apoya en los dos carros mediante soportes impresos o de aluminio.

| Parámetro | Valor |
|-----------|-------|
| Tipo de guía | MGN12H |
| Longitud | 300 mm |
| Carros | 1× por guía (2 en total) |
| Posición de montaje | Lateral izquierdo y derecho del bastidor Y |

---

## 📦 Bill of Materials — Fase 2

| # | Componente | Especificación | Enlace | Precio aprox. |
|---|------------|---------------|--------|--------------|
| 1 | Guía MGN12H eje X | 300 mm + 1 carro MGN12H | [AliExpress](https://es.aliexpress.com/w/wholesale-mgn12h-linear-rail-300mm.html) | ~8–12 € |
| 2 | Guía MGN12H eje Y ×2 | 300 mm + 1 carro MGN12H c/u | [AliExpress](https://es.aliexpress.com/w/wholesale-mgn12h-linear-rail-300mm.html) | ~16–24 € |
| 3 | Tornillos M3×8 BHCS | ×20 (montaje guías al perfil) | [AliExpress](https://es.aliexpress.com/item/4000026671295.html) | ~1 € |
| 4 | Tuercas T-nut M3 | ×20 (para perfil de aluminio) | [AliExpress](https://es.aliexpress.com/item/4000232925592.html) | ~2 € |
| 5 | Adaptador carro X → toolhead (impreso) | ABS/ASA | Diseño pendiente / Printables | — |
| 6 | Soportes cama → carro Y ×2 (impresos) | ABS/ASA | Diseño pendiente / Printables | — |
| 7 | Grasa de litio (lubricación guías) | Cualquier grasa de litio blanca | [Amazon](https://www.amazon.es/s?k=grasa+litio+blanca) | ~5 € |
| **Total estimado** | | | | **~35–50 €** |

> ⚠️ Investigar en [Printables](https://www.printables.com) y [Thingiverse](https://www.thingiverse.com) si existen adaptadores específicos para la Geeetech A20M antes de diseñar desde cero. Impresoras de tamaño similar (Ender 3, CR-10) tienen muchos diseños adaptables.

---

## 🖨️ Piezas a imprimir

| Pieza | Función | Material | Notas |
|-------|---------|----------|-------|
| Adaptador carro X → Mini Stealth | Conecta el carro MGN12H con el toolhead | ABS/ASA | Debe alinear el nozzle con la posición original |
| Soporte cama izquierdo | Fija la cama al carro Y izquierdo | ABS/ASA | Verificar altura respecto a la cama |
| Soporte cama derecho | Fija la cama al carro Y derecho | ABS/ASA | Debe ser simétrico al izquierdo |
| Tensor de correa X (si necesario) | Mantiene la correa tensa tras el cambio de carro | ABS/ASA | Puede reutilizarse el original |

> Ver parámetros de impresión en [`hardware/prints/README.md`](../../hardware/prints/README.md).

---

## 🔨 Proceso de instalación previsto

### Preparación

1. Completar y validar la Fase 1 al 100% — la Fase 2 modifica el carro X que ya lleva el toolhead
2. Imprimir todos los adaptadores antes de desmontar nada
3. Fotografiar el estado actual del eje X e Y antes de empezar

### Eje X

1. Retirar el toolhead (Mini Stealth completo) del carro X actual
2. Desmontar el carro X, los rodamientos LM8UU y las barras lisas de 8 mm
3. Limpiar el perfil de aluminio del eje X
4. Montar la guía MGN12H centrada en el perfil con tornillos M3×8 + T-nut
5. **Verificar la alineación:** la guía debe ser perfectamente paralela al perfil — usar un nivel o indicador de cuadrante
6. Lubricar el carro MGN12H con grasa de litio (una pequeña cantidad en las bolas)
7. Instalar el adaptador de toolhead en el carro MGN12H
8. Remontar el Mini Stealth v2 en el adaptador
9. Verificar que la correa GT2 sigue bien tensa y alineada

### Eje Y

1. Retirar la cama caliente (desconectar el cable del calentador y el termistor)
2. Desmontar los soportes de la cama, los rodamientos LM8UU y las barras lisas de 8 mm
3. Limpiar el bastidor Y
4. Montar las dos guías MGN12H, una a cada lado, con tornillos M3×8 + T-nut
5. **Alineación crítica:** las dos guías deben ser perfectamente paralelas entre sí — medir con calibre en varios puntos
6. Lubricar ambos carros
7. Instalar los soportes de cama impresos en los carros
8. Remontar la cama caliente sobre los soportes
9. Verificar la nivelación de la cama antes de continuar

### Calibración post-instalación

Tras instalar las guías no se requieren cambios en `printer.cfg`, pero sí recalibrar:

- [ ] `SCREWS_TILT_CALCULATE` — la nueva cama puede estar en posición ligeramente diferente
- [ ] `PROBE_CALIBRATE` — el z_offset puede haber cambiado levemente
- [ ] `BED_MESH_CALIBRATE` — generar un nuevo mesh con la geometría actualizada
- [ ] Verificar tensión de correas X e Y — las guías MGN12H tienen menos fricción y pueden requerir menos tensión

---

## ⚠️ Puntos críticos

**Alineación de las guías MGN12H en Y:** si las dos guías no son perfectamente paralelas, la cama sufrirá tensión torsional que se manifestará como ruido, desgaste prematuro de los carros y variación en las capas. Tomarse el tiempo necesario para alinear bien antes de apretar los tornillos definitivamente.

**Calidad de las guías:** las guías MGN12H baratas de AliExpress tienen calidades muy variables. Buscar vendedores con buenas valoraciones y pedir guías con preload **Z0** (sin precarga) o **Z1** (precarga leve) — las Z2 son demasiado rígidas para esta aplicación.

**Lubricación:** usar grasa de litio blanca, no aceite. El aceite se evapora con el calor y atrae polvo. Lubricar al instalar y cada ~200 horas de uso.

---

## 📊 Mejoras esperadas tras Fase 2

| Métrica | Fase 1 (barras lisas) | Fase 2 (MGN12H) |
|---------|----------------------|-----------------|
| Juego en X | ~0.1–0.2 mm | < 0.05 mm |
| Juego en Y | ~0.1–0.2 mm | < 0.05 mm |
| Velocidad máxima estable | ~150 mm/s | ~200–250 mm/s |
| Ruido en operación | Medio | Bajo |
| Ringing visible | Moderado | Mínimo |
| Peso eje X | ~800 g | ~250 g |

---

## 🔗 Referencias

- [MGN12H en AliExpress — búsqueda 300mm](https://es.aliexpress.com/w/wholesale-mgn12h-linear-rail-300mm.html)
- [Adaptador MGN12H para Ender 3 (referencia adaptable)](https://www.printables.com/model/26523)
- [Guía de alineación de guías lineales — Voron Documentation](https://docs.vorondesign.com/build/mechanical/)
- [Grasa de litio recomendada para guías lineales](https://www.amazon.es/s?k=grasa+litio+blanca+super+lube)
