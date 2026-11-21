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

1. En SNAP, cada banda aparecerá una sola vez, y no en tres tamaños de píxel, como en las carpetas. En total, 12 bandas: el satélite mide 13, pero B10 no entra en el producto L2A (lección 5.1).
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

En esta imagen todavía no se ve lo quemado: el 3 de abril aún no había habido incendio. Lo que buscamos es el lugar. Para eso necesitamos sus coordenadas.

### De dónde sacamos las coordenadas

Las coordenadas del centro de lo quemado las tomamos del registro de EFFIS sobre nuestro incendio. El número de ese registro es el 294223; ya lo citamos en el prólogo.

1. Abrimos en el navegador la dirección `https://api.effis.emergency.copernicus.eu/rest/2/burntareas/current/294223/`
2. El navegador muestra un texto en formato JSON: es el registro del incendio, con su número, la fecha, la superficie y el contorno.
3. Al principio buscamos la línea `"centroid"`. Es el centro geométrico del contorno de lo quemado. Al lado hay dos números: `[-6.674615360799909, 43.346846622747705]`.

Ojo: en el formato JSON (igual que en GeoJSON) **primero va la longitud y después la latitud**. Así que:

- longitud = −6,674615;
- latitud = 43,346847.

No necesitamos tantos decimales. Cuatro decimales son unos 10 m sobre el terreno, menos de un píxel. Redondeamos: latitud **43,3468**, longitud **−6,6746**.

### Cómo pasarlas a grados, minutos y segundos

SNAP no muestra las coordenadas en grados decimales, sino en grados, minutos y segundos. Hacemos la conversión nosotros. Solo hay una regla: un grado tiene 60 minutos y un minuto, 60 segundos. Por eso, cada vez, multiplicamos la parte decimal por 60.

**Latitud 43,3468:**

1. La parte entera son los grados: **43°**.
2. Multiplicamos la parte decimal por 60: 0,3468 × 60 = 20,808. La parte entera son los minutos: **20′**.
3. Volvemos a multiplicar la parte decimal por 60: 0,808 × 60 = 48,48. Redondeamos al entero y tenemos los segundos: **48″**.

Sale **43°20′48″ N**. La letra N indica latitud norte, porque el número es positivo.

**Longitud −6,6746.** El signo menos significa «al oeste de Greenwich». Hacemos la cuenta sin el signo:

1. Grados: **6°**.
2. 0,6746 × 60 = 40,476 → minutos: **40′**.
3. 0,476 × 60 = 28,56 → segundos: **29″**.

Sale **6°40′29″ W**. La letra W indica longitud oeste.

**Comprobación con la cuenta al revés:** grados + minutos / 60 + segundos / 3600. Para la latitud: 43 + 20/60 + 48/3600 = 43 + 0,3333 + 0,0133 = 43,3466. Coincide con 43,3468, salvo por el redondeo de los segundos.

### Buscamos ese lugar en SNAP

1. Con la rueda del ratón acercamos la imagen. Nuestro punto está en la parte inferior derecha de la tesela, cerca de su borde sur.
2. Abrimos la pestaña **Pixel Info**, movemos el cursor y seguimos las líneas **Latitude** (latitud) y **Longitude** (longitud).
3. Nos detenemos cuando marquen más o menos **43°20′48″ N** y **6°40′29″ W**.

## Paso 5. Leemos el número

Ponemos el cursor sobre un píxel en ese lugar y miramos la pestaña **Pixel Info**. Apuntamos:

- el valor de la línea **B12** del apartado **Bands**;
- las líneas **Latitude** y **Longitude**;
- las líneas **Image-X** e **Image-Y**: el número de píxel;
- las líneas **Map-X** y **Map-Y**: las coordenadas del píxel en metros;
- qué tipo de número aparece en B12: entero o decimal.

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

### Las bandas

En la carpeta **Bands** hay exactamente 12 bandas: B1–B9, B8A, B11 y B12. B10 no está, como esperábamos.

Cada banda aparece una sola vez, con su tamaño de píxel original. Se ve en la ventana **Information**:

