---
title: "5.3. Qué ha hecho la atmósfera"
---

## Dónde lo dejamos

En la lección 5.2 leímos, en un píxel cerca del centro de lo quemado, B12 = 0,1263. En la ficha, esta reflectancia aparece como BOA, *bottom of atmosphere*, «en la base de la atmósfera». Es decir, así refleja la propia superficie, como si no hubiera aire entre ella y el satélite.

Pero el satélite vuela a 786 km de altura, y la luz le llega atravesando toda la atmósfera. En esta lección vemos qué le hace el aire a la luz y cuánto ha cambiado el procesador los números para quitar su efecto.

## Qué le hace la atmósfera a la luz

La luz atraviesa el aire dos veces: del sol al suelo y del suelo al satélite. Por el camino le pasan dos cosas distintas.

1. **Dispersión.** Las moléculas del aire y las gotitas de la bruma desvían parte de la luz hacia los lados, también directamente hacia el objetivo del satélite. El satélite recibe luz que ni siquiera llegó al suelo. La que más se dispersa es la luz de onda corta, la azul. Por eso el cielo es azul y las montañas lejanas se ven azuladas.
2. **Absorción.** El vapor de agua, el ozono y otros gases se quedan con parte de la luz en ciertas longitudes de onda. Al satélite le llega menos de lo que reflejó el suelo.

De ahí salen dos niveles de procesado de Sentinel-2:

- **L1C**: la reflectancia en la cima de la atmósfera, TOA (*top of atmosphere*). Es lo que ve el satélite, con el aire incluido;
- **L2A**: la reflectancia en la superficie, BOA. El procesador Sen2Cor ha quitado la dispersión y la absorción.

Para quitar el aire, el procesador necesita saber cuánto había. Para eso calcula él mismo, a partir de la imagen, dos mapas que ya vimos en la lección 5.1: `AOT` (cuánta bruma, es decir, cuántos aerosoles) y `WVP` (cuánto vapor de agua).

## Qué queremos saber

**La pregunta:** ¿cuánto cambia la atmósfera el número de un píxel? ¿Y lo cambia igual en todas las bandas?

**Nuestra hipótesis antes de empezar:**

1. En la banda azul B2, la reflectancia de L1C será **mayor** que la de L2A. El aire dispersa la luz azul y la suma a la que reflejó el suelo.
2. En la banda B12, la diferencia entre L1C y L2A será **mucho menor** que en B2. Las ondas largas atraviesan el aire casi sin dispersarse.

**Cómo sabremos que nos hemos equivocado:** si en B2 la de L1C sale menor que la de L2A, o si la diferencia en B12 es igual que en B2 o mayor.

## Paso 1. Descargamos la imagen L1C de la misma fecha

1. En Copernicus Browser, abrimos la pestaña **Search**.
2. En la lista de fuentes de datos dejamos solo **Sentinel-2** y, dentro, marcamos **L1C**. Quitamos las marcas de L2A y de otros satélites.
3. Ponemos la fecha del **3 de abril de 2026** y pulsamos **Search**.
4. En la lista aparecen dos productos, como en la lección 5.1: las teselas 29TPH y 29TPJ. Cogemos la **29TPJ**: `S2B_MSIL1C_20260403T112109_N0512_R037_T29TPJ_20260403T152544.SAFE`. En la lista aparece con un tamaño de **611 MB**.
5. La descargamos en la misma carpeta `data/sentinel2` y la descomprimimos.

La hora de la toma que aparece en la lista es 11:21:09 UTC, la misma que la de nuestro L2A. Es la misma imagen, de la misma pasada del satélite. Solo cambia el procesado.

```{figure} ../../images/ch05-search-l1c-2026-04-03.jpg
:label: es-fig-ch05-search-l1c-2026-04-03
:alt: Búsqueda de Sentinel-2 L1C del 3 de abril de 2026: dos productos, teselas 29TPH y 29TPJ; elegimos 29TPJ (611 MB).
:width: 100%

Búsqueda de Sentinel-2 L1C del 3 de abril de 2026: dos productos, teselas 29TPH y 29TPJ; elegimos 29TPJ (611 MB). Contiene datos modificados de Copernicus Sentinel (2026).
```

## Paso 2. Abrimos los dos productos en SNAP

1. **File → Open Product…** y abrimos `MTD_MSIL1C.xml` desde la nueva carpeta L1C.
2. Si el L2A no está abierto, lo abrimos también: `MTD_MSIL2A.xml`, como en la lección 5.2.

