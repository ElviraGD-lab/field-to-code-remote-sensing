---
title: "Soluciones"
---

Respuestas a los ejercicios de cada lección.

## Lección 5.1

1. El nombre de la carpeta termina en `.SAFE`.
2. La banda B12 se toma con píxel de 20 m, así que el nombre debe terminar en `20m`, no en `10m`: `T29TPJ_20260403T112109_B12_20m.jp2`. En el producto no hay copias de B12 con píxel de 10 m.
3. La capa Scene classification asignó la mayor parte de lo quemado a la clase de sombras, porque lo quemado es oscuro. Una máscara hecha con esta capa recortaría lo quemado junto con las «sombras», y la superficie saldría mucho menor que la real.

## Lección 5.2

1. La ficha del producto, `MTD_MSIL2A.xml`, en la carpeta `.SAFE`.
2. Son 12 bandas, no 13. El satélite mide 13 bandas, pero B10 no entra en el producto L2A. En SNAP: B1–B9, B8A, B11 y B12.
3. Para comprobar las nubes solo donde importan: sobre lo quemado y en una franja de alrededor de 1 km a su alrededor, y no en toda la escena de 110 × 110 km. Si no, descartaríamos imágenes despejadas sobre lo quemado por culpa de nubes que están a decenas de kilómetros.

## Lección 5.3

1. TOA es *top of atmosphere*, la reflectancia en la cima de la atmósfera, nivel L1C. BOA es *bottom of atmosphere*, la reflectancia en la superficie, nivel L2A.
2. Es al revés. La que más se dispersa es la luz de onda corta, la azul, es decir, la banda B2. Las ondas largas, como las de B12, son las que menos se dispersan.
3. En color natural, tanto lo quemado como la sombra se ven como una mancha oscura sobre fondo verde, porque en la luz visible los dos reflejan poco. Las bandas infrarrojas ayudan a distinguirlos. En SWIR, lo quemado sale marrón rojizo y la sombra, casi negra.