- en B12, las líneas **Raster width** y **Raster height** marcan 5490 × 5490 píxeles;
- en el producto entero, las líneas **Product scene width** y **Product scene height** marcan 10 980 × 10 980 píxeles.

Veamos qué significa. Multiplicamos el número de píxeles por el tamaño del píxel:

- 5490 píxeles × 20 m = 109 800 m: es el lado de la tesela en la banda B12;
- 10 980 píxeles × 10 m = 109 800 m: el mismo lado en las bandas con píxel de 10 m.

Es el mismo cuadrado, de unos 110 km. Solo que en B12 está dividido en píxeles de 20 m y, en las bandas de 10 m, en píxeles el doble de pequeños. Así que SNAP guarda en un mismo producto bandas de distinto tamaño, cada una con el suyo.

Aparte de las bandas, en **Bands** hay más carpetas:

- **sun** y **view**: los ángulos del sol y del satélite;
- **quality**: mapas de calidad, entre ellos la clasificación de la escena y la probabilidad de nubes;
- **detector_footprint**, **nodata**, **opaque_clouds**, **cirrus_clouds** y otras: máscaras que indican qué detector tomó cada zona, dónde no hay datos y dónde hay nubes.

### El número del píxel

El píxel cerca del centro de lo quemado, tal como lo muestra **Pixel Info**:

- Latitude 43°20′48″ N, Longitude 6°40′27″ W: a dos segundos del punto de EFFIS;
- Image-X = 4425, Image-Y = 4903;
- Map-X = 688 510 m, Map-Y = 4 801 950 m;
- **B12 = 0,12630**.

Es un número decimal, no un entero de varios miles. La hipótesis 2 no se ha cumplido.

### Cómo se relacionan el número de píxel y los metros

Vamos a comprobar el número de píxel nosotros mismos. Para eso necesitamos la esquina de la tesela.

**De dónde la sacamos.** Abrimos el archivo `MTD_TL.xml` (la ficha de la tesela, lección 5.1) en cualquier editor de texto o en el navegador. Buscamos la línea `Geoposition resolution="20"`: es la rejilla con píxel de 20 m. Debajo hay cuatro valores:

- `ULX` = 600000: la coordenada X de la esquina superior izquierda de la tesela, en metros;
- `ULY` = 4900020: la coordenada Y de esa misma esquina;
- `XDIM` = 20: el paso del píxel en X, 20 m;
- `YDIM` = −20: el paso en Y. Es negativo porque los números de píxel crecen de arriba abajo, mientras que la coordenada Y crece de abajo arriba.

Las coordenadas están en la proyección UTM, huso 29 del hemisferio norte (en la ficha: `EPSG:32629`). Es el mismo sistema en el que SNAP muestra Map-X y Map-Y.

**La fórmula.** ¿Cuántos metros hay desde el borde izquierdo de la tesela hasta nuestro píxel? Map-X − ULX. ¿Cuántos píxeles son? Lo dividimos entre el tamaño del píxel:

- Image-X = (Map-X − ULX) / 20
- Image-Y = (ULY − Map-Y) / 20. Aquí es al revés, porque contamos hacia abajo desde el borde superior.

**El cálculo:**

- Image-X = (688 510 − 600 000) / 20 = 88 510 / 20 = **4425,5**
- Image-Y = (4 900 020 − 4 801 950) / 20 = 98 070 / 20 = **4903,5**

El medio píxel indica que Map-X y Map-Y son las coordenadas del **centro** del píxel. El píxel número 4425 ocupa el tramo de 4425,0 a 4426,0, y su centro está en 4425,5. Coincide con lo que muestra SNAP: Image-X = 4425, Image-Y = 4903.

```{figure} ../../images/ch05-snap-b12-information-2026-04-03.jpg
:label: es-fig-ch05-snap-b12-information-2026-04-03
:alt: Ventana Information de la banda B12: tipo de dato, multiplicador y desplazamiento.
:width: 100%

Ventana **Information** de la banda B12: tipo de dato, multiplicador y desplazamiento.
```

### Por qué en el píxel hay un número decimal

La ventana **Information** explica lo que ha pasado:

