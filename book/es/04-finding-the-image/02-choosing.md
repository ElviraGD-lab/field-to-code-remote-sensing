---
title: "4.2. Qué hemos encontrado y qué elegimos"
---

## Dónde lo dejamos

Hemos ido pasando las fechas dentro del marco alrededor de lo quemado y hemos revisado cada una en busca de nubes, sombras, humo y nieve. Ahora toca contrastar lo que hemos encontrado con las reglas que escribimos antes de buscar y elegir la pareja de imágenes.

## Qué hemos encontrado

En abril de 2026 hubo 9 pasadas sobre nuestro marco: los días 3, 8, 10, 13, 18, 20, 23, 28 y 30. Primero revisamos las fechas cercanas al incendio:

| Fecha | Qué hay en el marco | ¿Sirve? |
|---|---|---|
| 3 de abril | despejado, sin nieve | sí |
| 8 de abril | casi despejado, pero hay dos manchas blancas pequeñas en el sur del marco | dudosa |
| 10 de abril | despejado | sí |
| 13 de abril | nubes | no |
| 18 de abril | nubes | no |
| 20 de abril | despejado, pero hay una mancha blanca en el centro de lo quemado | dudosa |

## Las fichas de las imágenes

Para cada fecha que podía servir, leímos el nombre de la imagen:

| Fecha | Satélite | Hora, UTC | Órbita | Teselas | Versión del procesado |
|---|---|---|---|---|---|
| 3 de abril | Sentinel-2B | 11:21:09 | R037 | 29TPH, 29TPJ | 05.12 |
| 8 de abril | Sentinel-2C | 11:21:11 | R037 | 29TPH, 29TPJ | 05.12 |
| 10 de abril | Sentinel-2A | 11:21:31 | R037 | 29TPH, 29TPJ | 05.12 |
| 20 de abril | Sentinel-2A | 11:21:31 | R037 | 29TPH, 29TPJ | 05.12 |

La tabla nos dice tres cosas de un vistazo.

1. **Todas las imágenes son de la misma órbita relativa, la R037.** La regla 6 se cumple sola: en todas las imágenes, el satélite mira las laderas con el mismo ángulo.
2. **El incendio está en el límite entre dos teselas, la 29TPH y la 29TPJ.** Por eso el catálogo muestra dos productos para cada fecha.
3. **La hora de la toma apenas cambia:** hacia las 11:21. Es la órbita heliosíncrona del capítulo 3.

## La nubosidad de la escena engaña

También probamos el filtro de nubosidad que ofrece el catálogo. Si dejamos solo las imágenes con una nubosidad de la escena de hasta el 25 %:

- el 18 de abril pasa el filtro, aunque sobre el incendio está nublado;
- el 10 y el 20 de abril no lo pasan, aunque sobre el incendio está despejado.

La escena del 8 de abril también es nubosa: hay nubes al norte y al sur, pero no sobre nuestro marco.

**El filtro por nubosidad de toda la escena habría descartado dos imágenes buenas y dejado pasar una mala.** Es una confirmación directa de la regla: lo despejado se comprueba dentro de nuestro marco, no con la cifra de toda la escena.

```{figure} ../../images/ch04-scene-cloud-filter-25.jpg
:label: es-fig-ch04-scene-cloud-filter-25
:alt: Con el filtro de nubosidad de escena hasta el 25 %, en abril quedan solo el 3, el 8 y el 18.
:width: 100%

Con el filtro de nubosidad de escena hasta el 25 %, en abril quedan solo el 3, el 8 y el 18. Contiene datos modificados de Copernicus Sentinel (2026).
```

```{figure} ../../images/ch04-whole-scene-2026-04-08.jpg
:label: es-fig-ch04-whole-scene-2026-04-08
:alt: Escena del 8 de abril de 2026: nubes al norte y al sur, el marco casi despejado.
:width: 100%

Escena del 8 de abril de 2026: nubes al norte y al sur, el marco casi despejado. Contiene datos modificados de Copernicus Sentinel (2026).
```

## Las manchas blancas del 8 de abril: ¿son nubes o no?

Las manchas blancas del sur del marco, el 8 de abril, podían ser nubecillas o rocas claras. Lo comprobamos de dos maneras.

**Manera 1. La clasificación automática.** Las imágenes L2A traen una capa ya hecha, Scene classification[^scl]: el programa de procesado ha asignado cada píxel a una clase, como «vegetación», «nube», «sombra de nube» o «agua». La activamos para el 8 de abril.

La clasificación no marca las manchas como nubes con seguridad: solo hay unos pocos píxeles de «nube con probabilidad media» y «sin clasificar». Pero la capa nos enseñó otra cosa mucho más importante. El programa asignó la mayor parte de lo quemado a las clases «sombra de nube» o «sombra del relieve». Lo quemado es oscuro, y para el programa se parece a una sombra.

**Así que, si usamos esta capa como máscara de nubes y sombras, recortará la mitad de nuestra zona quemada.** No podemos fiarnos a ciegas de una máscara automática. Hay que revisarla a ojo, sobre todo en zonas quemadas.

**Manera 2. Comparar con una fecha cercana.** Las piedras y las rocas se quedan donde están; las nubes se van. En la imagen del 10 de abril, dos días después, no hay manchas blancas en esos mismos sitios.

**Conclusión:** el 8 de abril hay dos nubecillas dentro del marco. Tapan una parte minúscula, pero están ahí.

```{figure} ../../images/ch04-small-clouds-2026-04-08.jpg
:label: es-fig-ch04-small-clouds-2026-04-08
:alt: 8 de abril de 2026, color natural: dos manchas blancas pequeñas en el sur del marco.
:width: 100%

8 de abril de 2026, color natural: dos manchas blancas pequeñas en el sur del marco. Contiene datos modificados de Copernicus Sentinel (2026).
```

