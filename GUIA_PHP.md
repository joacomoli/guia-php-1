# Guía de 10 ejercicios — Programación II

**Formato:** solo enunciados. **No incluye soluciones:** el objetivo es que planifiquen, descomponen el problema y escriban su propio código con PHP puro (sin frameworks), usando lo visto en clases: variables, operadores, arrays (indexados y asociativos), condicionales, `for` / `while`, funciones propias, `date()`, paso de datos por URL (`$_GET`), formularios `GET` / `POST` (`$_POST`).

**Reglas generales para todas las entregas**

- Código legible: nombres de variables claros, indentación consistente.
- Probar casos límite (vacío, cero, valores “raros”) y explicar en comentarios qué hicieron con esos casos.
- Al mostrar en pantalla datos que vinieron del usuario, recordar escapar HTML cuando corresponda.

---

## Ejercicio 1 — Cotizador de pedido (merchandising)

Una productora ficticia vende remeras, tazas y pósters. Los precios unitarios están en un **array asociativo** (clave: nombre del producto, valor: precio en pesos). El usuario ingresa por **formulario POST** la cantidad deseada de cada ítem (tres campos numéricos).

**Pedido:** calcular el **subtotal**, aplicar un **descuento** según esta tabla (usar condicionales o `switch`, a criterio):

- Subtotal menor a $10.000: sin descuento.
- Entre $10.000 y $24.999: 5 %.
- $25.000 o más: 12 %.

Mostrar en la misma página (después del envío) un resumen: ítems pedidos, subtotal, porcentaje aplicado, monto descontado y **total final**. Encapsular el cálculo del descuento en **al menos una función** propia que reciba parámetros.

---

## Ejercicio 2 — Filtro de reseñas (blog temático)

Tienen un **array indexado** de reseñas; cada elemento es un **array asociativo** con claves: `autor`, `puntuacion` (entero del 1 al 5) y `texto`.

**Pedido:** mostrar en una página PHP solo las reseñas cuya `puntuacion` sea **mayor o igual** a un valor mínimo que el usuario elige en un **formulario GET** (por ejemplo: “mostrar desde 4 estrellas”). Si no hay ninguna que cumpla, mostrar un mensaje claro (no un listado vacío sin explicación). El valor mínimo debe leerse de `$_GET` con un nombre de parámetro coherente.

---

## Ejercicio 3 — Agenda de estreno (fechas con `date()`)

Simular la “semana del estreno” de una película: la fecha de estreno es un **string** fijo en formato `Y-m-d` definido en el código (por ejemplo `'2026-07-02'`).

**Pedido:** generar y mostrar una **tabla HTML** con siete filas: cada día desde el estreno inclusive hasta seis días después. Columnas sugeridas: “día de la semana”, “fecha en dd/mm/YYYY”. No hace falta base de datos: todo generado en PHP.

**Nota para el docente / alumnos:** con solo `date()` hace falta un **timestamp** por día. Opciones válidas: (a) consultar el manual de PHP y usar `strtotime()` para sumar días en un `for`; (b) si se quiere ceñir estrictamente a lo ya dictado en Clase 0–1, el docente puede autorizar leer el manual de `strtotime` como extensión de una clase, o bien simplificar el ejercicio a “siete fechas ya cargadas en un array” y que el desafío sea **formatear** cada una con `date()` a `d/m/Y` y mostrar el nombre del día.

---

## Ejercicio 4 — Mini ranking de personajes (ordenar sin “magia” de frameworks)

Hay un **array asociativo** donde cada clave es el nombre de un personaje y el valor es su cantidad de votos (entero). Ejemplo conceptual: `['Ellie' => 120, 'Joel' => 98, ...]`.

**Pedido:** mostrar un **ranking** del más votado al menos votado. Restricción: **no** usar funciones de ordenamiento listas de PHP (`sort`, `asort`, `uksort`, etc.) si el docente pide “implementación manual”; en ese caso, deben ordenar con bucles y comparaciones. Si el docente permite funciones nativas, deben **justificar** en un comentario por qué eligieron esa función.

