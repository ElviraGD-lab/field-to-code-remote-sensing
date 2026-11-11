---
title: "Capítulo 3. Qué ve un satélite"
---

## Dónde lo dejamos

En el capítulo 1 vimos que, en las bandas infrarrojas, lo quemado sale marrón rojizo, la vegetación viva sale verde y la sombra, casi negra. En las reglas para elegir imágenes también hablamos de bandas y de SWIR. Ha llegado el momento de entender qué hay detrás. Así dejaremos de limitarnos a reconocer colores y empezaremos a leer la imagen.

## Qué es la luz para un satélite

La luz del sol es una mezcla de ondas de distintas longitudes. El ojo solo ve una parte estrecha, más o menos entre 0,4 y 0,7 micrómetros (µm):

- las ondas cortas las vemos como azul;
- las medias, como verde;
- las largas, como rojo.

Más allá del rojo la luz sigue, pero el ojo ya no la ve:

- infrarrojo cercano (NIR): más o menos entre 0,7 y 1,3 µm;
- infrarrojo de onda corta (SWIR): más o menos entre 1,3 y 2,5 µm.

Es la misma luz del sol, solo que con otra longitud de onda. La radiación térmica, la que emite un cuerpo caliente, empieza todavía más allá, y aquí no la necesitamos.

**Al satélite le da igual si el ojo ve esa luz o no. Mide todas estas franjas de la misma manera.**

## Qué mide cada banda

Sentinel-2 divide la luz en 13 franjas estrechas[^s2]. Cada una se llama banda. En cada banda, el satélite mide una sola cosa: qué fracción de la luz del sol que llega a la superficie se refleja. Ese número, entre 0 y 1, se llama reflectancia. Un 0 significa que la superficie ha absorbido toda la luz; un 1, que la ha reflejado toda.

Para nuestro trabajo importan siete bandas:

| Banda | Luz | Píxel | Para qué nos sirve |
|---|---|---|---|
| B2 | azul | 10 m | color natural |
| B3 | verde | 10 m | color natural |
| B4 | rojo | 10 m | color natural; las plantas lo absorben |
| B8 | infrarrojo cercano | 10 m | las plantas vivas lo reflejan mucho |
| B8A | infrarrojo cercano, estrecho | 20 m | lo mismo; se usa junto con el SWIR |
| B11 | infrarrojo de onda corta 1 | 20 m | sensible al agua de las plantas |
| B12 | infrarrojo de onda corta 2 | 20 m | la banda principal para lo quemado |

De aquí salen los 20 metros del capítulo 1: en Sentinel-2, las bandas infrarrojas con las que se busca lo quemado tienen píxeles de 20 por 20 metros.

## Cómo refleja la luz la vegetación viva

Vamos a analizar una hoja paso a paso. Cada paso se deduce de cómo está hecha la hoja.

1. **La luz roja y la azul, la hoja las absorbe.** La clorofila toma esa energía para la fotosíntesis. Por eso, en la banda roja, la vegetación viva sale oscura.
2. **La verde la absorbe un poco menos.** Por eso vemos las hojas verdes.
3. **El infrarrojo cercano, la hoja lo refleja mucho.** No le sirve para la fotosíntesis y, además, dentro de la hoja hay muchas células separadas por huecos de aire. En cada frontera entre célula y aire, la luz se dispersa y la mayor parte vuelve hacia fuera. Una hoja viva brilla mucho en el infrarrojo cercano, mucho más que en la luz visible.
4. **El infrarrojo de onda corta lo absorbe el agua de la hoja.** Cuanta más agua tiene la planta, más oscura sale en el SWIR.

**Así que la vegetación viva tiene su propio patrón:** oscura en el rojo, brillante en el infrarrojo cercano y oscura en el SWIR. Ese patrón de reflexión en las distintas bandas se llama firma espectral.

## Qué cambia el incendio

Quememos ahora esa hoja y veamos qué pasa en cada paso.

1. **Ya no hay clorofila:** la luz roja ya no se absorbe tanto.
2. **Ya no hay células con aire:** el carbón y la ceniza no dispersan el infrarrojo cercano. En el infrarrojo cercano, lo quemado se vuelve oscuro.
3. **Ya no hay agua:** no queda nada que absorba el SWIR, y la tierra seca y desnuda refleja bien esa luz. En el SWIR, lo quemado sale más claro que la vegetación que había antes.