Ahora en **Product Explorer** hay dos productos: `[1]` y `[2]`. Por el nombre vemos cuál es `MSIL1C` y cuál `MSIL2A`.

## Paso 3. Ponemos una marca en el mismo punto de los dos productos

Para comparar con honestidad, necesitamos el mismo píxel en los dos productos. Con el cursor no se acierta exactamente en el mismo punto. Para eso, SNAP tiene las marcas (*pins*): puntos con coordenadas exactas.

Las coordenadas las tomamos del registro de EFFIS, como en la lección 5.2: latitud 43,3468, longitud −6,6746. En la ventana de SNAP las escribimos así: `43.3468` y `-6.6746`, con punto y con el guion normal del teclado.

1. Abrimos la banda **B2** del producto L2A con un doble clic.
2. Abrimos **View → Tool Windows → Pin Manager**.
3. En **Pin Manager**, pulsamos el botón **New pin** (el icono con el signo más).
4. En la ventana que se abre, escribimos **Lat** = `43.3468` y **Lon** = `-6.6746`. Pulsamos **OK**.
5. Abrimos la banda **B2** del producto L1C y repetimos los puntos 3 y 4 para él.

## Paso 4. Leemos la reflectancia en la marca

En **Pin Manager** hay un botón **Filter pixel data to be displayed in table** (el icono del embudo). Lo pulsamos. Se abre la lista de todas las capas del producto. Las bandas están al principio. Marcamos **B2** y **B12** y pulsamos **OK**. En la tabla de marcas aparecen sus valores en el punto de la marca.

Lo hacemos en los dos productos. En el producto L2A marcamos además **quality_aot** y **quality_wvp**: nos harán falta en el paso 6.

## Paso 5. Comprobamos que SNAP ha convertido los números igual

En la lección 5.2 vimos que SNAP convierte solo el número del archivo en reflectancia, con la fórmula de la ficha. En el L1C comprobamos lo mismo: solo se pueden restar números que estén en las mismas unidades.

1. En **Product Explorer**, seleccionamos **B2** del producto L1C y abrimos **Analysis → Information**. Apuntamos **Scaling factor** y **Scaling offset**.
2. Abrimos la ficha del L1C: **Metadata → Level-1C_User_Product → General_Info → Product_Image_Characteristics**. Apuntamos **QUANTIFICATION_VALUE**. Desplegamos **Radiometric_Offset_List** y apuntamos los valores de **RADIO_ADD_OFFSET**.

## Paso 6. Cuánta bruma y cuánto vapor había

En la tabla de marcas del producto L2A ya están **quality_aot** y **quality_wvp**. Apuntamos sus valores. Después comprobamos en qué unidades están:

1. En **Product Explorer**, seleccionamos **quality_aot** y abrimos **Analysis → Information**. Apuntamos **Geophysical unit** y **Scaling factor**.
2. Hacemos lo mismo con **quality_wvp**.
3. En la ficha del L2A, en **Product_Image_Characteristics → QUANTIFICATION_VALUES_LIST**, buscamos **AOT_QUANTIFICATION_VALUE** y **WVP_QUANTIFICATION_VALUE**.

En el producto L1C no hay estas capas. Las calcula el procesador Sen2Cor cuando convierte el L1C en un producto L2A. Antes de ese procesado, sencillamente no existen.

## Cómo vamos a calcular

Con los números apuntados, calculamos dos cosas para cada banda.

**1. La diferencia:** cuánto ha sumado o restado la atmósfera.

diferencia = TOA − BOA

Si la diferencia es positiva, el satélite vio más luz de la que reflejó el suelo: el aire la añadió. Si es negativa, al satélite le llegó menos luz.

**2. La diferencia en porcentaje:** cuánto supone comparada con la propia reflectancia del suelo.

diferencia en % = (TOA − BOA) / BOA × 100 %

¿Para qué el segundo número? Una diferencia de 0,02 en una superficie oscura con reflectancia de 0,04 es la mitad de la señal. En una superficie clara con reflectancia de 0,4 es solo una vigésima parte. El porcentaje muestra cuánto se equivocaría quien usara L1C en lugar de L2A.

## Qué ha salido

**La primera parte de la hipótesis se ha cumplido. La segunda, no, y es lo más interesante de la lección.**

### Los números que hemos obtenido

La marca está en el mismo punto en los dos productos: Lon −6,674600, Lat 43,346800. **Pin Manager** muestra:

| | B2 | B12 |
|---|---|---|
| L1C (TOA) | 0,1213 | 0,166 |
| L2A (BOA) | 0,0848 | 0,198 |

### ¿Se pueden comparar?

