---
title: "Capítulo 2. Pensar como ingenieros"
---

## Dónde lo dejamos

Hemos visto lo quemado en la imagen y hemos entendido que, para medirlo, hay que comparar imágenes de antes y de después del incendio. Lo más fácil ahora sería coger dos imágenes, calcular algo y sacar un número.

Pero no lo vamos a hacer así. Primero veamos por qué.

## Por qué no nos ponemos a calcular sin más

El número lo vamos a obtener de todas formas. Un programa siempre calcula algo. La cuestión es otra: ¿podremos fiarnos de ese número y explicarlo?

Si empezamos por el cálculo, lo normal es que pase esto:

1. cogemos las primeras imágenes que encontramos;
2. probamos un umbral: salen 650 ha;
3. probamos otro: 720 ha;
4. nos quedamos con el que «parece cierto», es decir, el que más se acerca a las 700 ha de EFFIS.

Al final no tenemos una medida, sino un ajuste a la cifra de otros. Y nadie, ni siquiera nosotros, podrá explicar por qué lo hicimos así.

**Un ingeniero decide primero qué va a medir, cómo lo va a medir y cómo va a comprobar el resultado. Solo después mide.**

## El método en seis pasos

Repetiremos este orden en cada capítulo del libro. Y sirve para abordar cualquier problema con datos de satélite.

1. **Pregunta.** Convertimos una tarea difusa en una pregunta que se pueda responder midiendo: qué exactamente, dónde, cuándo y con qué precisión.
2. **Qué sabemos y qué no.** Separamos lo conocido de lo desconocido.
3. **Opciones.** De qué maneras se puede responder a la pregunta.
4. **Elección.** Elegimos una manera y apuntamos por qué esa y no otra.
5. **Comprobación.** Dejamos por escrito, de antemano, cómo comprobaremos el resultado y qué consideraremos un fracaso.
6. **Hacer y comparar.** Lo hacemos y comparamos el resultado con lo que esperábamos.

**Lo más importante son los pasos 1 y 5. Una buena pregunta y una comprobación escrita de antemano nos protegen de engañarnos a nosotros mismos.**

## Paso 1. Convertimos «¿cuánto ardió?» en una pregunta

«¿Cuánto ardió?» suena claro, pero no se puede responder midiendo. La pregunta deja cinco cosas en el aire.

1. **Qué significa «ardió».** Dentro del contorno del incendio quedan islas sin quemar. ¿Las contamos o no? Decidimos lo siguiente: lo quemado son las zonas donde el fuego del 6 de abril de 2026 destruyó o dañó la vegetación. Las islas interiores no cuentan. La superficie dentro del contorno general también la anotaremos, pero aparte, porque los servicios suelen dar precisamente esa.
2. **Dónde.** Solo este incendio de Bustantigo. Las zonas quemadas en 2017 y en 2023 no entran, aunque linden con la nuestra.
3. **Cuándo.** En la fecha de la primera imagen despejada después del incendio. Más tarde la huella se debilita, como vimos en el prólogo.
4. **Con qué precisión.** No un solo número, sino una superficie con un intervalo en el que el valor real cae con una probabilidad del 95 %.
5. **En qué unidad.** En hectáreas.

Ahora la pregunta queda así:

**P1. ¿Qué superficie de vegetación ardió en el incendio del 6 de abril de 2026 en Bustantigo, según la primera imagen despejada de Sentinel-2 después del incendio, con un intervalo del 95 %, y cuánto depende esa superficie de la iluminación de las laderas?**

Es larga, pero se puede responder midiendo, y la respuesta se puede comprobar.

La segunda pregunta la construimos igual:

**P2. ¿Cómo cambia la huella del incendio en las imágenes de Sentinel-2, desde la primera imagen despejada después del incendio hasta noviembre de 2026, en cinco incendios de febrero a abril en matorrales de montaña de Asturias, y qué parte de ese cambio se explica por el cambio de iluminación de las laderas y no por el rebrote de la vegetación?**

## Paso 2. Qué sabemos y qué no

**Sabemos:**

- la fecha del incendio (6 de abril de 2026) y el lugar;
- dos estimaciones ajenas de la superficie: 681 y 700 ha, sin margen de error;
- que lo quemado se ve bien en las bandas infrarrojas;
- que la imagen del 8 de abril está despejada sobre el incendio;
- que la luz en las laderas cambia con la estación del año.

**No sabemos:**

- qué imagen de «antes» del incendio está despejada y nos sirve;
- cuál es la mejor manera de trazar el perímetro de lo quemado;
- cuánto influye la luz en el resultado precisamente en nuestras laderas;
- cuál es el margen de error.