```{figure} ../../images/ch04-scene-classification-2026-04-08.jpg
:label: es-fig-ch04-scene-classification-2026-04-08
:alt: Capa Scene classification del 8 de abril de 2026: gran parte de lo quemado aparece como sombra.
:width: 100%

Capa Scene classification del 8 de abril de 2026: gran parte de lo quemado aparece como sombra. Contiene datos modificados de Copernicus Sentinel (2026).
```

## La decisión según las reglas

Ahora aplicamos las reglas que escribimos antes de buscar, sin hacer excepciones.

1. **La imagen de «antes» es la del 3 de abril de 2026.** Es la imagen despejada más cercana al incendio: 3 días antes. En el marco no hay nubes, ni sombras, ni nieve. Solo hay nieve lejos, al sur, en las montañas altas.
2. **La imagen de «después» es la del 10 de abril de 2026.** Según la regla 4, en el marco no puede haber nubes. La del 8 de abril incumple esa regla, así que la primera imagen totalmente despejada después del incendio es la del 10 de abril.
3. **Entre las dos imágenes hay 7 días.** Según la regla 3, hasta dos semanas es «bien».

**No cogemos la del 8 de abril, aunque sobre ella se trazaron las 681 ha y aunque las nubecillas sean muy pequeñas.** Para esto escribimos las reglas de antemano: para que la elección no dependa de qué imagen nos resulta más familiar o más bonita.

Esta decisión nos cuesta poco. En dos días, la huella del incendio casi no se debilita, y la imagen del 8 de abril la guardamos como reserva y para comparar.

La imagen del 20 de abril no hace falta para la pareja, pero nos servirá para la serie temporal del capítulo 13. Allí tendremos que excluir del cálculo la mancha blanca del centro de lo quemado.

```{figure} ../../images/ch04-before-2026-04-03-swir.jpg
:label: es-fig-ch04-before-2026-04-03-swir
:alt: Imagen de «antes»: 3 de abril de 2026, SWIR.
:width: 100%

Imagen de «antes»: 3 de abril de 2026, SWIR. Contiene datos modificados de Copernicus Sentinel (2026).
```

```{figure} ../../images/ch04-after-2026-04-10-swir.jpg
:label: es-fig-ch04-after-2026-04-10-swir
:alt: Imagen de «después»: 10 de abril de 2026, SWIR.
:width: 100%

Imagen de «después»: 10 de abril de 2026, SWIR. Contiene datos modificados de Copernicus Sentinel (2026).
```

Descargaremos las dos teselas de cada fecha que necesitamos. En el capítulo 5 abriremos los archivos y comprobaremos qué tesela cubre nuestro marco entero.

:::{admonition} Tus datos
Para nuestro propio incendio, hacemos una tabla igual: fecha, qué hay en el marco, si sirve y la ficha de la imagen. La capa Scene classification es útil, pero en zonas quemadas puede confundir lo quemado con sombras. La revisamos siempre a ojo.
:::

## Resumen

**Conceptos nuevos**

- **Scene classification (SCL):** capa de clases ya preparada que acompaña a cada imagen L2A: vegetación, nube, sombra, agua, nieve y otras.
- **Máscara de nubes:** capa con la que se excluyen del cálculo los píxeles con nubes y sombras.

**Lo esencial**

- La nubosidad de toda la escena no dice si sobre nuestra zona está despejado.
- Una máscara automática de nubes puede confundir lo quemado con sombra, así que la revisamos a ojo.
- Una nube se distingue de una roca comparando con una fecha cercana: las nubes se van y las rocas se quedan.
- Decidimos según las reglas escritas de antemano, aunque otra imagen nos resulte más familiar.

## Preguntas para un ingeniero

1. ¿Por qué no hemos cogido la imagen del 8 de abril, si las nubecillas tapan una parte minúscula del marco?

:::{dropdown} Respuesta
Porque, según la regla escrita antes de buscar, en el marco no puede haber nubes, y la imagen del 10 de abril sí cumple esa regla. Si empezamos a saltarnos las reglas «en cosas pequeñas», la elección vuelve a depender de lo que nos apetece. Además, dos días apenas cambian la huella del incendio.
:::

2. Queremos excluir automáticamente las nubes y las sombras con la capa Scene classification. ¿Qué peligro tiene en una zona quemada?

:::{dropdown} Respuesta
La capa asigna muchos píxeles quemados a la clase de sombras, porque lo quemado es oscuro. Una máscara hecha con esta capa recortaría la mayor parte de lo quemado, y la superficie saldría mucho menor que la real.
:::

3. ¿Cómo distinguimos una nube pequeña de una roca clara sin salir de Copernicus Browser?

:::{dropdown} Respuesta
Mirando el mismo sitio en una fecha cercana. En unos días, la nube se habrá ido o se habrá movido, y la roca seguirá en su sitio. Además, junto a una nube suele haber una sombra.
:::

## La pregunta que queda abierta

Ya tenemos la pareja de imágenes: el 3 y el 10 de abril de 2026. Pero ¿qué hay exactamente en el archivo que vamos a descargar? ¿Qué números contiene, y por qué ya son reflectancia en la superficie y no simplemente la luz que llega al satélite? De eso trata el capítulo 5.

---

## Notas y fuentes

[^scl]: [Copernicus SentiWiki, *Sentinel-2 processing*](https://sentiwiki.copernicus.eu/web/s2-processing) (en inglés): el procesador Sen2Cor genera con el producto L2A la capa de clasificación de la escena (SCL).