**El incendio le da la vuelta al patrón:** en el infrarrojo cercano, lo que era claro pasa a oscuro; en el SWIR, lo que era oscuro pasa a más claro. Ningún otro cambio habitual en una ladera hace las dos cosas a la vez. Por eso la mejor forma de buscar lo quemado es la pareja «infrarrojo cercano y SWIR».

## De dónde salen los colores de nuestra imagen

Ahora ya podemos explicar lo que vimos en el capítulo 1. La visualización SWIR asigna tres bandas a los tres colores de la pantalla:

- B12 (SWIR 2), al rojo;
- B8A (infrarrojo cercano), al verde;
- B4 (luz roja), al azul.

Deducimos cada color nosotros mismos:

- **Vegetación viva:** B8A brillante, B12 oscura → en pantalla domina el verde. Sale verde.
- **Lo quemado:** B8A oscura, B12 más clara → domina el rojo y el conjunto es poco brillante. Sale marrón rojizo.
- **Sombra de una nube:** poca luz en todas las bandas → casi negra.
- **Nube:** lo refleja casi todo en todas las bandas → blanca.
- **Agua:** absorbe tanto el infrarrojo cercano como el SWIR → negra. En nuestra imagen, el río Navia y el embalse salen, efectivamente, negros.

**El color de la imagen no es «el color del objeto», sino el registro de cuánta luz ha reflejado en cada una de las tres bandas.** Si sabemos qué banda va a qué color, podemos predecir el color de cualquier superficie.

## Qué significa «asignar una banda a un color»

### El satélite ya lo ha medido todo

**Empecemos por lo más importante:** cuando cambiamos de visualización, el satélite no hace nada. Pasó una sola vez sobre Asturias el 8 de abril de 2026 y, en esa pasada, midió la luz en las 13 bandas a la vez.

Para cada píxel tenemos 13 números, uno por banda. Podemos imaginar la imagen como una pila de 13 hojas de papel vegetal con la misma cuadrícula. En cada hoja, cada casilla guarda un número: cuánta luz reflejó ese trozo de terreno en esa banda.

**Los datos son siempre los mismos. Lo único que cambia es cómo los mostramos.**

### La pantalla solo sabe hacer tres colores

Todas las pantallas muestran el color de la misma manera. En cada punto hay tres bombillas diminutas: una roja, una verde y una azul. Cada una se enciende con cierta intensidad, desde apagada hasta el máximo. Cualquier color de la pantalla es una mezcla de esas tres:

- solo se enciende la roja: vemos rojo;
- la roja y la verde: amarillo;
- las tres con fuerza: blanco;
- las tres débiles: casi negro.

**La pantalla no puede mostrar 13 capas a la vez. Solo tiene tres bombillas.**

### Elegimos qué capa maneja cada bombilla

Por eso elegimos tres capas de las trece y decidimos:

- los números de esta capa manejan la bombilla roja;
- los de esta, la verde;
- los de esta, la azul.

Cuanto mayor es el número del píxel, más fuerte se enciende la bombilla. Eso es lo que significa «asignar una banda a un color».

Una visualización de Copernicus Browser es una receta ya hecha: qué tres bandas van a qué tres bombillas. Al cambiar de visualización, solo cambiamos la receta con la que se muestran los datos.

Esto ya lo conocemos de la topografía. Un mismo levantamiento de puntos se puede colorear en el mapa por altura o por fecha de medición. Las medidas son las mismas; solo cambia la forma de mostrarlas a la vista.

### Lo vemos píxel a píxel

Tomemos tres píxeles: matorral vivo, zona quemada y agua. Los números de abajo son inventados, solo sirven de ejemplo, pero guardan entre sí las mismas proporciones que las superficies reales:

| Píxel | B3 (luz verde) | B4 (luz roja) | B8 (infrarrojo cercano) |
|---|---|---|---|
| matorral vivo | 0,06 | 0,04 | 0,40 |
| zona quemada | 0,06 | 0,07 | 0,12 |
| agua | 0,05 | 0,03 | 0,01 |

La receta True Color asigna B4 a la bombilla roja, B3 a la verde y B2 a la azul. Es lo que ve el ojo: cada banda va a «su» color. El matorral sale verde oscuro.

La receta False color asigna B8 a la bombilla roja, B4 a la verde y B3 a la azul. Veamos el matorral vivo:

- **La bombilla roja recibe B8 = 0,40.** Es un número alto: se enciende con fuerza.
- **La verde recibe B4 = 0,04:** casi no se enciende.
- **La azul recibe B3 = 0,06:** casi no se enciende.