Sí. En el L1C, la ventana **Information** de B2 muestra **Scaling factor 1.0E-4** y **Scaling offset −0.1**. En la ficha del L1C: **QUANTIFICATION_VALUE = 10000** y todos los **RADIO_ADD_OFFSET = −1000**. Es la misma fórmula que la del L2A en la lección 5.2:

reflectancia = (número del archivo − 1000) / 10 000

Así que los dos productos se muestran en las mismas unidades, como reflectancias. Se pueden restar.

Para comprobarlo, buscamos los números de los archivos, como en la lección 5.2: número = reflectancia × 10 000 + 1000.

- L1C, B2: 0,1213 × 10 000 + 1000 = 1213 + 1000 = 2213
- L2A, B2: 0,0848 × 10 000 + 1000 = 848 + 1000 = 1848
- L1C, B12: 0,166 × 10 000 + 1000 = 1660 + 1000 = 2660
- L2A, B12: 0,198 × 10 000 + 1000 = 1980 + 1000 = 2980

Enteros de varios miles, como debe ser.

### El cálculo para B2

1. Diferencia: 0,1213 − 0,0848 = **0,0365**.
2. En porcentaje: 0,0365 / 0,0848 × 100 % = 0,4304 × 100 % ≈ **43 %**.

La diferencia es positiva: en la banda azul, el satélite vio un 43 % más de luz de la que reflejó el suelo. **La hipótesis 1 se ha cumplido.** La mayor parte de esa diferencia es luz que dispersó la propia atmósfera. Pero en B2 actúa además otra corrección, que veremos un poco más abajo, al analizar B12.

### El cálculo para B12

1. Diferencia: 0,166 − 0,198 = **−0,032**.
2. En porcentaje: −0,032 / 0,198 × 100 % = −0,1616 × 100 % ≈ **−16 %**.

La diferencia es negativa: en la superficie, la reflectancia es **mayor** que la que vio el satélite. Y su tamaño es casi el mismo que en B2: 0,032 frente a 0,0365. **La hipótesis 2 no se ha cumplido.** Esperábamos que en B12 el procesador apenas cambiara nada. Pero el satélite vio en B12 un 16 % menos de lo que salió en la superficie después del procesado.

### Por qué en B12 sale así

Miremos las propias imágenes. Abrimos una junto a otra la banda B2 del L1C y la del L2A (figura). En el L1C se ven bien las laderas: un lado de cada cordal está claro y el otro, oscuro. En el L2A ese claroscuro es mucho más débil; el relieve parece suavizado.

```{figure} ../../images/ch05-snap-pin-l1c-b2-2026-04-03.jpg
:label: es-fig-ch05-snap-pin-l1c-b2-2026-04-03
:alt: Banda B2 del 3 de abril de 2026: a la izquierda L2A, a la derecha L1C, con la misma marca. En L1C las laderas se ven mucho más contrastadas. Abajo, la tabla de la marca en L1C: B2 = 0,1213, B12 = 0,166.
:width: 100%

Banda B2 del 3 de abril de 2026: a la izquierda L2A, a la derecha L1C, con la misma marca. En L1C las laderas se ven mucho más contrastadas. Abajo, la tabla de la marca en L1C: B2 = 0,1213, B12 = 0,166. Contiene datos modificados de Copernicus Sentinel (2026).
```

Es la segunda parte del trabajo del procesador, de la que todavía no hemos hablado. Además de la atmósfera, Sen2Cor corrige también la **iluminación de las laderas**: con el modelo digital del terreno sabe con qué ángulo ilumina el sol cada píxel. A la ladera que da la espalda al sol le sube la reflectancia, y a la que mira al sol se la baja. El objetivo es que una misma superficie dé el mismo número en cualquier ladera.

En nuestro píxel de B12 actúan a la vez dos correcciones:

- la atmosférica: en B12 es pequeña, porque casi no hay dispersión;
- la corrección por la ladera: actúa en todas las bandas y puede ser grande.

Con dos números en un solo píxel no podemos decir cuál de las dos ha dado el −16 %. Pero la imagen muestra que la corrección del relieve funciona, y de forma notable. Y en el prólogo ya leímos que, en las laderas oscuras, esta corrección a veces se pasa. **Para nuestra segunda pregunta de investigación esto es importante: el L2A ya incluye una corrección de la iluminación, y tenemos que tenerla en cuenta.** Nos ocuparemos de ello a fondo en el capítulo 7.

### Cuánta bruma y cuánto vapor había

En la misma marca del L2A:

- **quality_aot = 0,147**;
- **quality_wvp = 0,819**.

```{figure} ../../images/ch05-snap-pin-l2a-aot-wvp-2026-04-03.jpg
:label: es-fig-ch05-snap-pin-l2a-aot-wvp-2026-04-03
:alt: Tabla de la marca en L2A: B2 = 0,0848, B12 = 0,198, quality_aot = 0,147, quality_wvp = 0,819.
:width: 100%

Tabla de la marca en L2A: B2 = 0,0848, B12 = 0,198, quality_aot = 0,147, quality_wvp = 0,819. Contiene datos modificados de Copernicus Sentinel (2026).
```

**De dónde salen estos números y en qué unidades están.** En la ventana **Information**, las dos capas tienen **Scaling factor 0.001** y **Scaling offset 0.0**. En la ficha del L2A: **AOT_QUANTIFICATION_VALUE = 1000** y **WVP_QUANTIFICATION_VALUE = 1000**; en el vapor, la unidad es el centímetro. La fórmula es la misma en esencia, solo que sin desplazamiento:

valor = número del archivo / 1000

Los números de los archivos: 0,147 × 1000 = 147 y 0,819 × 1000 = 819.

**Qué significa AOT = 0,147.** AOT es el espesor óptico de los aerosoles, es decir, de la bruma, a una longitud de onda de 550 nm (luz verde). No es un espesor en metros, sino una medida de cuánta luz no deja pasar la bruma. La fracción de luz que atraviesa la bruma en línea recta, en vertical de arriba abajo, es e^(−AOT), donde e ≈ 2,718. Lo calculamos con la calculadora:

e^(−0,147) = 1 / e^0,147 = 1 / 1,158 = **0,863**

Así que alrededor del 86 % de la luz directa atravesó la bruma, y alrededor del 14 % se dispersó o se absorbió. El 3 de abril el aire estaba bastante limpio, aunque no del todo.

**Qué significa WVP = 0,819 cm.** Si todo el vapor de agua que hay sobre este píxel, desde el suelo hasta la cima de la atmósfera, se condensara en agua, formaría una capa de 0,819 cm de espesor, es decir, de unos 8 mm.

## Si algo falla

1. **En los resultados de la búsqueda aparece Sentinel-1, no Sentinel-2.** Si en la búsqueda está marcado Sentinel-1, en la lista saldrán productos con nombres `S1A_…`, `S1C_…` y con el instrumento SAR. Es un satélite radar: toma las imágenes a otra hora y no mide la luz del sol. Dejamos en la búsqueda solo Sentinel-2 L1C. Por las primeras letras del nombre del producto siempre se ve qué satélite es: `S2` es Sentinel-2 y `S1`, Sentinel-1.
2. **El número de B12 no coincide con el de la lección 5.2.** En la lección 5.2, B12 valía 0,1263, y aquí, en el L2A, vale 0,198. Son píxeles distintos. La marca está en el punto X = 8847,3, Y = 9806,6 (columnas X e Y de **Pin Manager**). Son números de la rejilla de 10 m. La banda B12 está en la rejilla de 20 m, con píxeles el doble de grandes, así que dividimos entre 2: 8847,3 / 2 = 4423,65 → píxel **4423**; 9806,6 / 2 = 4903,3 → píxel **4903**. En la lección 5.2 era el píxel 4425, 4903. La diferencia es de 2 píxeles en X, es decir, 40 m. En la montaña, en 40 m puede cambiar la ladera o la vegetación. Por eso solo comparamos números en el mismo punto: para eso sirven las marcas.
3. **En la tabla de marcas no aparecen quality_aot ni quality_wvp.** Eso significa que la marca está en el producto L1C, que no tiene esas capas. Abrimos **Pin Manager** en el producto L2A.

:::{admonition} Tus datos
Para nuestro propio incendio, descargamos el L1C de la misma fecha y la misma tesela que el L2A, y ponemos una marca en nuestro punto: las coordenadas las sacamos del `"centroid"` de nuestro registro de EFFIS. El píxel tiene que ser el mismo en los dos productos; si no, la comparación no es honesta.
:::

## Resumen

**Términos nuevos**