**Todo lo que no sabemos es, justamente, el plan del libro.** Cada capítulo siguiente resuelve un punto de la segunda lista.

## Por qué la comprobación se escribe antes del cálculo

Este es el paso 5, y es el que menos costumbre tenemos de hacer. Cuando ya tenemos el resultado delante, nos dan muchas ganas de darlo por bueno si «parece cierto». Le pasa a cualquiera, incluso a un científico con experiencia.

Por eso lo hacemos así:

1. **Escribimos las reglas antes del cálculo:** qué imágenes usamos, cómo comprobamos y qué resultado consideramos un fracaso.
2. **Guardamos ese texto, con su fecha, en el repositorio del libro.** La fecha del commit demuestra que las reglas existían antes que el resultado.
3. Si aun así cambiamos una regla, explicamos por qué y mostramos el resultado con las dos reglas.

**Cualquier resultado es un resultado, aunque no nos guste. Ajustar no vale.**

## Reglas para elegir las imágenes

Ya tenemos escritas las preguntas P1 y P2. Ahora necesitamos las imágenes: una de antes del incendio y otra de después. Antes de abrir el catálogo, vamos a escribir las reglas con las que elegiremos. Si primero miramos y luego decidimos, la mano se nos irá sola hacia la imagen «bonita».

## Para qué queremos reglas

Vamos a comparar dos imágenes y a considerar quemado lo que haya cambiado. Eso significa que todo lo que cambie por algo que no sea el incendio será un error. Y entre dos imágenes pueden cambiar muchas cosas:

- las nubes y sus sombras;
- la nieve en las cumbres;
- la altura del sol y las sombras en las laderas;
- el ángulo con el que el satélite mira la ladera;
- el verde de la primavera, que crece aunque no haya incendio.

**Una buena pareja de imágenes son dos imágenes que solo se diferencian en el incendio.** Cada una de las reglas que siguen elimina una de esas diferencias que sobran.

Esto ya lo conocemos del control de deformaciones. Para ver si una estructura se ha movido, la medimos con el mismo instrumento, desde los mismos puntos y en condiciones parecidas. Si no, la diferencia entre lecturas no mostrará el movimiento, sino el cambio de condiciones.

## Primero, nuestra zona

Las reglas no las comprobamos en toda la escena, sino en nuestra zona: lo quemado más una franja de 1 km alrededor.

La franja hace falta porque, más adelante, tomaremos junto a lo quemado zonas sin quemar para comparar. Ellas también necesitan una imagen despejada.

La nubosidad de toda la escena que muestra el catálogo solo nos orienta sobre dónde buscar. La decisión la tomamos mirando nuestra zona.

## Reglas

1. **Nivel de procesado L2A.** Es un producto ya preparado, en el que se ha eliminado el efecto de la atmósfera. Qué se le ha hecho exactamente lo veremos en el capítulo 5.
2. **La imagen de «después» es la primera imagen despejada tras la extinción del incendio.** Más tarde, la huella se debilita. En la imagen no debe haber humo ni llamas.
3. **La imagen de «antes» es la imagen despejada más cercana al inicio del incendio.** Cuanto más cerca estén las fechas, menos diferencia habrá en el sol y en el verde de la primavera.
   - bien: hasta 2 semanas entre imágenes;
   - aceptable: hasta 6 semanas;
   - más de 6 semanas: cogemos la imagen despejada más cercana, pero lo anotamos como punto débil y comprobamos su efecto en el capítulo 7.
4. **Sobre nuestra zona no hay nubes, ni sombras de nubes, ni bruma.** Lo comprobamos a ojo en dos visualizaciones, color natural y SWIR, porque en color natural la sombra y lo quemado se parecen.
5. **No hay nieve en la zona.** En febrero y marzo puede haberla en las cumbres de más de 1000 metros.
6. **Si es posible, la misma órbita.** El satélite pasa sobre Asturias por distintos «carriles», y desde cada uno mira las laderas con un ángulo propio. Desde el mismo carril, las sombras y la iluminación son iguales. Si no encontramos la misma órbita, lo anotamos.
7. **Antes del incendio no había ardido nada en la zona.** Si no, parte de la imagen de «antes» ya sería zona quemada.

**Si no hay ninguna pareja que cumpla todas las reglas, no las suavizamos en silencio.** Cogemos la mejor posible, anotamos qué regla se incumple y comprobamos cuánto afecta al resultado.

## Qué anotamos de cada imagen

Para cada imagen elegida, hacemos una pequeña ficha:

- fecha y hora de la toma;
- satélite: Sentinel-2A, 2B o 2C;
- número de órbita y número de escena (tesela);
- nubosidad de toda la escena y nubosidad sobre nuestra zona;
- altura y acimut del sol;
- versión del procesado.

La ficha sirve para la reproducibilidad. Con ella, cualquiera encontrará exactamente la misma imagen. Y la altura del sol la necesitaremos en el capítulo 7, donde nos ocuparemos de la luz en las laderas.

## Resumen

**Conceptos nuevos**

- **Pregunta medible:** una pregunta en la que está claro qué medimos, dónde, cuándo y con qué precisión.
- **Criterio:** una regla escrita de antemano con la que elegimos los datos o decidimos si el resultado es válido.
- **Reproducibilidad:** cualquier otra persona puede repetir nuestro cálculo a partir de nuestras notas y obtener el mismo resultado.
- **Zona de estudio:** lo quemado más una franja alrededor, donde se comprueban las reglas.
- **Órbita:** el «carril» por el que el satélite pasa sobre la Tierra; desde cada uno mira con un ángulo propio.
- **Tesela:** cada uno de los cuadrados de 110 por 110 km en los que se dividen las imágenes de Sentinel-2; cada tesela tiene su número.
- **Ficha de la imagen:** el registro de todos los datos con los que se puede encontrar y comprobar una imagen.

**Lo esencial**

- Primero la pregunta y las reglas; después, el cálculo.
- En una buena pregunta está claro qué, dónde, cuándo, con qué precisión y en qué unidad.
- La comprobación y el criterio de fracaso se escriben antes del cálculo, con fecha.
- Ajustarse a la cifra de otros no es medir.
- Una buena pareja de imágenes solo se diferencia en el incendio.
- Que esté despejada se comprueba sobre nuestra zona, no con la nubosidad de toda la escena.
- «Antes», lo más cerca posible del incendio; «después», la primera imagen despejada tras el incendio.
- Una regla incumplida no se oculta: se anota y se comprueba.

## Preguntas para un ingeniero

1. Hemos obtenido 698 ha, casi lo mismo que EFFIS. ¿Significa eso que nuestro resultado es correcto?

:::{dropdown} Respuesta
No. Coincidir con la cifra de otros no demuestra nada: la de EFFIS tampoco tiene margen de error. El resultado se valida con la comprobación escrita de antemano, por ejemplo con puntos aleatorios y sobre el terreno, no por parecerse a otra estimación.
:::

2. ¿Por qué en la pregunta P1 es importante indicar «según la primera imagen despejada después del incendio»?

:::{dropdown} Respuesta
Porque la huella del incendio se debilita con el tiempo. Una imagen tomada tres meses después dará una superficie menor. Sin fecha, dos personas obtendrán números distintos y las dos tendrán «razón».
:::

3. ¿Por qué hemos decidido no contar las islas sin quemar dentro del contorno?

:::{dropdown} Respuesta
Porque la pregunta es cuánta vegetación ardió, y las islas no ardieron. Pero también anotaremos aparte la superficie de todo el contorno, para poder comparar con honestidad nuestra cifra con la de los servicios que miden por el contorno.
:::

4. Tenemos una escena totalmente despejada de 10 semanas antes del incendio y una imagen de 5 días antes, despejada sobre nuestra zona pero con nubes a 50 km. ¿Cuál cogemos?

:::{dropdown} Respuesta
La de 5 días antes. Las nubes a 50 km no afectan a nuestra medida. En cambio, 10 semanas suponen un sol bastante más bajo y una vegetación distinta, y esa diferencia se colaría como zona quemada.
:::

5. ¿Por qué comprobamos que la imagen esté despejada también en SWIR y no solo en color natural?

:::{dropdown} Respuesta
Porque en color natural la sombra de una nube se parece a lo quemado, y una bruma ligera apenas se ve. En SWIR la sombra sale casi negra y lo quemado, marrón rojizo, así que no hay forma de confundirlos.
:::

6. ¿Para qué anotar la altura del sol si ahora no la usamos?

:::{dropdown} Respuesta
La necesitaremos en el capítulo 7 para estimar cuánto cambia el resultado por la diferencia de luz entre «antes» y «después». Anotarla ahora cuesta un segundo; buscarla más tarde es trabajo de más y un riesgo de error.
:::

## La pregunta que queda abierta

Ya tenemos las reglas. Pero contienen muchas palabras que de momento solo entendemos a medias: bandas, SWIR, órbita, por qué el satélite pasa siempre a la misma hora. ¿Qué mide en realidad Sentinel-2? De eso trata el capítulo 3.
