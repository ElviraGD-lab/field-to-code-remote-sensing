---
title: "Capítulo 1. Tres cifras para un solo incendio"
---

## Dónde lo dejamos

En el prólogo vimos que el incendio de Bustantigo tiene dos cifras de superficie, 681 y 700 ha, y que ninguna lleva margen de error. También vimos que, en la montaña, el satélite puede confundir el sol de primavera con hierba que ha vuelto a crecer.

Antes de calcular nada, vamos a aclarar tres cosas:

1. qué mide en realidad el satélite;
2. de dónde salen esas dos cifras;
3. por qué no coinciden.

Y al final miraremos el incendio por primera vez con nuestros propios ojos.

## Qué es la teledetección

**La teledetección es medir sin tocar.** No recorremos la ladera con una cinta métrica: la medimos desde lejos, desde un avión, un dron o un satélite. De ahí el nombre: detectar a distancia.

Lo más parecido que ya conocemos es la fotografía aérea. Un avión sobrevuela el terreno y lo fotografía, y luego con esas fotos se dibuja el mapa. Sentinel-2 hace lo mismo, pero con dos diferencias importantes.

1. **Mide, no fotografía.** Cada punto de la imagen no guarda un «color para el ojo», sino un número: qué fracción de la luz del sol ha reflejado la superficie. Es una medida, como la lectura de un instrumento. Con ella podemos calcular, comparar y comprobar.
2. **Ve más que el ojo.** El ojo ve tres colores: rojo, verde y azul. Sentinel-2 mide la luz en 13 franjas estrechas del espectro[^s2]. Algunas son invisibles para nosotros: el infrarrojo cercano y el infrarrojo de onda corta. Y es justo en el infrarrojo donde más se diferencian la vegetación viva y lo quemado.

Hay una tercera cosa que conviene tener clara: Sentinel-2 no emite nada. Solo recibe la luz del sol que refleja la tierra. Un instrumento así se llama pasivo. Uno activo, como el distanciómetro láser de una estación total o un LiDAR, envía su propia señal y capta el reflejo. Para nosotros, la consecuencia principal es esta: un instrumento pasivo depende del sol. Donde el sol ilumina poco, la medida es peor. De ahí viene nuestro problema con las laderas.

**Así que el satélite es un instrumento de medida. Y toda medida tiene un error que hay que conocer.**

## Quién calculó las 681 y las 700 hectáreas

Las dos cifras salen de imágenes de satélite, pero se obtuvieron de forma distinta.

1. 681 ha: el catálogo abierto de grandes incendios de España. Su autor tomó la imagen de Sentinel-2 del 8 de abril y digitalizó el perímetro, es decir, trazó el contorno a mano sobre la imagen. Él mismo avisa de que el perímetro puede desviarse cientos de metros[^edu].
2. 700 ha: el servicio europeo EFFIS, que cartografía los incendios de toda Europa. El perímetro se obtiene de forma semiautomática a partir de imágenes de satélite: un programa marca las zonas que han cambiado y una persona lo revisa[^rda]. El registro se actualizó el 9 de abril[^effis].

**Así que no son dos «verdades», sino dos medidas hechas por personas distintas y con métodos distintos.**

## Por qué un mismo incendio da cifras distintas

Como ingenieros, nos preguntamos: ¿19 ha de diferencia es mucho o poco? Para responder, hay que saber qué error cabe esperar. Vamos a calcularlo.

Sentinel-2 divide el terreno en celdas: los píxeles. En las bandas infrarrojas con las que se busca lo quemado, cada píxel mide 20 por 20 metros. Es nuestro «paso de medida». El perímetro no puede ser más preciso que un píxel.

Veamos qué pasa si el perímetro se desplaza un solo píxel hacia fuera.

1. La superficie del incendio ronda las 700 ha, es decir, 7 000 000 m².
2. **La longitud del perímetro.** Si el incendio fuera un círculo, tendría un radio de unos 1,5 km y un perímetro de unos 9,4 km. El contorno real es sinuoso, así que el perímetro es más largo. Tomamos unos 15 km.
3. **Desplazamiento de un píxel:** 15 000 m × 20 m = 300 000 m², es decir, 30 ha.

**La diferencia entre 681 y 700 ha es menor que lo que cambia la superficie al mover el perímetro un solo píxel.** Así que con estas dos cifras no podemos decir cuál es más precisa. Coinciden dentro de un margen de error que nadie ha indicado.

Además del tamaño del píxel, hay otras tres razones por las que las cifras no coinciden:

- imágenes y fechas distintas: cuanto más tardía es la imagen, más débil es la huella del incendio;
- una forma distinta de trazar el perímetro: a mano o con un programa;
- qué se cuenta como quemado: si se incluyen las islas sin quemar dentro del contorno y el borde poco quemado.