- **TOA** (*top of atmosphere*): la reflectancia en la cima de la atmósfera, tal como la ve el satélite. Nivel L1C. Ejemplo: B2 = 0,1213.
- **BOA** (*bottom of atmosphere*): la reflectancia en la superficie, sin el efecto del aire. Nivel L2A. Ejemplo: B2 = 0,0848.
- **Dispersión**: el aire desvía parte de la luz hacia los lados; la que más, la azul.
- **Absorción**: los gases se quedan con parte de la luz en ciertas longitudes de onda.
- **Corrección atmosférica**: la conversión de TOA en BOA. En Sentinel-2 la hace el procesador Sen2Cor.
- **AOT**: el espesor óptico de los aerosoles, es decir, cuánta luz no deja pasar la bruma. Ejemplo: 0,147, de modo que pasa alrededor del 86 % de la luz directa.
- **WVP**: el vapor de agua en la columna de aire, en centímetros de agua. Ejemplo: 0,819 cm.
- **Corrección del relieve**: el recálculo de la reflectancia teniendo en cuenta cómo ilumina el sol la ladera.
- **Marca** (*pin*) en SNAP: un punto con coordenadas exactas en el que se pueden leer los valores de distintas capas y productos.

**Qué recordar**

- La atmósfera cambia sobre todo la banda azul: en nuestro punto, B2 en la cima de la atmósfera es un 43 % mayor que en la superficie.
- El L2A no es solo la corrección atmosférica, sino también la corrección de la iluminación de las laderas. En la montaña, puede cambiar los números tanto como la atmósfera, o más.
- Solo comparamos productos en el mismo punto y en las mismas unidades.

## Preguntas para un ingeniero

1. ¿Por qué usamos el L2A, y no el L1C, para calcular lo quemado?

:::{dropdown} Respuesta
En el L1C, la reflectancia del suelo lleva mezclada luz de la atmósfera, y cada día en una cantidad distinta, porque la bruma y el vapor cambian. Si comparamos «antes» y «después» con el L1C, parte de la diferencia será solo una diferencia de tiempo atmosférico. En el L2A esa aportación está eliminada.
:::

2. ¿Por qué calculamos también la diferencia en porcentaje?

:::{dropdown} Respuesta
Una misma diferencia significa cosas distintas en una superficie oscura y en una clara. En nuestro punto, la diferencia en B2 es de 0,0365, y eso es el 43 % de la reflectancia del suelo. En una superficie con reflectancia de 0,4, esos mismos 0,0365 serían alrededor del 9 %.
:::

3. En B12, el L2A ha salido mayor que el L1C. ¿Significa que el procesador se ha equivocado?

:::{dropdown} Respuesta
No necesariamente. El procesador también corrige la iluminación de las laderas, y en un píxel de una ladera en sombra la reflectancia sube después de la corrección. Para saber si esa corrección es correcta, hay que comparar una misma superficie en laderas con orientaciones distintas. De eso nos ocuparemos en el capítulo 7.
:::


## Ejercicios

1. **Recordar:** ¿qué significan las siglas TOA y BOA, y a qué nivel de procesado corresponde cada una?
2. **Corregir:** en la frase «La atmósfera dispersa sobre todo la luz de la banda B12, porque es la que tiene la onda más larga» hay un error. ¿Cuál?
3. **Repaso de hace siete lecciones (capítulo 1):** ¿por qué, en color natural, es fácil confundir lo quemado con la sombra de una nube?

Las respuestas están en la página [Soluciones](../solutions.md).

## La pregunta que queda abierta

Ahora sabemos que en cada píxel del L2A hay una reflectancia en la superficie, ya corregida por la atmósfera y por la ladera. Sabemos leerla en un punto. Pero lo quemado son miles de píxeles. ¿Cómo mostramos las imágenes de «antes» y «después» para que lo quemado se vea entero y la comparación sea honesta: las mismas bandas, el mismo brillo y el mismo contraste? De eso trata el capítulo 6.

---

## Notas y fuentes

- Fichas de los productos `MTD_MSIL1C.xml` y `MTD_MSIL2A.xml` de la imagen del 3 de abril de 2026: QUANTIFICATION_VALUE = 10000, RADIO_ADD_OFFSET = −1000 (L1C); AOT_QUANTIFICATION_VALUE = 1000, WVP_QUANTIFICATION_VALUE = 1000 (L2A).
- ESA, *Sen2Cor Level-2A Algorithm Theoretical Basis Document*, v2.10 (en inglés): corrección atmosférica, AOT y vapor de agua, corrección del relieve con el modelo digital del terreno. https://step.esa.int/thirdparties/sen2cor/2.10.0/docs/S2-PDGS-MPC-L2A-ATBD-V2.10.0.pdf
- Copernicus SentiWiki, «S2 Processing» (en inglés): niveles de procesado L1C y L2A, AOT y vapor de agua. https://sentiwiki.copernicus.eu/web/s2-processing (consultado el 19/11/2026)
