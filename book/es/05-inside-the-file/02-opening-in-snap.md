---
title: "5.2. Abrimos la imagen en SNAP"
---

## Dónde lo dejamos

Ya tenemos las cuatro imágenes en el ordenador. Sabemos cómo está organizada la carpeta `.SAFE` y dónde está la banda B12. Pero todavía no hemos visto los números que hay dentro de los archivos.

En esta lección abrimos la imagen del 3 de abril en SNAP y leemos el número de un píxel.

## Por qué SNAP

SNAP es un programa gratuito de la Agencia Espacial Europea para trabajar con imágenes Sentinel. Entiende la carpeta `.SAFE` completa: abre todas las bandas, las fichas y las máscaras como un solo producto. No tenemos que ir buscando los archivos a mano por las carpetas.

Los mapas, el marco y el contorno de lo quemado los haremos más adelante en QGIS, porque allí es más cómodo trabajar con vectores. Todo lo que tiene que ver con la imagen en sí lo hacemos en SNAP.

## Qué queremos saber

**La pregunta:** ¿qué número hay en un píxel de la banda B12 y qué significa?

**Nuestra hipótesis antes de empezar:**

1. En SNAP, cada banda aparecerá una sola vez, y no en tres tamaños de píxel, como en las carpetas. En total, 12 bandas: el satélite mide 13, pero B10 no entra en el producto L2A.
2. En el píxel de B12 veremos un número entero de varios miles, el mismo que hay en el archivo.

**Cómo sabremos que nos hemos equivocado:** si hay otro número de bandas o si en el píxel aparece un número decimal.

## Paso 1. Miramos la ventana de SNAP

Abrimos SNAP. De momento solo necesitamos tres partes de la ventana:

1. **Product Explorer**, a la izquierda: la lista de productos abiertos y lo que contienen.
2. **La ventana de imagen**, en el centro: aquí aparecerá la banda.
3. **Pixel Info**: una pestaña junto a **Product Explorer**. Muestra los valores del píxel que queda bajo el cursor.

Si no vemos algún panel, lo abrimos desde el menú **View → Tool Windows**. El resto de botones y menús no los tocamos por ahora.

## Paso 2. Abrimos el producto

1. **File → Open Product…**
2. Entramos en la carpeta `data/sentinel2` y después en la carpeta de la imagen del 3 de abril (`S2B_MSIL2A_20260403…SAFE`).
3. Elegimos el archivo `MTD_MSIL2A.xml` (la ficha del producto) y pulsamos **Open**.

SNAP lee la ficha y, a partir de ella, encuentra todos los archivos del producto. En **Product Explorer** aparece una línea `[1]` con el nombre del producto. La imagen no aparece sola: de momento, el producto solo se ha añadido a la lista.

Desplegamos la línea `[1]` con la flecha. Dentro hay varias carpetas: **Metadata**, **Vector Data**, **Bands** y otras. Desplegamos **Bands** y contamos las bandas. De paso, miramos qué más hay aparte de las bandas.

```{figure} ../../images/ch05-snap-bands-2026-04-03.jpg
:label: es-fig-ch05-snap-bands-2026-04-03
:alt: El producto del 3 de abril de 2026 abierto en SNAP: en Bands, las 12 bandas y las carpetas de máscaras y ángulos.
:width: 100%

El producto del 3 de abril de 2026 abierto en SNAP: en **Bands**, las 12 bandas y las carpetas de máscaras y ángulos. Contiene datos modificados de Copernicus Sentinel (2026).
```

## Paso 3. Abrimos la banda B12

Hacemos doble clic en **B12**. En el centro aparece la pestaña `[1] B12` con una imagen en blanco y negro de toda la tesela, 110 × 110 km. Una imagen grande puede tardar unos segundos en dibujarse.

```{figure} ../../images/ch05-snap-b12-tile-2026-04-03.jpg
:label: es-fig-ch05-snap-b12-tile-2026-04-03
:alt: Banda B12 del 3 de abril de 2026: toda la tesela 29TPJ.
:width: 100%

Banda B12 del 3 de abril de 2026: toda la tesela 29TPJ. Contiene datos modificados de Copernicus Sentinel (2026).
```

