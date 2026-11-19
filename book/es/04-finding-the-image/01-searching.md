---
title: "4.1. Buscamos las imágenes"
---

## Dónde lo dejamos

Las reglas para elegir las imágenes ya están escritas de antemano. Sabemos qué mide el satélite y por qué muchas pasadas no sirven por culpa de las nubes. Ahora buscamos la pareja: la imagen despejada más cercana antes del incendio y la primera despejada después.

## Qué esperamos encontrar

Primero apuntamos lo que esperamos, como siempre.

1. **La imagen de «después».** Lo más probable es que sea la del 8 de abril de 2026: sobre ella se trazaron las 681 ha, y en el capítulo 1 vimos que está despejada sobre lo quemado. Pero la regla pide la primera imagen despejada después del incendio. Así que hay que comprobar si hay alguna despejada antes, el 6 o el 7 de abril, cuando el fuego aún podía estar activo.
2. **La imagen de «antes».** Aquí no sabemos nada. En primavera, Asturias suele estar nublada, así que puede que tengamos que alejarnos varias semanas del incendio.

## Paso 1. Marcamos nuestra zona

Las reglas no se comprueban en toda la escena, sino en lo quemado más 1 km alrededor. Para ver esa zona en cada imagen, la marcamos en el mapa.

1. En Copernicus Browser, abrimos la imagen del 8 de abril de 2026 con la visualización SWIR: es donde mejor se ve lo quemado.
2. Acercamos el mapa hasta que lo quemado ocupe más o menos un tercio de la pantalla.
3. A la derecha, elegimos la herramienta de polígono (el icono del pentágono) y rodeamos lo quemado con un margen de aproximadamente 1 km por todos lados. La precisión no importa: es un marco dentro del cual buscaremos nubes.

Ahora el marco se queda en el mapa mientras pasamos de una fecha a otra.

```{figure} ../../images/ch04-frame-2026-04-08-swir.jpg
:label: es-fig-ch04-frame-2026-04-08-swir
:alt: Marco de la zona de estudio (amarillo) sobre la imagen del 8 de abril de 2026 en SWIR; a la izquierda, el calendario de fechas con pasadas.
:width: 100%

Marco de la zona de estudio (amarillo) sobre la imagen del 8 de abril de 2026 en SWIR; a la izquierda, el calendario de fechas con pasadas. Contiene datos modificados de Copernicus Sentinel (2026).
```

## Paso 2. Vamos hacia atrás en las fechas

Junto a la fecha hay dos flechas, «‹» y «›». Llevan a la pasada anterior o a la siguiente. La escala y el marco no cambian, así que es fácil comparar el mismo lugar en distintas fechas.

En cada fecha, miramos dentro del marco y nos hacemos cuatro preguntas:

1. ¿Hay nubes?
2. ¿Hay sombras de nubes? Lo comprobamos en SWIR: la sombra sale casi negra.
3. ¿Hay humo o fuego activo?
4. ¿Hay nieve? En SWIR, la nieve sale clara, de un blanco azulado.

Si la respuesta a cualquiera de ellas es «sí», la imagen no sirve y pasamos a la siguiente.

Primero comprobamos el «después»: las fechas del 6, 7 y 8 de abril. Nos quedamos con la primera en la que las cuatro respuestas son «no».

Después comprobamos el «antes»: desde el 5 de abril hacia atrás, día a día, hasta encontrar la primera imagen despejada.

## Paso 3. Leemos la ficha de la imagen

Con la fecha elegida, pulsamos «Find products for current view», debajo de la fecha. Copernicus Browser mostrará la lista de imágenes que cubren la pantalla. Cada una tiene un nombre largo, por ejemplo:

S2B_MSIL2A_20260408T112119_N0511_R037_T29TPH_20260408T151234

Ese nombre es la ficha de la imagen escrita en una sola línea. Vamos a desmontarlo por partes (los números del ejemplo son inventados):

| Parte | Qué significa |
|---|---|
| S2B | satélite: Sentinel-2B |
| MSIL2A | instrumento MSI, nivel de procesado L2A |
| 20260408T112119 | fecha y hora de la toma en UTC: 8 de abril de 2026, 11:21:19 |
| N0511 | versión del procesado: 05.11 |
| R037 | órbita relativa 37 |
| T29TPH | tesela 29TPH |
| última parte | cuándo se procesó la imagen |

Con solo el nombre, cualquiera encontrará exactamente la misma imagen. Por eso lo anotamos completo.

```{figure} ../../images/ch04-products-2026-04-03.jpg
:label: es-fig-ch04-products-2026-04-03
:alt: Productos L2A del 3 de abril de 2026 que cubren el marco: uno por tesela (29TPH y 29TPJ).
:width: 100%

Productos L2A del 3 de abril de 2026 que cubren el marco: uno por tesela (29TPH y 29TPJ). Contiene datos modificados de Copernicus Sentinel (2026).
```

## Paso 4. Capturas de la escena completa y de cerca

Para cada imagen elegida, hacemos estas capturas:

1. **Vista de toda la escena:** alejamos el mapa hasta ver la mayor parte de la tesela, unos 100 km, en color natural. En esta captura se ve la nubosidad de toda la escena.
2. **Vista de cerca de lo quemado:** acercamos el mapa al marco, en color natural y en SWIR.

:::{admonition} Tus datos
Este orden sirve para cualquier incendio: un marco alrededor de lo quemado con margen, pasar las fechas con las flechas, las cuatro preguntas dentro del marco y el nombre de la imagen como ficha.
:::
