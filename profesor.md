# El flujo de una petición web — Guía para el profesor

**Tipo:** Actividad de repaso interactiva (drag & drop)
**Duración estimada en clase:** 15–30 min
**Nivel:** Básico–Intermedio
**Recurso:** `index.html` (autocontenido, sin dependencias, funciona offline)

---

## 🎯 Objetivo pedagógico

Que el alumnado interiorice el **modelo mental del flujo de una petición web** sobre su stack real:
**HTML → fetch → Express → MySQL**, distinguiendo en qué capa ocurre cada paso y en qué orden.

Al terminar, el alumno debe ser capaz de:
- Explicar qué ocurre desde que pulsa un botón hasta que se actualiza la pantalla.
- Distinguir las capas: Navegador, HTTP/fetch, Express y MySQL.
- Entender la diferencia entre:
  - Un error **HTTP** (404, 400, 500): hay respuesta, `response.ok = false`.
  - Un error **de red**: no hay respuesta, la promesa se rechaza directamente (`.catch`).

---

## 📋 Cómo funciona la actividad

1. Hay **6 escenarios** (pestañas): GET, POST, 404, 500, validación 400 y sin red.
2. En cada uno hay tarjetas desordenadas. Cada tarjeta indica la **capa** donde ocurre el paso
   (color + etiqueta): Navegador, HTTP·fetch, Express, MySQL.
3. El alumno **arrastra cada tarjeta** a su posición en el flujo (o la toca y pulsa el hueco;
   funciona en móvil y con teclado).
4. Pulsa **Comprobar**: las correctas se ponen en verde, las erróneas en rojo, y se muestra la
   explicación de cada paso ("¿por qué va aquí?").
5. Puede **reintentar** (cuenta aciertos e intentos), **limpiar**, **reiniciar** o **ver la
   solución**.
6. El mejor resultado y los escenarios superados se guardan en `localStorage` (por navegador).
7. Al superar un escenario se muestra el **diagrama del flujo** con los pasos agrupados por capa.

---

## 📤 Cómo repartirla

- **Opción A (sin plataforma):** los alumnos abren `index.html` con doble clic (funciona por
  `file://` sin servidor).
- **Opción B (Moodle / Classroom):** subir `index.html` como recurso del tema; se descarga y
  abre igual.
- **Opción C (GitHub Pages):** publicar el repositorio y compartir la URL (se indica abajo). Es
  la recomendada si además quieres que vean un despliegue real.

---

## ✅ Soluciones de los escenarios

El orden correcto (paso 1 → paso último):

**1. Cargar datos (GET)**
Navegador (click) → Navegador (`fetch('/api/productos')`) → HTTP (viaja la GET) →
Express (encuentra ruta) → Express (SELECT) → MySQL (devuelve filas) →
Express (`res.json`, 200) → Navegador (`.then` actualiza DOM).

**2. Enviar datos (POST)**
Navegador (submit) → Navegador (`preventDefault`) → Navegador (`JSON.stringify`) →
HTTP (`fetch` POST con body) → Express (ruta POST) → Express (`express.json()` → `req.body`) →
Express (validación) → Express (INSERT) → MySQL (confirma) →
Express (`res.status(201)`) → Navegador (mensaje + nuevo GET).

**3. Error 404**
Navegador (`fetch('/api/productos/999')`) → HTTP → Express (ruta `/:id`) →
Express (SELECT por id) → MySQL (0 filas) → Express (`res.status(404)`) →
HTTP (respuesta 404, `response.ok = false`) → Navegador (comprueba `response.ok` y lanza) →
Navegador (`.catch` muestra mensaje).

**4. Error 500**
Navegador (`fetch`) → Express (llama controlador) → Express (la SQL falla) →
MySQL (excepción a Node) → Express (try/catch) → Express (`res.status(500)`) →
Navegador (`response.ok = false`) → Navegador (`.catch` muestra mensaje).

**5. Validación 400**
Navegador (submit, campo vacío) → Navegador (POST con body) → Express (ruta + parsea) →
Express (valida y detecta vacío) → Express (`res.status(400)`) → Navegador (`response.ok = false`) →
Navegador (lanza + `.catch`) → Navegador (muestra mensaje en el formulario).

**6. Sin red / servidor caído**
Navegador (`fetch`) → HTTP (sale la petición) → Navegador (nadie responde / AbortController) →
Navegador (la promesa se **rechaza**) → Navegador (`.catch` captura) → Navegador (mensaje).

---

## 🔑 Conceptos clave que conviene destacar en clase

- `fetch()` **no se rechaza** ante un 404/500: se resuelve con `response.ok = false`. El rechazo
  (`.catch`) solo ocurre cuando **no hay respuesta** (red, timeout, servidor apagado).
- El servidor siempre debe **validar** los datos del cliente (nunca confiar a ciegas).
- El orden de las capas de ida es Navegador → HTTP → Express → MySQL; la vuelta recorre
  MySQL → Express → HTTP → Navegador.
- Un mismo escenario visita una capa **más de una vez** (p. ej. en GET: Navegador al inicio y al
  final; Express para consultar y para responder).

---

## 🚀 Publicación en GitHub Pages (pasos)

1. Crear repositorio e inicializar:
   ```bash
   git init
   git add index.html
   git commit -m "Actividad: el flujo de una petición web"
   ```
2. Crear el repositorio en GitHub (sin README) y vincular:
   ```bash
   git remote add origin https://github.com/TU_USUARIO/repaso-flujo.git
   git branch -M main
   git push -u origin main
   ```
3. En GitHub: **Settings → Pages → Source → Deploy from a branch → main → / (root) → Save**.
4. La URL será `https://TU_USUARIO.github.io/repaso-flujo/` (listo en 1–2 minutos).
   `index.html` en la raíz se sirve automáticamente; no requiere build ni configuración extra.

---

## 💡 Ideas para ampliar

- **Desafío "construye el flujo real":** tras la actividad, pedir que monten el stack completo
  (Express + MySQL + formulario con fetch) y que verifiquen cada escenario observando la red en
  DevTools (pestaña Network) y los logs de Express/MySQL.
- **Dibújalo a mano:** que representen el flujo del escenario 1 con flechas entre las 4 capas.
- **Comparar errores:** que expliquen con sus palabras por qué en un 500 no se ejecuta el `.then`.
- **Variación competitiva:** a mayor aciertos en menos intentos, "nivel alcanzado" en la app.