Se enciende sobre todo la roja, así que la vegetación viva sale roja en False color. No porque la hierba sea roja, sino porque hemos asignado su infrarrojo cercano, que es muy alto, a la bombilla roja.

**El color de la pantalla no nos dice «de qué color es el objeto», sino «en qué banda brilla más» con la receta elegida.**

## Nos ponemos a prueba con la imagen

Hagamos lo mismo que en el capítulo 1: primero predecimos y luego miramos.

En Copernicus Browser, sobre la misma imagen del 8 de abril de 2026, activamos la visualización False color. En ella, las bandas se asignan así:

- B8 (infrarrojo cercano), al rojo;
- B4 (luz roja), al verde;
- B3 (luz verde), al azul.

Predecimos de qué color saldrán:

- la vegetación viva;
- lo quemado;
- el agua.

Apuntamos la predicción antes de cambiar de visualización y, después, la comprobamos en la imagen.

## Qué ha salido

```{figure} ../images/ch03-false-color-2026-04-08.jpg
:label: es-fig-ch03-false-color
:alt: Imagen del 8 de abril de 2026 en False color (bandas B8, B4 y B3), Copernicus Browser. Contiene datos modificados de Copernicus Sentinel (2026).
:width: 100%

Imagen del 8 de abril de 2026 en False color (bandas B8, B4 y B3), Copernicus Browser. Contiene datos modificados de Copernicus Sentinel (2026).
```

Hemos predicho los colores en False color a partir de la tabla y los hemos comprobado en la imagen del 8 de abril de 2026.

- **La vegetación viva sale de un rojo intenso.** Su infrarrojo cercano va a la bombilla roja y es lo que más brilla. La predicción se cumple.
- **El agua sale negra.** El río Navia y el embalse aparecen en la imagen como líneas negras. Los tres números son casi cero y no se enciende ninguna bombilla. Se cumple.
- **Lo quemado sale oscuro, casi negro, con un tono pardo.** Las tres bombillas se encienden poco, la roja algo más que las otras. Se cumple.

Pero en esta imagen también se ve algo que no habíamos predicho: en False color, las sombras de las nubes también salen oscuras, casi como lo quemado. Tiene sentido: en la sombra hay poca luz en todas las bandas.

**Así que False color separa bien lo vivo de lo que no lo está, pero en ella lo quemado y la sombra se parecen. Para buscar lo quemado es mejor la visualización SWIR: ahí lo quemado sale marrón rojizo y la sombra, negra.**

**De aquí sale una regla que nos servirá en cualquier trabajo con imágenes: una misma imagen la miramos con varias recetas, porque cada receta muestra una diferencia distinta.**

:::{admonition} Tus datos
Las bandas y sus números son los mismos en cualquier imagen de Sentinel-2, en cualquier punto de la Tierra. La tabla de bandas y lo que hemos deducido sobre los colores sirven para cualquier incendio.
:::

Ya sabemos qué mide cada banda y cómo se forma la imagen a partir de las bandas. Antes de buscar imágenes, nos queda entender cuándo y cada cuánto pasa el satélite sobre nuestro incendio.

## El satélite da la vuelta a la Tierra pasando por los polos

Sentinel-2 vuela a unos 786 km de altura[^orb], en una órbita que pasa casi por los polos. Mientras va de norte a sur, la Tierra gira debajo de él. Por eso, en cada vuelta ve una franja nueva de terreno de 290 km de ancho.

El satélite no trabaja solo:

- el trabajo principal lo hacen Sentinel-2B y Sentinel-2C;
- el veterano Sentinel-2A sigue tomando imágenes de apoyo; la ESA ha decidido mantenerlo hasta finales de 2026[^s2a].

## Por qué pasa siempre a la misma hora

La órbita de Sentinel-2 es heliosíncrona. Gira poco a poco a la vez que la Tierra se mueve alrededor del Sol. Como resultado, el satélite cruza el ecuador siempre a las 10:30, hora solar local. Sobre Asturias, eso equivale a las 11:20 UTC, más o menos; es la hora que ya usamos en el prólogo.

¿Por qué se hace así? Por la mañana suele haber menos nubes que por la tarde, y el sol ya está bastante alto. Y, sobre todo, las imágenes de días distintos se pueden comparar: en todas, el sol está en el mismo momento del día.

