# Consideraciones generales

1. el framework a utilizar es python django
2. utiliza comando como django admin startapp para crear apps, en lo posible no crees manualmente las carpetas de la app
3. utiliza la estrategìa de templates y extends para el diseño de las paginas, se puede usar javascript, pero cada vez que algo sea posible hacerlo con el framework y con python, trabaja en python, que el javascript se limite a temas de front y usabailidad de paginas.
4. el proyecto se trabajara con una base de datos sqlite3 en el entorno de sesarrollo, en el archivo settings.py se configurara la conexion a la base de datos.
5. cada vez que te pida hacer algo, revisa la petición, analisala y si tienes dudas, pregunta, no empieces cn el codigo hasta no estar seguros.
6. el proyecto se trabajara con un sistema de autenticación, se usara el modulo de autenticación de django, se creara un usuario admin y se usara para acceder al proyecto.
7. el usuario admin será user: admin y password: adminadmin
8. el proyecto se trabajara con un sistema de roles, se usara el modulo de roles de django, se crearan los roles necesarios para el proyecto.
9. para la hoja de estilos del proyecto, ve construyendo un archivo styles.css, no creemos dependencia de bootsrap, usemos solo css puro.
10. el diseño de la pagina debe considerar un menu izquierdo tipo hamurguesa, que cuando este desplegado muestre iconos y texto de opciones, y si esta comprimido solo debe mostrar los iconos.


# Estrategia Recomendada de Carpetas para Archivos estáticos en Proyectos Django de Gran tamaño

Para sistemas Django de gran escala, la organización de archivos estáticos (CSS, JavaScript, imágenes) es crucial para mantener un código mantenible, escalable y organizado. La estrategia recomendada combina organización por aplicación con archivos globales cuando es necesario.

## Estructura de Directorios Recomendada

Para proyectos grandes, la arquitectura óptima incluye tanto archivos estáticos especá­ficos de aplicación como archivos globales del proyecto:

```
mi_proyecto/
|
|-------- manage.py
|-------- requirements.txt
|
|-------- config/                         # Configuración del proyecto
|   |-------- __init__.py
|   |-------- settings/
|   |   |-------- base.py
|   |   |-------- development.py
|   |   |-------- production.py
|   |-------- urls.py
|   |-------- wsgi.py
|
|-------- apps/                            # Todas las aplicaciones Django
|   |-------- usuarios/
|   |   |-------- static/
|   |   |   |-------- usuarios/            # Namespacing obligatorio
|   |   |       |-------- css/
|   |   |       |   |-------- usuarios.css
|   |   |       |-------- js/
|   |   |       |   |-------- usuarios.js
|   |   |       |-------- images/
|   |   |           |-------- logo-usuarios.png
|   |   |-------- templates/
|   |   |-------- models.py
|   |   |-------- views.py
|   |
|   |-------- productos/
|   |   |-------- static/
|   |   |   |-------- productos/          # Namespacing obligatorio
|   |   |       |-------- css/
|   |   |       |-------- js/
|   |   |       |-------- images/
|   |   |-------- ...
|   |
|   |-------- ordenes/
|       |-------- static/
|       |   |-------- ordenes/            # Namespacing obligatorio
|       |       |-------- css/
|       |       |-------- js/
|       |       |-------- images/
|       |-------- ...
|
|-------- static/                          # Archivos estáticos globales
|   |-------- css/
|   |   |-------- base.css
|   |   |-------- theme.css
|   |-------- js/
|   |   |-------- main.js
|   |   |-------- utils.js
|   |-------- images/
|   |   |-------- logo.png
|   |   |-------- favicon.ico
|   |-------- vendor/                      # Bibliotecas externas
|   |   |-------- bootstrap/
|   |   |-------- jquery/
|   |   |-------- fontawesome/
|   |-------- dist/                        # Archivos compilados (si usas Webpack/Gulp)
|       |-------- bundle.js
|       |-------- bundle.css
|
|-------- staticfiles/                     # Directorio de recolección (producción)
|
|-------- templates/                       # Templates globales
|   |-------- base.html
|
|-------- media/                          # Archivos subidos por usuarios
    |-------- uploads/
```

## Principios Fundamentales

### 1. Namespacing Obligatorio para Archivos Especá­ficos de Aplicaciones

Django buscará¡ el primer archivo estático que coincida con el nombre. Si tienes `usuarios/static/style.css` y `productos/static/style.css`, Django solo encontrará¡ el primero. La solución es crear un subdirectorio adicional con el nombre de la aplicación:

```
usuarios/
    static/
        usuarios/              # Subdirectorio adicional
            css/
            js/
            images/
```

Luego, en tus templates:

```django
{% load static %}
<link rel="stylesheet" href="{% static 'usuarios/css/usuarios.css' %}">
<script src="{% static 'usuarios/js/usuarios.js' %}"></script>
```

