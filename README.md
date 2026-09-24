# El flujo de una petición web

Actividad interactiva de **repaso** para que el alumnado comprenda, mediante **drag & drop**,
el flujo completo de una petición web sobre el stack **HTML → fetch → Express → MySQL**.

Está pensada para clases de desarrollo web: el alumno ordena los pasos de cada escenario,
descubre **en qué capa** ocurre cada paso y recibe retroalimentación inmediata con la
explicación de cada uno.

## Cómo funciona

1. Se elige un **escenario** (6 en total).
2. Se **arrastran las tarjetas** al hueco del paso donde creen que ocurre cada acción
   (también funciona tocando y pulsando el hueco; compatible con móvil y teclado).
3. Se pulsa **Comprobar**: las correctas se marcan en verde, las erróneas en rojo y se
   muestra la explicación de cada paso.
4. Se puede reintentar, limpiar, reiniciar o ver la solución.
5. Al superar un escenario se muestra un **diagrama del flujo** con los pasos agrupados por capa.

Cada tarjeta indica la **capa** donde ocurre el paso, codificada por color:

| Capa | Color |
|------|-------|
| Navegador (HTML, CSS y JS del cliente) | Azul |
| HTTP · fetch (la comunicación) | Verde |
| Express (servidor Node, rutas y controladores) | Naranja |
| MySQL (la base de datos) | Rojo |

## Escenarios

1. **Cargar datos (GET)** — pedir una lista al servidor.
2. **Enviar datos (POST)** — guardar un registro desde un formulario.
3. **Error 404** — recurso que no existe (`response.ok = false`).
4. **Error 500** — fallo en el servidor o en la consulta SQL.
5. **Validación 400** — datos inválidos que rechaza la validación del servidor.
6. **Sin red / servidor caído** — error de red: la promesa se **rechaza** (`.catch`).

Concepto clave que se trabaja: `fetch()` **no se rechaza** ante errores HTTP (404/400/500),
solo ante fallos de red o timeout.

## Uso

- **Sin instalación:** abre `index.html` con doble clic en cualquier navegador.
- **Moodle / Classroom:** súbelo como recurso; funciona sin servidor.
- **GitHub Pages:** despliega el repositorio y comparte la URL (ver sección siguiente).

El mejor acierto y los escenarios superados se guardan en `localStorage` del navegador.

## Despliegue en GitHub Pages

`index.html` en la raíz se sirve automáticamente, sin build ni configuración extra:

1. Sube este repositorio a GitHub.
2. En **Settings → Pages → Source**, elige *Deploy from a branch* → `main` → `/ (root)` → **Save**.
3. La URL será `https://TU_USUARIO.github.io/repaso-flujo/`.

## Estructura del repositorio

```
repaso-flujo/
├── index.html     # la actividad (autocontenida, sin dependencias)
├── profesor.md    # guía del docente: soluciones, claves y cómo repartirla
└── README.md      # este archivo
```

## Licencia

Material educativo de uso libre en el aula.