**De aquí sale una conclusión importante para nosotros. La diferencia de sol entre dos imágenes depende solo de la época del año, no de la hora. Cuanto más cerca estén las fechas de «antes» y «después», menor será esa diferencia. Por eso, en las reglas, pedimos que la imagen de «antes» sea lo más cercana posible al incendio.**

## Cada cuánto ve nuestro incendio

- Un satélite vuelve a la misma traza cada 10 días.
- Dos satélites vuelan en posiciones opuestas de la órbita, así que en el ecuador cualquier lugar se fotografía cada 5 días.
- En nuestras latitudes, las franjas de vueltas vecinas se solapan, y un mismo lugar cae en varias franjas a la vez. Por eso sobre Asturias hay todavía más imágenes. Cuántas exactamente sobre nuestro incendio, lo veremos en el catálogo en el capítulo 4.

Pero que pase a menudo no significa que haya imágenes despejadas a menudo. Sentinel-2 mide la luz del sol, y la luz no atraviesa las nubes. En Asturias, la primavera es nubosa, así que muchas pasadas no sirven para nuestra zona. La frecuencia de las pasadas sirve precisamente para eso: para encontrar una imagen despejada entre muchas nubladas.

## La traza de la pasada: la órbita relativa

En 10 días, el satélite da 143 vueltas y luego repite las mismas trazas. Cada una de las 143 trazas tiene su número: es la órbita relativa.

Un mismo lugar puede caer en las franjas de varias trazas vecinas:

- desde una traza, el satélite mira la ladera casi desde arriba;
- desde otra, la mira de lado, desde el borde de su franja.

Una ladera iluminada por el sol se ve distinta según desde dónde se mire. Por eso escribimos en las reglas que, si es posible, las imágenes de «antes» y «después» sean de la misma órbita relativa.

## El píxel sobre el terreno

El número de un píxel no es el valor en un punto, sino la media de todo el cuadrado: 20 por 20 metros en las bandas infrarrojas. De ahí salen dos consecuencias.

1. **En el borde de lo quemado, los píxeles son mixtos:** tienen una parte quemada y otra de vegetación viva, y su valor es una media. De ahí viene la incertidumbre de un píxel en el perímetro que calculamos en el capítulo 1.
2. **Una isla sin quemar más pequeña que un píxel, el satélite no la verá.** Se «disolverá» en el valor medio de lo quemado.

## Teselas

Para trabajar cómodamente con los datos, las franjas de imagen se cortan en cuadrados de 100 por 100 km con un pequeño solape, de unos 110 km. Son las teselas. Cada una tiene un código con esta forma, por ejemplo: 29TPH. Las primeras cifras son el número de huso UTM, y las letras, la posición del cuadrado dentro de él. Nuestro incendio está al oeste de los 6° O, así que su tesela está en el huso UTM 29. Cuál es exactamente, lo leeremos en el catálogo.

:::{admonition} Tus datos
La hora de paso de Sentinel-2 es la misma, en hora solar local, para cualquier punto de la Tierra. El número de órbita relativa y de tesela de cualquier lugar se lee más fácilmente en el catálogo de imágenes: aparece en cada imagen.
:::

## Resumen

**Conceptos nuevos**

- **Infrarrojo cercano (NIR):** luz con una longitud de onda de entre 0,7 y 1,3 µm, aproximadamente; las plantas vivas la reflejan mucho.
- **Infrarrojo de onda corta (SWIR):** luz con una longitud de onda de entre 1,3 y 2,5 µm, aproximadamente; la absorbe el agua de las plantas.
- **Banda:** franja estrecha del espectro en la que el satélite hace una medida.
- **Reflectancia:** fracción de la luz recibida que la superficie refleja, entre 0 y 1.
- **Firma espectral:** patrón de reflexión de una superficie en las distintas bandas.
- **Órbita heliosíncrona:** órbita en la que el satélite pasa sobre cualquier lugar siempre a la misma hora local.
- **Anchura de barrido:** el ancho de terreno que el satélite ve en una pasada; en Sentinel-2, 290 km.
- **Frecuencia de revisita:** cada cuánto fotografía el satélite el mismo lugar.
- **Órbita relativa:** el número de la traza de la pasada; Sentinel-2 tiene 143.
- **Píxel mixto:** un píxel en el que caen superficies distintas; su valor es una media.
- **Tesela:** cada uno de los cuadrados de unos 110 por 110 km, con su código, en los que se cortan las imágenes de Sentinel-2.

**Lo esencial**