## Paso 4. Buscamos el lugar del incendio

En esta imagen todavía no se ve lo quemado: el 3 de abril aún no había habido incendio. Lo que buscamos es el lugar.

1. Con la rueda del ratón acercamos la imagen. El incendio está en la parte inferior derecha de la tesela, cerca de su borde sur.
2. Abrimos la pestaña **Pixel Info**, movemos el cursor y seguimos las líneas **Latitude** (latitud) y **Longitude** (longitud).
3. Nos detenemos cerca de **43°20′46″ N, 6°40′30″ W**. Es el centro de lo quemado según el contorno de EFFIS.

SNAP muestra las coordenadas en grados, minutos y segundos. En muchas fuentes, como EFFIS, aparecen en grados decimales: 43,346 y −6,675. Pasar de un formato a otro es sencillo: un grado tiene 60 minutos y un minuto, 60 segundos.

**De grados decimales a grados, minutos y segundos:**

1. La parte entera son los grados: 43,346 → **43°**.
2. Multiplicamos la parte decimal por 60: 0,346 × 60 = 20,76. La parte entera son los minutos: **20′**.
3. Volvemos a multiplicar la parte decimal por 60: 0,76 × 60 = 45,6 ≈ **46″**.

Sale 43°20′46″ N. La letra N indica latitud norte, porque el número es positivo. La longitud −6,675 lleva signo menos, así que está al oeste de Greenwich: 6°; 0,675 × 60 = 40,5 → 40′; 0,5 × 60 = 30″. Sale 6°40′30″ W.

**Al revés:** grados + minutos / 60 + segundos / 3600. Por ejemplo, 43 + 20/60 + 46/3600 = 43,346.

Hay una segunda referencia: el número de píxel. En las líneas **Image-X** e **Image-Y**, SNAP indica qué píxel es contando desde la izquierda y desde arriba. El centro de lo quemado en la banda B12 está más o menos en X = 4420, Y = 4910, de 5490.

## Paso 5. Leemos el número

Ponemos el cursor sobre un píxel en ese lugar y miramos, en la pestaña **Pixel Info**, la línea **B12** del apartado **Bands**. Apuntamos tres cosas:

- el valor de B12;
- la latitud y la longitud del píxel;
- qué tipo de número es: entero o decimal.

```{figure} ../../images/ch05-snap-b12-pixel-info-2026-04-03.jpg
:label: es-fig-ch05-snap-b12-pixel-info-2026-04-03
:alt: Banda B12 cerca del centro de lo quemado; a la izquierda, Pixel Info con las coordenadas del píxel y B12 = 0,12630.
:width: 100%

Banda B12 cerca del centro de lo quemado; a la izquierda, **Pixel Info** con las coordenadas del píxel y B12 = 0,12630. Contiene datos modificados de Copernicus Sentinel (2026).
```

## Paso 6. De dónde ha sacado SNAP ese número

Ahora comprobamos qué ha hecho SNAP con el número del archivo.

1. En **Product Explorer**, hacemos un solo clic en **B12** para seleccionarla.
2. Abrimos el menú **Analysis → Information**.
3. En la lista buscamos tres líneas: **Raw data type**, **Scaling factor** y **Scaling offset**. Apuntamos sus valores.

Después miramos la ficha del producto:

1. En **Product Explorer**, desplegamos **Metadata → Level-2A_User_Product → General_Info → Product_Image_Characteristics**.
2. Abrimos **QUANTIFICATION_VALUES_LIST** y **BOA_ADD_OFFSET_VALUES_LIST**. Apuntamos los valores de **BOA_QUANTIFICATION_VALUE** y **BOA_ADD_OFFSET** para la banda B12.

## Qué ha salido

**La primera parte de la hipótesis se ha cumplido; la segunda, no: en el píxel hay un número decimal, no un entero.**