En caso de empate en votos, definir ustedes una regla clara (por ejemplo: orden alfabético del nombre) y documentarla en el código.

---

## Ejercicio 5 — Validador de registro (lógica, sin base de datos)

Simular un registro de usuario con **formulario POST** con campos: `usuario`, `email`, `edad`, `clave`, `clave_repetir`.

**Pedido:** al enviar, validar **en PHP** (no solo con HTML):

- `usuario`: no vacío, longitud entre 4 y 20 caracteres.
- `edad`: número entero entre 13 y 120.
- `clave` y `clave_repetir`: deben coincidir y tener al menos 8 caracteres.
- `email`: debe contener al menos un `@` y un punto después del `@` (validación simple con funciones de string; no hace falta regex avanzada salvo que el docente lo permita).

Mostrar **todos los errores** encontrados en una lista (no solo el primero), o un mensaje de éxito si todo es válido. No guardar en MySQL todavía: solo feedback en pantalla.

---

## Ejercicio 6 — Navegación por “modo” con query string

Una misma página `catalogo.php` debe mostrar contenido distinto según un parámetro **GET** llamado `modo`, con valores permitidos: `todos`, `ofertas`, `novedades`.

**Pedido:** si `modo` no existe o tiene un valor no permitido, mostrar un mensaje de error amable y un enlace para volver con `modo=todos`. Si es válido, mostrar un título distinto y una lista distinta (pueden ser listas **simuladas** en arrays en el mismo archivo). Usar `switch` o `if/elseif` de forma ordenada. Incluir desde otra página enlaces de prueba del tipo `catalogo.php?modo=ofertas`.

---

## Ejercicio 7 — Tabla de multiplicar personalizada (`for` + función)

El usuario envía por **GET** un entero `n` entre 1 y 12.

**Pedido:** si el número es válido, mostrar la **tabla de multiplicar** de `n` del 1 al 10 en una tabla HTML. Si no es válido, mensaje de error. La generación de cada fila puede hacerse con un `for`. Opcional exigente: escribir una **función** que reciba `n` y `m` y devuelva el producto (sin usar `*` directamente en el cuerpo principal del script más de una vez… o inventen una restricción creativa con el docente).

---

## Ejercicio 8 — Inventario con alerta de stock (arrays + bucles + condición)

Un **array indexado** de productos; cada producto es asociativo: `codigo`, `nombre`, `stock`, `stock_minimo`.

**Pedido:** recorrer el inventario y mostrar una tabla. Agregar una columna **“Estado”** que diga `OK` si `stock >= stock_minimo`, o `REPONER` si no. Al final, mostrar un **resumen**: cuántos productos están en `REPONER`. Usar al menos un bucle `for` o `foreach` y contadores.

---

## Ejercicio 9 — Adivinanza con intentos (`while` + `rand`)

Juego en una sola página: al cargar por primera vez (sin parámetros), el script genera un número aleatorio del 1 al 100 y el número secreto se pasa de un envío a otro usando un **campo oculto** `input type="hidden"` en un formulario POST con el valor del número.

**Pedido:** el usuario ingresa un intento; el servidor responde “mayor”, “menor” o “correcto”. Limitar a **máximo 7 intentos**; si se agotan, mostrar el número secreto. Reiniciar puede ser un enlace que vuelva a la página sin POST.


---

## Ejercicio 10 — Integración: “Panel” de métricas de lectura del blog

Combinar varios conceptos: tienen un array de **entradas de blog** (asociativo por entrada: `titulo`, `fecha_publicacion` en `Y-m-d`, `visitas`).

**Pedido:**

1. Mostrar todas las entradas en una lista o tabla.
2. Calcular y mostrar: **total de visitas** del blog (suma).
3. Indicar cuál entrada tiene **más visitas** (si hay empate, listar todas las empatadas).
4. Agregar un **formulario GET** con un año (selector o campo numérico) que **filtre** y muestre solo las entradas de ese año; si el año no tiene entradas, mensaje informativo.

Encapsular en **funciones** al menos: (a) suma de visitas, (b) búsqueda del máximo de visitas.

---