### 2. Separación de Archivos Globales y Especá­ficos de aplicación

- **Archivos especá­ficos de aplicación**: CSS, JS e imágenes que solo usa una aplicación especá­fica deben estar en `app/static/app/`
- **Archivos globales**: Estilos base, JavaScript compartido, assets del tema, librerá­as de terceros van en el directorio `static/` del proyecto

### 3. Organización de Archivos Compilados y Procesados

Para proyectos grandes que usan herramientas de construcción (Webpack, Gulp, etc.):

```
static/
    src/              # Archivos fuente (SCSS, TypeScript, etc.)
        scss/
        ts/
    dist/             # Archivos compilados y minificados
        css/
        js/
    public/           # Assets que no requieren procesamiento
        images/
        fonts/
```

## Configuración en settings.py

Para proyectos de gran tamaño, tu configuración debe incluir:

```python
# settings/base.py
import os
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent.parent

# URL para servir archivos estáticos
STATIC_URL = '/static/'

# Directorios adicionales donde buscar archivos estáticos
STATICFILES_DIRS = [
    BASE_DIR / 'static',              # Archivos globales del proyecto
    # No necesitas listar apps individuales aquá­,
    # AppDirectoriesFinder las encuentra automáticamente
]

# Directorio donde collectstatic recopila todos los archivos
STATIC_ROOT = BASE_DIR / 'staticfiles'

# Configuración de almacenamiento
STORAGES = {
    "staticfiles": {
        "BACKEND": "django.contrib.staticfiles.storage.ManifestStaticFilesStorage",
    },
}

# Finders (configuración predeterminada, no necesitas cambiarla)
STATICFILES_FINDERS = [
    'django.contrib.staticfiles.finders.FileSystemFinder',
    'django.contrib.staticfiles.finders.AppDirectoriesFinder',
]
```

## Mejores Prá¡cticas para Proyectos Grandes

### 1. Usa Herramientas de Build Frontend

Para proyectos empresariales, integra herramientas modernas:

- **Webpack**: Para bundling, minificación, code splitting
- **Gulp**: Para automatización de tareas (compilación SASS, optimización de imágenes)
- **django-webpack-loader**: Para integrar Webpack con Django

### 2. Organización por Tipo vs por Funcionalidad

Hay dos enfoques vá¡lidos:

**Por tipo** (recomendado para proyectos medianos):
```
static/
    css/
        usuarios.css
        productos.css
    js/
        usuarios.js
        productos.js
```

**Por funcionalidad** (recomendado para proyectos grandes):
```
static/
    usuarios/
        css/
        js/
    productos/
        css/
        js/
```

### 3. Versionado y Cache Busting

Usa `ManifestStaticFilesStorage` para agregar hashes a los nombres de archivos:

```python
STORAGES = {
    "staticfiles": {
        "BACKEND": "django.contrib.staticfiles.storage.ManifestStaticFilesStorage",
    },
}
```

Esto convierte `main.css` en `main.133742.css`, facilitando la invalidación de caché.

### 4. Separación de Entornos

Divide tu configuración de archivos estáticos segáºn el entorno:

**Desarrollo:**
- Usa `DEBUG=True` para servir archivos automáticamente
- Archivos sin minificar con sourcemaps

**Producción:**
- Ejecuta `python manage.py collectstatic`
- Sirve archivos estáticos con Nginx/Apache o CDN
- Archivos minificados y comprimidos

## Flujo de Trabajo Recomendado

**Desarrollo:**
1. Coloca archivos estáticos en `app/static/app/` o `static/`
2. Usa `{% load static %}` y `{% static %}` en templates
3. Django sirve automáticamente con `runserver`

**Despliegue:**
1. Ejecuta `python manage.py collectstatic`
2. Configura Nginx/Apache para servir `/staticfiles/`
3. Implementa caché headers apropiados
4. Opcionalmente, sube a CDN

## Recomendaciones Adicionales para Sistemas Grandes

### Modularidad y Reutilización

- Agrupa aplicaciones relacionadas en subdirectorios dentro de `apps/`
- Mantén archivos estáticos autocontenidos en cada app para facilitar reutilización
- Documenta dependencias entre apps

### Performance

- Minifica CSS/JS en producción
- Optimiza imágenes automáticamente
- Implementa lazy loading para assets grandes
- Usa HTTP/2 para multiplexing

### Mantenibilidad

- Establece convenciones de nombres claras
- Documenta la estructura en el README
- Usa linters (ESLint, Stylelint) para consistencia
- Implementa revisiones de código para archivos estáticos

## Conclusión

Esta estrategia te permitirá mantener un proyecto Django de gran tamaño organizado, escalable y fá¡cil de mantener, aprovechando las capacidades nativas de Django mientras incorporas herramientas modernas del ecosistema frontend segáºn sea necesario.