**Por eso nuestra tarea no es elegir una de las dos cifras, sino obtener la nuestra, con su margen de error y explicando cómo la hemos conseguido.**

## Miramos el incendio con nuestros propios ojos

Ahora abrimos la imagen. Trabajamos en Copernicus Browser, una web gratuita de la Unión Europea donde podemos ver todas las imágenes de Sentinel-2 en el navegador, sin descargar nada. Hoy es la herramienta principal para echar un primer vistazo a las imágenes.

Paso a paso:

1. Abrimos https://browser.dataspace.copernicus.eu
2. **Creamos una cuenta gratuita:** arriba a la derecha, «Login» y después «Register». La necesitaremos durante todo el libro.
3. **Buscamos el lugar.** En la barra de búsqueda de arriba escribimos las coordenadas del incendio, 43.361, -6.671, o el nombre Bustantigo.
4. **Elegimos los datos.** A la izquierda, en la pestaña de búsqueda: colección Sentinel-2, nivel L2A. Ponemos la fecha del 8 de abril de 2026: es la imagen sobre la que se trazaron las 681 ha.
5. **La vemos en color natural:** visualización True Color. Es lo que vería el ojo.
6. **La vemos en infrarrojo:** visualización SWIR. Aquí se muestran las bandas invisibles.

**Antes de mirar, apuntamos lo que esperamos ver.** Es una costumbre de ingeniero: primero predecir y luego comprobar. Esperamos que:

- en color natural, lo quemado se vea mal: una mancha oscura que parece la sombra de la ladera;
- en SWIR, lo quemado tenga un color claramente distinto del matorral vivo, y su perímetro se vea más nítido.

## Lo que hemos visto

```{figure} ../images/ch01-true-color-2026-04-08.jpg
:label: es-fig-ch01-true-color-2026-04-08
:alt: Imagen Sentinel-2 L2A del 8 de abril de 2026 en color natural (True Color), Copernicus Browser.
:width: 100%

Imagen Sentinel-2 L2A del 8 de abril de 2026 en color natural (True Color), Copernicus Browser. Contiene datos modificados de Copernicus Sentinel (2026).
```

```{figure} ../images/ch01-wildfires-layer-2026-04-08.jpg
:label: es-fig-ch01-wildfires-layer-2026-04-08
:alt: La misma imagen con la visualización Wildfires.
:width: 100%

La misma imagen con la visualización Wildfires. Contiene datos modificados de Copernicus Sentinel (2026).
```

```{figure} ../images/ch01-swir-2026-04-08.jpg
:label: es-fig-ch01-swir-2026-04-08
:alt: La misma imagen en infrarrojo (SWIR: bandas B12, B8A y B4). La zona quemada de Bustantigo es la mancha marrón rojiza del centro.
:width: 100%

La misma imagen en infrarrojo (SWIR: bandas B12, B8A y B4). La zona quemada de Bustantigo es la mancha marrón rojiza del centro. Contiene datos modificados de Copernicus Sentinel (2026).
```

### Color natural

En la primera imagen, la del 8 de abril de 2026 en color natural, se ve en el centro una mancha marrón oscura. Esa es la zona quemada de Bustantigo.

Pero miremos un poco más a la derecha, hacia Tineo: ahí hay otra mancha oscura casi igual. No es un incendio, sino la sombra de una nube. La propia nube está justo al lado.

**En color natural, lo quemado y la sombra se ven igual:** una mancha oscura sobre verde. Si buscáramos lo quemado solo a ojo y con los colores normales, nos equivocaríamos con facilidad. La primera parte de lo que esperábamos se ha cumplido.

### Bandas infrarrojas

En la tercera imagen, con la visualización SWIR, el panorama cambia:

- La vegetación viva sale de un verde intenso.
- Lo quemado sale marrón rojizo oscuro, con un borde nítido. Se ve al instante.
- La sombra de la nube junto a Tineo sale casi negra, no roja.
- Las nubes salen blancas.

**En las bandas infrarrojas, lo quemado se distingue tanto de la vegetación viva como de la sombra.** La segunda parte de lo que esperábamos también se ha cumplido.

Por qué ocurre lo veremos en el capítulo 3. De momento basta con una idea: las plantas vivas tienen agua y, por eso, reflejan el infrarrojo de otra manera que la tierra quemada. El satélite lo mide aunque el ojo no vea la diferencia.

### Qué más se ve

En la imagen SWIR hay otras manchas pequeñas de color marrón rojizo, por ejemplo más abajo, cerca de Cangas del Narcea. Lo más probable es que sean huellas de otros incendios de esa misma primavera. Lo comprobaremos más adelante, cuando busquemos los otros cuatro incendios.