**Las bandas.** En la carpeta **Bands** hay exactamente 12 bandas: B1–B9, B8A, B11 y B12. B10 no está, como esperábamos. Cada banda aparece una sola vez, con su tamaño de píxel original. Se ve en la ventana **Information**: B12 tiene 5490 × 5490 píxeles (píxel de 20 m), y el producto entero, 10 980 × 10 980 (píxel de 10 m). SNAP guarda en un mismo producto bandas de distinto tamaño.

Aparte de las bandas, en **Bands** hay más carpetas:

- **sun** y **view**: los ángulos del sol y del satélite;
- **quality**: mapas de calidad, entre ellos la clasificación de la escena y la probabilidad de nubes;
- **detector_footprint**, **nodata**, **opaque_clouds**, **cirrus_clouds** y otras: máscaras que indican qué detector tomó cada zona, dónde no hay datos y dónde hay nubes.

**El número del píxel.** Un píxel cerca del centro de lo quemado:

- Image-X = 4425, Image-Y = 4903;
- 43°20′48″ N, 6°40′27″ W;
- **B12 = 0,12630**.

Es un número decimal, no un entero de varios miles. La hipótesis 2 no se ha cumplido.

**Por qué.** La ventana **Information** explica lo que ha pasado:

- **Raw data type: uint16**: en el archivo hay, efectivamente, números enteros de 0 a 65 535;
- **Scaling factor: 1.0E-4**: un multiplicador de 0,0001;
- **Scaling offset: −0.1**: un desplazamiento de −0,1.

SNAP lee del archivo un número entero y lo convierte al momento: lo multiplica por 0,0001 y le resta 0,1. Lo que vemos en pantalla ya es el resultado: la reflectancia.

```{figure} ../../images/ch05-snap-b12-information-2026-04-03.jpg
:label: es-fig-ch05-snap-b12-information-2026-04-03
:alt: Ventana Information de la banda B12: tipo de dato, multiplicador y desplazamiento.
:width: 100%

Ventana **Information** de la banda B12: tipo de dato, multiplicador y desplazamiento.
```

La ficha del producto dice lo mismo con otras palabras: **BOA_QUANTIFICATION_VALUE = 10000** y **BOA_ADD_OFFSET = −1000**. De ahí sale la fórmula:

**reflectancia = (número del archivo − 1000) / 10 000**

Comprobémoslo con nuestro píxel. Hacemos el camino inverso desde lo que muestra SNAP: número del archivo = 0,1263 × 10 000 + 1000 = **2263**. Es un entero de varios miles, justo lo que esperábamos en la hipótesis. Así que en el archivo la hipótesis es correcta, pero SNAP nos muestra el número ya convertido.

**0,1263 significa que la superficie de este píxel refleja alrededor del 13 % de la luz del sol en la banda B12.**

## Si algo falla

1. **En el píxel aparece −0,1.** No es una reflectancia, sino «sin datos»: en el archivo hay un 0, y después de la conversión queda (0 − 1000) / 10 000 = −0,1. Pasa en los bordes de la imagen, donde el satélite no miró. SNAP excluye por sí mismo estos píxeles de los cálculos: lo indica la línea **Valid pixel expression** de la ventana **Information**.
2. **Pixel Info muestra un número, pero no es el de B12.** Miramos justo la línea **B12** del apartado **Bands**: más arriba, en la misma pestaña, están las coordenadas y los números de píxel, y es fácil confundirlos.
3. **Otro programa muestra números enteros.** Si abrimos el archivo `.jp2` con otro programa que no sea SNAP, veremos el número del archivo, por ejemplo 2263. En ese caso, hacemos la conversión nosotros con la fórmula de arriba.

:::{tip} Dato curioso
¿Por qué hay que restar 1000? Sobre superficies oscuras, como el agua, después de la corrección atmosférica la reflectancia a veces sale un poco por debajo de cero. Un número entero sin signo no puede ser negativo, así que el procesador suma 1000 a todos los valores antes de guardarlos en el archivo. Y nosotros, al leerlos, restamos ese 1000.
:::

