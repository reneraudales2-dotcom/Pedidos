# Pedidos – Quiosco de pedidos de Ágape Coffee

Página web de una sola pantalla para que los clientes armen su pedido desde una tablet o celular. Al confirmar, el pedido se guarda en una hoja de Google (a través de un Formulario de Google) y el cliente recibe su número de orden.

No necesita servidor ni instalación: es un solo archivo `index.html` más las fotos.

## Cómo funciona

1. El cliente elige productos en las pestañas **Comida**, **Bebidas Calientes** y **Bebidas Frías**.
2. Abajo siempre ve el total y el botón **VER PEDIDO**.
3. En el resumen puede ajustar cantidades, indicar el sabor (en productos que lo permiten) y escribir observaciones.
4. Al confirmar, el pedido se envía al formulario y se muestra el número de orden. La pantalla se reinicia sola a los 8 segundos.

Si falla el internet al enviar, la página avisa y **conserva el pedido** para reintentar.

## Editar el menú

Todo el menú está en el arreglo `MENU` dentro de `index.html`. Para agregar o cambiar un producto, edita una sola línea:

```js
{ id: 'latte', cat: 'calientes', nombre: 'Latte', precios: { '8oz': 60, '12oz': 65 }, img: 'latte.jpg' },
```

- `cat`: `comida`, `calientes` o `frias`.
- `precios`: un tamaño → se muestra como etiqueta; dos o más → aparece el selector de tamaño. Para productos sin tamaño usa `{ [U]: 150 }`.
- `img`: nombre del archivo de la foto. Si falta o no carga, se muestra un ícono de respaldo.
- `sabor: true`: agrega un campo opcional para indicar el sabor en el resumen.

Los precios se escriben solo aquí; el total se calcula a partir de este arreglo.

## Fotos

Guárdalas en la raíz del repositorio junto a `index.html`. Recomendaciones:

- Usa formato `.jpg` o `.webp` (evita `.jfif`, no todos los navegadores lo soportan).
- Usa nombres sin tildes ni espacios (`bombon.webp`, `te.jpg`). Si renombras una foto, cambia también el nombre en `img` dentro de `MENU`.

## Número de orden

Es un contador que empieza en 1 cada día y se guarda en el dispositivo. Si usas **varias tablets o cajas** al mismo tiempo, abre cada una con una letra en la dirección para que los números no se repitan:

- `https://tu-pagina/?caja=A` → pedidos A-1, A-2, A-3…
- `https://tu-pagina/?caja=B` → pedidos B-1, B-2…

Si el campo de número de orden del formulario de Google está configurado como "solo números", déjalo como texto corto para que acepte las letras.

## Formulario de Google

La dirección del formulario y los códigos de cada campo (`entry.…`) están al inicio del script, en `FORM_URL` y `CAMPOS`. Si recreas el formulario, actualiza esos valores.

> Nota: la dirección del formulario es visible en el código, así que cualquiera podría enviarle pedidos falsos. Revisa siempre el detalle de productos y recalcula el total al preparar el pedido.

## Publicar con GitHub Pages

En el repositorio: **Settings → Pages → Deploy from a branch → `main` / `(root)`**. La página quedará disponible en `https://<usuario>.github.io/Pedidos/`.