- **Raw data type: uint16**: en el archivo hay números enteros sin signo, guardados en 16 bits. Con 16 bits hay 2¹⁶ = 65 536 valores posibles, es decir, números de 0 a 65 535.
- **Scaling factor: 1.0E-4**: el multiplicador. La notación 1.0E-4 significa 1,0 × 10⁻⁴ = 0,0001.
- **Scaling offset: −0.1**: un desplazamiento de −0,1.

SNAP lee del archivo un número entero y lo convierte al momento:

**reflectancia = número del archivo × 0,0001 − 0,1**

Lo que vemos en pantalla ya es el resultado: la reflectancia.

### La misma fórmula en la ficha

La ficha del producto dice lo mismo con otras palabras:

- **BOA_QUANTIFICATION_VALUE = 10000**: por cuánto se multiplicó la reflectancia para guardarla como número entero;
- **BOA_ADD_OFFSET = −1000**: lo que hay que sumar al número del archivo antes de dividir.

De ahí sale la fórmula:

**reflectancia = (número del archivo + BOA_ADD_OFFSET) / BOA_QUANTIFICATION_VALUE = (número del archivo − 1000) / 10 000**

Por qué funciona así:

1. **Por qué se multiplica por 10 000.** La reflectancia es un número decimal entre 0 y 1. Guardar números enteros es más sencillo y ocupa menos que guardar decimales. Si multiplicamos 0,1263 por 10 000, sale 1263: un número entero, y no perdemos ninguno de los cuatro decimales.
2. **Por qué se suma 1000.** Sobre superficies muy oscuras, como el agua, después de la corrección atmosférica la reflectancia a veces sale un poco por debajo de cero. Un número entero sin signo no puede ser negativo. Por eso, desde el 25 de enero de 2022 (versión del procesado 04.00), se suma 1000 a todos los valores antes de guardarlos y se resta al leerlos[^offset].

Es la misma fórmula que usa SNAP. Si quitamos el paréntesis:

(número − 1000) / 10 000 = número / 10 000 − 1000 / 10 000 = número × 0,0001 − 0,1

### Comprobación con nuestro píxel

SNAP ha mostrado una reflectancia de 0,1263. ¿Qué número hay en el archivo? Recorremos la fórmula al revés:

1. reflectancia = (número − 1000) / 10 000
2. multiplicamos los dos lados por 10 000: reflectancia × 10 000 = número − 1000
3. sumamos 1000: número = reflectancia × 10 000 + 1000

Sustituimos: 0,1263 × 10 000 + 1000 = 1263 + 1000 = **2263**.

Es un entero de varios miles, justo lo que esperábamos en la hipótesis. Así que en el archivo la hipótesis es correcta, pero SNAP nos muestra el número ya convertido.

### Qué significa 0,1263

La reflectancia es una fracción de la luz. Para pasarla a porcentaje, la multiplicamos por 100: 0,1263 × 100 = 12,63 %. **La superficie de este píxel refleja alrededor del 13 % de la luz del sol en la banda B12.**

## Si algo falla

1. **En el píxel aparece −0,1.** No es una reflectancia, sino «sin datos». En esos píxeles, el archivo guarda un 0. Si lo metemos en la fórmula: (0 − 1000) / 10 000 = −0,1. Pasa en los bordes de la imagen, donde el satélite no miró. SNAP excluye por sí mismo estos píxeles de los cálculos: lo indica la línea **Valid pixel expression** de la ventana **Information**.
2. **Pixel Info muestra un número, pero no es el de B12.** Miramos justo la línea **B12** del apartado **Bands**. Más arriba, en la misma pestaña, están las coordenadas y los números de píxel, y es fácil confundirlos.
3. **Otro programa muestra números enteros.** Si abrimos el archivo `.jp2` con otro programa que no sea SNAP, veremos el número del archivo, por ejemplo 2263. En ese caso, hacemos la conversión nosotros con la fórmula de arriba.

:::{admonition} Tus datos
Para nuestro propio incendio:

1. buscamos el número de nuestro incendio en EFFIS y abrimos su registro en la misma dirección, cambiando el número por el nuestro;
2. cogemos `"centroid"` (primero la longitud, después la latitud) y lo pasamos a grados, minutos y segundos;
3. abrimos el `MTD_MSIL2A.xml` de nuestra imagen y buscamos ese punto en la pestaña **Pixel Info**.