:::{admonition} Tus datos
Para nuestro propio incendio: abrimos el `MTD_MSIL2A.xml` de nuestra imagen y buscamos nuestras coordenadas en la pestaña **Pixel Info**. Si las tenemos en grados decimales, las pasamos a grados, minutos y segundos. La fórmula de conversión es la misma para todas las imágenes Sentinel-2 L2A, pero los valores del desplazamiento y del multiplicador los comprobamos siempre en la ficha de nuestro producto.
:::

## Resumen

**Términos nuevos**

- **SNAP**: programa gratuito de la Agencia Espacial Europea para trabajar con imágenes Sentinel.
- **Producto** en SNAP: todo el contenido de la carpeta `.SAFE` abierto como una unidad: bandas, máscaras y fichas.
- **Número del archivo** (raw, DN): el número entero que se guarda en el archivo de la banda. Ejemplo: 2263.
- **Reflectancia**: la fracción de la luz del sol que refleja la superficie. Ejemplo: 0,1263, es decir, alrededor del 13 %.
- **Scaling factor y Scaling offset**: el multiplicador y el desplazamiento con los que SNAP convierte el número del archivo en reflectancia. Ejemplo: 1.0E-4 y −0.1.
- **Grados, minutos y segundos**: forma de escribir las coordenadas en la que un grado tiene 60 minutos y un minuto, 60 segundos. Ejemplo: 43°20′46″ N = 43,346.

**Qué recordar**

- En un archivo Sentinel-2 L2A hay un número entero, no una reflectancia.
- Reflectancia = (número del archivo − 1000) / 10 000.
- SNAP hace esta conversión solo y muestra ya la reflectancia.

## Preguntas para un ingeniero

1. Si SNAP hace la conversión solo, ¿para qué necesitamos la fórmula?

:::{dropdown} Respuesta
Porque no todos los programas lo hacen. Si abrimos el archivo en Python o en otro SIG, obtendremos el número del archivo. Si se nos olvida restar 1000, todas las reflectancias saldrán 0,1 más altas de lo que son, y los índices que vamos a calcular serán erróneos.
:::

2. ¿Por qué hay que sacar el desplazamiento y el multiplicador de la ficha, en vez de sabérselos de memoria?

:::{dropdown} Respuesta
Porque dependen de la versión del procesado. El desplazamiento de −1000 apareció en 2022, con la versión 04.00 del procesador; en los productos anteriores no está. La ficha siempre dice la verdad sobre su producto.
:::

3. En el píxel hay 0,1263. ¿Es mucho o poco para la banda B12?

:::{dropdown} Respuesta
De momento no lo sabemos, porque no tenemos con qué comparar. Compararemos como ingenieros: el mismo píxel antes y después del incendio y, al lado, píxeles que no ardieron.
:::


## Ejercicios

1. **Recordar:** ¿qué archivo elegimos en SNAP para abrir todo el producto de una vez?
2. **Corregir:** en la frase «SNAP muestra las bandas B1–B12, 13 bandas en total» hay un error. ¿Cuál?
3. **Repaso de hace tres lecciones (4.1):** ¿para qué dibujamos un marco alrededor de lo quemado antes incluso de empezar a elegir las imágenes?

Las respuestas están en la página [Soluciones](../solutions.md).

## La pregunta que queda abierta

Ya tenemos la reflectancia. Pero en la ficha aparece como BOA, «en la base de la atmósfera» (*bottom of atmosphere*). El satélite vuela a 786 km de altura, y la luz le llega atravesando toda la atmósfera. ¿Cómo ha sabido el procesador cuánta luz reflejó el suelo y cuánta añadió el aire? Lo vemos en la lección 5.3.

---

## Notas y fuentes

- [Copernicus SentiWiki, «S2 Products»](https://sentiwiki.copernicus.eu/web/s2-products) (en inglés): composición del producto L2A y formato SAFE. Consultado el 19/11/2026.
- Ficha del producto `MTD_MSIL2A.xml` de la imagen del 3 de abril de 2026: BOA_QUANTIFICATION_VALUE = 10000, BOA_ADD_OFFSET = −1000.
