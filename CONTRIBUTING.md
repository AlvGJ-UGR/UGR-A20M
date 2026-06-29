# 🤝 Cómo contribuir al proyecto UGR-A20M

Gracias por tu interés en el proyecto. Esta guía explica cómo proponer mejoras, reportar errores y contribuir documentación o configuraciones.

---

## Tipos de contribución bienvenidos

| Tipo | Ejemplos |
|------|---------|
| 🐛 **Correcciones** | Errores en documentación, valores incorrectos en `printer.cfg`, links rotos |
| 📝 **Documentación** | Mejorar guías existentes, añadir capturas, completar checklists con experiencia real |
| 🔧 **Configuraciones** | Mejoras a `printer.cfg` o `macros.cfg` probadas en hardware real |
| 📸 **Fotografías** | Fotos del proceso de montaje, antes/después, benchmarks |
| 🖨️ **Builds alternativas** | Adaptaciones del proyecto a impresoras similares (Ender 3, CR-10...) |
| 📊 **Resultados** | Benchmarks, comparativas de materiales, mediciones |

## Lo que no se acepta

- Conversión CoreXY — fuera del alcance del proyecto
- Configuraciones de firmware no probadas en hardware real
- Contenido sin relación con impresión 3D o el proyecto

---

## Flujo de trabajo paso a paso

### 1. Abre un Issue primero

Antes de escribir código o documentación, abre un [Issue](https://github.com/AlvGJ-UGR/UGR-A20M/issues/new/choose) describiendo qué quieres cambiar y por qué. Esto evita trabajo duplicado y permite alinear expectativas.

### 2. Haz fork del repositorio

Desde la web de GitHub, pulsar el botón **Fork** en la esquina superior derecha del repositorio. Esto crea una copia en tu cuenta.

### 3. Clona tu fork y crea una rama

```bash
# Clonar tu fork (sustituir TU_USUARIO por tu nombre de GitHub)
git clone https://github.com/TU_USUARIO/UGR-A20M.git
cd UGR-A20M

# Añadir el repositorio original como remote "upstream"
git remote add upstream https://github.com/AlvGJ-UGR/UGR-A20M.git

# Crear una rama descriptiva para tu cambio
git checkout -b fix/corregir-offset-crtouch
# o
git checkout -b feat/anadir-perfil-petg-slicer
# o
git checkout -b docs/completar-fase2-guias
```

### 4. Realiza los cambios

Edita los archivos necesarios siguiendo las [convenciones del proyecto](#convenciones-del-repositorio).

### 5. Verifica antes de hacer commit

```bash
# Ver qué archivos has modificado
git status

# Ver el diff de tus cambios
git diff

# Verificar que los links markdown no están rotos (requiere markdown-link-check)
# npx markdown-link-check docs/guia_calibracion.md
```

### 6. Haz commit con mensaje descriptivo

Seguimos el estándar [Conventional Commits](https://www.conventionalcommits.org/):

```bash
# Formato: tipo(ámbito): descripción en imperativo
git add docs/guia_calibracion.md
git commit -m "fix(docs): corregir orden pasos 6 y 7 en guía de calibración"
```

**Tipos de commit válidos:**

| Tipo | Cuándo usarlo |
|------|--------------|
| `feat` | Nueva funcionalidad o documento |
| `fix` | Corrección de error |
| `docs` | Solo documentación |
| `refactor` | Reorganización sin cambio de contenido |
| `chore` | Tareas de mantenimiento (gitignore, deps...) |

**Ejemplos correctos:**
```
feat(firmware): add NOZZLE_CHANGE macro with temperature warning
fix(docs): correct CR-Touch wiring pin order in esquema_conexiones
docs(fase-1): add assembly photos for Sharkfin extruder
fix(printer.cfg): set correct gear_ratio for BMG clone (50:17)
docs(bom): update AliExpress links for 2025 pricing
```

### 7. Sincroniza con el repositorio original

Antes de hacer push, asegúrate de que tu rama está actualizada:

```bash
git fetch upstream
git rebase upstream/main
```

Si hay conflictos, resolverlos manualmente y continuar:

```bash
git rebase --continue
```

### 8. Push y Pull Request

```bash
git push origin fix/corregir-offset-crtouch
```

Ve a GitHub, abre un **Pull Request** desde tu fork hacia `AlvGJ-UGR/UGR-A20M:main`. El template de PR ([`.github/pull_request_template.md`](.github/pull_request_template.md)) se cargará automáticamente — rellenarlo completamente.

---

## Convenciones del repositorio

### Nombres de archivo

```
docs/fase-X/NN_nombre_descriptivo.md       # documentación por fase
hardware/bom/BOM_faseX.md                  # lista de materiales
photos/fase-X/YYYY-MM-DD_descripcion.jpg   # fotografías
```

### Markdown

- Usar las mismas cabeceras (`##`, `###`) que los archivos existentes
- Tablas con cabecera separada por `|---|`
- Bloques de código con triple backtick y el lenguaje especificado (` ```ini `, ` ```bash `, ` ```gcode `)
- Emojis en títulos de sección para consistencia visual

### Tablas de BOM

Seguir el formato de [`hardware/bom/BOM_fase1.md`](hardware/bom/BOM_fase1.md): columnas fijas (Componente · Especificación · Enlace · Precio), enlace en la celda de compra, precio en euros con tilde (~).

### Configuraciones Klipper

- Comentarios en español
- Marcar con `# ← CALIBRAR` los valores que el usuario debe personalizar
- Incluir la fórmula de cálculo cuando aplique (p. ej. `rotation_distance`)
- Una sección por bloque funcional con separador `# ---`

### Fotografías

- Formato: JPG, mínimo 1920×1080 px
- Nombre: `YYYY-MM-DD_descripcion-breve.jpg`
- Fondo neutro, buena iluminación
- Ver checklist completo en [`photos/README.md`](photos/README.md)

---

## Política de revisión

- Este es un **proyecto personal** mantenido por un único autor — los PRs se revisan cuando hay tiempo disponible, sin SLA formal
- Los PRs que modifiquen `printer.cfg` o `macros.cfg` deben especificar el hardware en que se probaron, incluyendo versión de Klipper
- Las fotografías aportadas deben ser originales del contribuidor y estar bajo licencia CC BY-SA 4.0
- Si un PR lleva más de 2 semanas sin respuesta, mencionar al autor en un comentario del issue original

---

## Contacto

**Autor principal:** Álvaro González Jiménez — `alvarogj1@correo.ugr.es`  
**Issues:** [github.com/AlvGJ-UGR/UGR-A20M/issues](https://github.com/AlvGJ-UGR/UGR-A20M/issues)  
**Universidad de Granada:** [ugr.es](https://www.ugr.es)