- La vegetación viva sale oscura en el rojo, brillante en el infrarrojo cercano y oscura en el SWIR.
- El incendio le da la vuelta a ese patrón: el infrarrojo cercano baja y el SWIR sube.
- El color de la imagen depende de qué banda se asigna a cada color de la pantalla.
- Lo quemado se ve mejor con la pareja «infrarrojo cercano y SWIR».
- Sentinel-2 pasa sobre Asturias siempre hacia las 11:20 UTC, así que la diferencia de sol entre imágenes solo depende de la estación.
- Hay muchas pasadas, pero pocas imágenes despejadas: el satélite no ve a través de las nubes.
- Desde órbitas relativas distintas, las laderas se ven distintas.
- Un píxel es la media de un cuadrado; los bordes de lo quemado y las islas pequeñas quedan difuminados.

## Preguntas para un ingeniero

1. ¿Por qué una hoja viva brilla más en el infrarrojo cercano que en la luz visible?

:::{dropdown} Respuesta
La luz visible, sobre todo la roja y la azul, la absorbe la clorofila para la fotosíntesis. El infrarrojo cercano a la planta no le sirve, y dentro de la hoja se dispersa una y otra vez en las fronteras entre células y aire, así que la mayor parte vuelve hacia fuera.
:::

2. Una ladera se ha secado tras un verano caluroso, pero no ha ardido. ¿Cómo cambiará en el SWIR y en el infrarrojo cercano?

:::{dropdown} Respuesta
En el SWIR se aclarará, porque las plantas tienen menos agua. En el infrarrojo cercano cambiará poco, porque las células de las hojas siguen ahí. En lo quemado cambian las dos cosas a la vez: el infrarrojo cercano se oscurece mucho y el SWIR sube. Por eso la sequedad y el incendio se pueden distinguir.
:::

3. ¿Por qué en la visualización SWIR tanto la sombra como el agua salen negras? ¿Cómo las distinguimos?

:::{dropdown} Respuesta
Las dos apenas reflejan luz en ninguna de las tres bandas asignadas. Se distinguen por la forma y el lugar: el agua sigue el cauce del río o la orilla del embalse, y la sombra está junto a una nube y se desplaza con ella en las imágenes de fechas distintas.
:::

4. Dos imágenes se tomaron el 10 de marzo y el 8 de abril. ¿Por qué el sol está distinto en cada una, si el satélite pasa a la misma hora?

:::{dropdown} Respuesta
Porque la hora del día es la misma, pero la época del año no. En un mes, el sol del mediodía sube más, así que las laderas reciben la luz de otra manera.
:::

5. El satélite pasó 12 veces sobre el incendio en un mes, pero solo hay 2 imágenes despejadas. ¿Es un error del catálogo?

:::{dropdown} Respuesta
No. Sentinel-2 mide la luz del sol reflejada y no ve a través de las nubes. La pasada existió, pero sobre nuestra zona había nubes.
:::

6. Dentro de lo quemado hay un claro sin quemar de 10 por 10 metros. ¿Lo veremos en la imagen?

:::{dropdown} Respuesta
Por separado, no: ocupa solo una cuarta parte de un píxel de 20 por 20 metros. Su reflexión se mezclará con la de lo quemado, y el píxel se verá algo más claro que sus vecinos, pero seguirá pareciendo quemado.
:::

## La pregunta que queda abierta

Ya sabemos qué mide el satélite, cuándo pasa y por qué hay imágenes nubladas. Ahora podemos buscar nuestra pareja de imágenes: la despejada más cercana de «antes» y la primera despejada de «después». Eso es el capítulo 4.

---

## Notas y fuentes

[^s2]: [Copernicus SentiWiki, *Sentinel-2 mission*](https://sentiwiki.copernicus.eu/web/s2-mission) (en inglés): 13 bandas espectrales; cuatro de 10 m, seis de 20 m y tres de 60 m.
[^orb]: [Copernicus SentiWiki, *Sentinel-2 mission*](https://sentiwiki.copernicus.eu/web/s2-mission) (en inglés): órbita heliosíncrona a 786 km de altura media, paso por el nodo descendente a las 10:30 de hora solar local, ciclo de 10 días y 143 órbitas, barrido de 290 km.
[^s2a]: [Copernicus Data Space Ecosystem, «Sentinel-2A Extension Campaign Prolonged Until the End of 2026», 15 de mayo de 2026](https://dataspace.copernicus.eu/node/3911) (en inglés).