En la segunda captura está abierta la visualización Wildfires. Resalta las llamas activas: el fuego está muy caliente y brilla mucho en el infrarrojo de onda corta. El 8 de abril el incendio ya está apagado, así que no hay nada que resaltar y la imagen se parece a la de color natural. Esta capa solo sirve mientras el incendio sigue activo.

### Una cifra que nos será útil

Junto a la fecha, Copernicus Browser indica una nubosidad del 30 %. Pero sobre nuestro incendio no hay nubes: están más al oeste y al sur.

La clave es que ese 30 % es la nubosidad de toda la escena, un cuadrado de 110 por 110 km. **Para nuestro trabajo importa si hay nubes sobre la zona que estudiamos, no sobre toda la escena.** Volveremos a esto en el capítulo 4, cuando elijamos las imágenes.

:::{admonition} Tus datos
Todo esto se puede hacer con cualquier incendio. Solo hacen falta las coordenadas del lugar y una fecha: el primer día despejado después del incendio. Las coordenadas y las fechas de los grandes incendios de Europa están en EFFIS.
:::

## Resumen

**Conceptos nuevos**

- **Teledetección:** medir la superficie terrestre sin contacto, desde un avión, un dron o un satélite.
- **Sensor pasivo:** instrumento que recibe la luz solar reflejada y no emite nada por sí mismo.
- **Píxel:** celda de la imagen con un único valor medido; en las bandas infrarrojas de Sentinel-2 mide 20 por 20 metros.
- **Banda espectral:** franja estrecha de luz en la que mide el instrumento.
- **Escena:** una imagen de Sentinel-2, un cuadrado de 110 por 110 km.

**Lo esencial**

- El satélite es un instrumento de medida, y sus resultados tienen margen de error.
- La diferencia entre 681 y 700 ha es menor que lo que cambia la superficie al mover el perímetro un píxel, así que con estas cifras no podemos saber cuál es más precisa.
- En color natural, lo quemado se confunde fácilmente con una sombra; en las bandas infrarrojas se distinguen.
- La nubosidad de la escena y la nubosidad sobre nuestra zona son cosas distintas.

## Preguntas para un ingeniero

1. En la imagen en color natural vemos una mancha oscura. ¿Cómo comprobamos si es una zona quemada o una sombra?

:::{dropdown} Respuesta
Cambiamos a las bandas infrarrojas (SWIR): lo quemado saldrá marrón rojizo y la sombra, casi negra. También podemos mirar si hay cerca una nube que proyecte esa sombra.
:::

2. Dos servicios dan 681 y 700 ha. ¿Podemos decir cuál se ha equivocado?

:::{dropdown} Respuesta
No. Mover el perímetro un solo píxel cambia la superficie en unas 30 ha, y la diferencia entre las dos cifras es de 19 ha. Sin conocer el margen de error de ambas estimaciones, no podemos decir cuál es más precisa.
:::

3. La imagen tiene una nubosidad del 30 %, pero sobre el incendio no hay nubes. ¿Nos sirve?

:::{dropdown} Respuesta
Para un primer vistazo, sí: el 30 % se refiere a toda la escena, y a nosotros solo nos importa nuestra zona. Pero la elección definitiva de las imágenes la haremos con reglas claras que fijaremos de antemano.
:::

## La pregunta que queda abierta

Ya hemos visto lo quemado. Pero para medirlo hay que comparar la imagen de «después» con la de «antes». ¿Qué imágenes elegimos y con qué reglas, para poder fiarnos luego del resultado? Antes de buscar, aprenderemos a pensar como ingenieros: primero la pregunta y las reglas, después la búsqueda.

---

## Notas y fuentes

[^edu]: [edu.forestry.es, «Grandes Incendios Forestales 2026 en España»](https://edu.forestry.es/p/gif2026.html): Allande, 681 ha, perimetración sobre imagen Sentinel-2 del 8 de abril de 2026; «Las delimitaciones pueden contener errores de cientos de metros».
[^rda]: [EFFIS, *Rapid Damage Assessment*](https://forest-fire.emergency.copernicus.eu/about-effis/technical-background/rapid-damage-assessment) (en inglés): los incendios se cartografían con un procedimiento no supervisado y después se verifican y corrigen por interpretación visual.
[^effis]: EFFIS, área quemada 294223 (Allande): 700 ha, actualizada el 9 de abril de 2026. [API de áreas quemadas de EFFIS](https://api.effis.emergency.copernicus.eu/rest/2/burntareas/current/).
[^s2]: [Copernicus SentiWiki, *Sentinel-2 mission*](https://sentiwiki.copernicus.eu/web/s2-mission) (en inglés): 13 bandas espectrales; cuatro de 10 m, seis de 20 m y tres de 60 m.
