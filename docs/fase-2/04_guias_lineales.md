# 🔧 Fase 2 — Guías lineales MGN12H

**Estado:** 🔜 Planificada (pendiente de completar Fase 1)

---

## 🎯 Objetivo

Sustituir las barras lisas y rodamientos lineales originales de la Geeetech A20M por **guías lineales MGN12H** en los ejes X e Y, mejorando la precisión de movimiento, reduciendo el juego y aumentando la rigidez del conjunto.

---

## ¿Por qué guías lineales?

| Característica | Barras lisas (stock) | Guías MGN12H |
|---------------|---------------------|--------------|
| Juego lateral | Alto (rodamientos holgados) | Mínimo (<0.05 mm) |
| Rigidez | Media | Alta |
| Fricción | Media | Baja (precargada) |
| Mantenimiento | Lubricación frecuente | Esporádica |
| Peso | Alto (barras + soportes) | Bajo |
| Coste | — | ~15–25 € por eje |

---

## 📐 Especificaciones de las guías

### Eje X

| Parámetro | Valor |
|-----------|-------|
| Tipo de guía | MGN12H |
| Longitud | 300 mm (A20M tiene recorrido 255 mm) |
| Carros | 1× MGN12H |
| Montaje | Sustituye a las 2 barras lisas de 8 mm del eje X |

### Eje Y

| Parámetro | Valor |
|-----------|-------|
| Tipo de guía | MGN12H |
| Longitud | 300 mm |
| Carros | 1× MGN12H por guía (2 guías en total) |
| Montaje | Sustituye a las 2 barras lisas de 8 mm del eje Y |

---

## 📦 Bill of Materials — Fase 2

> ⚠️ Pendiente de definir. Los precios y referencias se actualizarán antes de iniciar esta fase.

| # | Componente | Especificación | Enlace | Precio aprox. |
|---|------------|---------------|--------|--------------|
| 1 | Guía lineal MGN12H eje X | 300 mm + 1 carro | Por definir | ~8–12 € |
| 2 | Guía lineal MGN12H eje Y ×2 | 300 mm + 1 carro c/u | Por definir | ~16–24 € |
| 3 | Tornillería M3 montaje | M3×8, M3×10, tuercas T-nut | — | ~3 € |
| 4 | Piezas adaptadoras (impresas) | ABS/ASA | Diseño pendiente | — |
| **Total estimado** | | | | **~30–40 €** |

---

## 🖨️ Piezas a diseñar/imprimir

Para montar las guías MGN12H en el bastidor de la A20M será necesario diseñar o adaptar:

- [ ] Soporte de guía X al carro del eje X (aluminio o impreso)
- [ ] Soporte de guía Y al bastidor (×2)
- [ ] Carro X adaptado a MGN12H (para fijar el toolhead)
- [ ] Tensores de correa X e Y (si los originales no son compatibles)

> Pendiente de investigar si existen diseños en Printables/Thingiverse específicos para la Geeetech A20M.

---

## 📋 Proceso previsto

1. Desmontar el eje X actual (barras lisas, rodamientos, carro)
2. Fijar la guía MGN12H al perfil del eje X
3. Adaptar el soporte del toolhead al carro MGN12H
4. Repetir en eje Y (×2 guías)
5. Realinear y tensionar correas
6. Calibrar en Klipper (no requiere cambios en `printer.cfg` salvo ajuste de posiciones)

---

## 🔗 Referencias

- [MGN12H en AliExpress (búsqueda)](https://es.aliexpress.com/w/wholesale-mgn12h-linear-rail-300mm.html)
- [Guía de instalación MGN en Ender 3 (referencia)](https://www.printables.com/model/26523-ender-3-mgn12h-linear-rail-upgrade)
- [Comunidad Voron — uso de MGN12H](https://vorondesign.com/)
