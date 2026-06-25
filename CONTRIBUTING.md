# 🤝 Cómo contribuir al proyecto UGR-A20M

Gracias por tu interés en el proyecto. Esta guía explica cómo proponer mejoras, reportar errores y contribuir documentación.

---

## Tipos de contribución bienvenidos

- 🐛 **Correcciones** — errores en la documentación, configuraciones incorrectas
- 📝 **Documentación** — mejorar guías existentes, añadir traducciones
- 🔧 **Configuraciones** — mejoras a `printer.cfg` o `macros.cfg` basadas en experiencia real
- 🖨️ **Builds alternativas** — adaptaciones del proyecto a otras impresoras similares
- 📊 **Resultados** — benchmarks, comparativas, fotos del proceso

## Lo que no se acepta

- Cambios que impliquen conversión CoreXY (fuera del alcance del proyecto)
- Configuraciones de firmware no probadas en hardware real
- Contenido sin relación con el proyecto

---

## Proceso para contribuir

### 1. Abre un Issue primero

Antes de hacer cambios, abre un [Issue](https://github.com/AlvGJ-UGR/UGR-A20M/issues) describiendo:
- Qué quieres cambiar y por qué
- Si es un bug: cómo reproducirlo

### 2. Fork y rama

```bash
git fork https://github.com/AlvGJ-UGR/UGR-A20M.git
git checkout -b feat/descripcion-corta
```

### 3. Realiza los cambios

Sigue las convenciones del proyecto:

**Commits** — formato [Conventional Commits](https://www.conventionalcommits.org/):
```
feat(firmware): add filament runout sensor macro
fix(docs): correct CR-Touch wiring pin order
docs(fase-1): add photos to extruder assembly section
```

**Documentación** — markdown con la misma estructura de los archivos existentes.

**Código Klipper** — comentarios en español, una sección por bloque funcional.

### 4. Pull Request

Abre un Pull Request describiendo:
- Qué cambia y por qué
- Si incluye cambios en `printer.cfg`: especificar en qué hardware se probó

---

## Convenciones del repositorio

### Nombres de archivo

```
docs/fase-X/NN_nombre_descriptivo.md    # documentación por fase
hardware/bom/BOM_faseX.md               # lista de materiales
photos/fase-X/YYYY-MM-DD_descripcion.jpg
```

### Tablas de materiales

Seguir el formato de `hardware/bom/BOM_fase1.md`: columnas fijas, enlace en la referencia, precio en euros.

### Configuraciones Klipper

- Comentarios en español
- Marcar con `# ← CALIBRAR` los valores que el usuario debe personalizar
- Incluir la fórmula de cálculo cuando aplique

---

## Contacto

**Autor principal:** Álvaro González Jiménez — `alvarogj1@correo.ugr.es`  
**Issues:** [github.com/AlvGJ-UGR/UGR-A20M/issues](https://github.com/AlvGJ-UGR/UGR-A20M/issues)