La fórmula de conversión es la misma para todas las imágenes Sentinel-2 L2A desde 2022, pero los valores del multiplicador y del desplazamiento los comprobamos siempre en la ficha de nuestro producto.
:::

## Resumen

**Términos nuevos**

- **SNAP**: programa gratuito de la Agencia Espacial Europea para trabajar con imágenes Sentinel.
- **Producto** en SNAP: todo el contenido de la carpeta `.SAFE` abierto como una unidad: bandas, máscaras y fichas.
- **Número del archivo** (raw, DN): el número entero que se guarda en el archivo de la banda. Ejemplo: 2263.
- **Reflectancia**: la fracción de la luz del sol que refleja la superficie. Ejemplo: 0,1263, es decir, alrededor del 13 %.
- **Scaling factor y Scaling offset**: el multiplicador y el desplazamiento con los que SNAP convierte el número del archivo en reflectancia. Ejemplo: 1.0E-4 y −0.1.
- **Grados, minutos y segundos**: forma de escribir las coordenadas en la que un grado tiene 60 minutos y un minuto, 60 segundos. Ejemplo: 43°20′48″ N = 43,3468.
- **UTM**: sistema de coordenadas en metros en el que están las teselas de Sentinel-2. Ejemplo: nuestra tesela está en el huso 29 del hemisferio norte, `EPSG:32629`.

**Qué recordar**

- En un archivo Sentinel-2 L2A hay un número entero, no una reflectancia.
- Reflectancia = (número del archivo − 1000) / 10 000.
- SNAP hace esta conversión solo y muestra ya la reflectancia.
- El número de píxel se puede comprobar con sus coordenadas en metros y con la esquina de la tesela que da `MTD_TL.xml`.

## Preguntas para un ingeniero

1. Si SNAP hace la conversión solo, ¿para qué necesitamos la fórmula?

:::{dropdown} Respuesta
Porque no todos los programas lo hacen. Si abrimos el archivo en Python o en otro SIG, obtendremos el número del archivo. Si se nos olvida restar 1000, todas las reflectancias saldrán 1000 / 10 000 = 0,1 más altas de lo que son, y los índices que vamos a calcular serán erróneos.
:::

2. ¿Por qué hay que sacar el multiplicador y el desplazamiento de la ficha, en vez de sabérselos de memoria?

:::{dropdown} Respuesta
Porque dependen de la versión del procesado. El desplazamiento apareció con la versión 04.00, en enero de 2022; en los productos anteriores no está, y para ellos la fórmula es otra: número / 10 000. La ficha siempre dice la verdad sobre su producto.
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

- Copernicus SentiWiki, «S2 Products» (en inglés): composición del producto L2A y formato SAFE. https://sentiwiki.copernicus.eu/web/s2-products (consultado el 19/11/2026)
- EFFIS, registro de superficie quemada 294223 (Allande): centro del contorno. https://api.effis.emergency.copernicus.eu/rest/2/burntareas/current/294223/ (consultado el 21/11/2026)
- Ficha del producto `MTD_MSIL2A.xml` y ficha de la tesela `MTD_TL.xml` de la imagen del 3 de abril de 2026: BOA_QUANTIFICATION_VALUE = 10000, BOA_ADD_OFFSET = −1000; esquina de la tesela ULX = 600000, ULY = 4900020.
[^offset]: ESA, «Copernicus Sentinel-2: Major Products Upgrade Upcoming» (en inglés): el desplazamiento se añadió para no perder los valores negativos sobre superficies oscuras. https://sentinels.copernicus.eu/-/copernicus-sentinel-2-major-products-upgrade-upcoming ; foro ESA STEP, «Introduction of additional Radiometric Offset in PB04.00 products»: desplazamiento de −1000 en los productos L1C y L2A desde el 25 de enero de 2022. https://forum.step.esa.int/t/info-introduction-of-additional-radiometric-offset-in-pb04-00-products/35431 (consultado el 21/11/2026)
