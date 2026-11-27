---
title: "6.1. Por qué una misma ladera sale de distinto color"
---

## Dónde lo dejamos

Abrimos en SNAP las imágenes del 3 y del 10 de abril con la composición B8A–B11–B12, y el 10 de abril lo quemado se ve como una mancha azul. Pero en las imágenes hay algo raro. La del 3 de abril tiene un tono azulado, y la del 10 de abril, verde anaranjado. Y eso que en siete días solo ardió la zona de Bustantigo; todo lo demás debería seguir igual.

Vamos a ver de dónde sale esa diferencia. Si no la entendemos, cualquier comparación a ojo entre «antes» y «después» nos engañará.

## Qué queremos saber

**La pregunta:** ¿por qué el terreno que no ha ardido sale de distinto color en las dos imágenes?

**Nuestra hipótesis antes de empezar:**

1. El terreno apenas ha cambiado. Su reflectancia es más o menos la misma en las dos imágenes.
2. El color distinto lo ha puesto el propio SNAP: ha ajustado el brillo y el contraste de cada imagen por separado, según sus propios números.

**Cómo sabremos que nos hemos equivocado:** si en un mismo punto fuera de lo quemado la reflectancia de las bandas es claramente distinta en las dos imágenes. O si SNAP muestra las dos imágenes con los mismos ajustes de brillo.

## Cómo muestra la pantalla la reflectancia

Primero recordemos la lección 3.1. En la pantalla, cada punto tiene tres bombillas: una roja, una verde y una azul. El brillo de cada una es un número de 0 (apagada) a 255 (encendida del todo). La reflectancia de una banda, en cambio, es un número decimal, normalmente entre 0 y 0,5. El programa tiene que pasar de uno a otro.

Para eso elige dos números para cada banda: **min** y **max**.

- Una reflectancia igual a **min** o menor → la bombilla está apagada (0).
- Una reflectancia igual a **max** o mayor → la bombilla está encendida del todo (255).
- Todo lo que queda entre los dos se reparte a partes iguales.

La fórmula es esta:

**brillo = (reflectancia − min) / (max − min) × 255**

Por qué es así. Primero restamos min: así, una reflectancia igual a min se convierte en 0. Después dividimos entre (max − min), es decir, entre el ancho del intervalo: así, una reflectancia igual a max se convierte en 1, y todo lo que hay entre medias, en una fracción entre 0 y 1. Esa fracción indica qué parte del camino entre min y max ha recorrido nuestra reflectancia. Por último, multiplicamos por 255 para pasar a la escala de la bombilla.

Si sale menos de 0, nos quedamos con 0. Si sale más de 255, con 255.

Esto se llama **estiramiento del contraste** (*contrast stretch*): estiramos un intervalo estrecho de reflectancias hasta ocupar toda la escala de brillo de la pantalla.

**Un ejemplo con números inventados.** Supongamos una reflectancia de 0,20, con min = 0,05 y max = 0,35:

- reflectancia − min = 0,20 − 0,05 = 0,15;
- max − min = 0,35 − 0,05 = 0,30;
- 0,15 / 0,30 = 0,5;
- 0,5 × 255 = 127,5 ≈ **128**: la bombilla brilla a la mitad.

Ahora tomemos la misma reflectancia de 0,20, pero con min = 0,10 y max = 0,25:

- reflectancia − min = 0,20 − 0,10 = 0,10;
- max − min = 0,25 − 0,10 = 0,15;
- 0,10 / 0,15 ≈ 0,667;
- 0,667 × 255 ≈ **170**: la bombilla brilla bastante más.

**La reflectancia es la misma, pero el color en pantalla es distinto.** Todo depende de qué min y qué max se elijan.

## Paso 1. Abrimos las dos imágenes con la misma composición

1. Abrimos en SNAP los productos del 3 y del 10 de abril (`MTD_MSIL2A.xml`, como en la lección 5.2).
2. En cada uno: **Window → Open RGB Image Window**, con las bandas **Red** = `B8A`, **Green** = `B11`, **Blue** = `B12`.
3. Ponemos las ventanas una junto a otra: **Window → Tile Horizontally**.

A nosotros, el producto del 3 de abril se nos abrió primero, así que su ventana se llama [1]. La del 10 de abril es la [3]. Los números pueden salir distintos: dependen del orden en que se abran los productos. Saber cuál es cada fecha es fácil: en la imagen del 10 de abril se ve lo quemado en azul.

## Paso 2. Miramos qué min y qué max ha elegido SNAP por su cuenta

1. Hacemos clic en la ventana de la imagen del 3 de abril para activarla.
2. Abrimos **View → Tool Windows → Colour Manipulation**.
3. Arriba en la ventana hay tres botones: **Red**, **Green** y **Blue**. Cada uno muestra su banda: **Red**, B8A; **Green**, B11; **Blue**, B12.
4. Debajo de cada botón hay un histograma (cuántos píxeles tienen cada reflectancia) y una barra de color con dos deslizadores triangulares: a la izquierda, min; a la derecha, max. Debajo de los deslizadores aparecen sus números.
5. Apuntamos min y max de las tres bandas.
6. Hacemos clic en la ventana del 10 de abril y apuntamos lo mismo.

```{figure} ../../images/ch06-colour-manip-b8a-2026-04-03.jpg
:label: es-fig-ch06-colour-manip-b8a-2026-04-03
:alt: Colour Manipulation del 3 de abril, botón Red (banda B8A). Arriba a la derecha, las estadísticas de la banda (Min −0,1, Max 0,783); debajo de los deslizadores, el estiramiento que eligió SNAP: −0,00339 y 0,44.
:width: 100%

**Colour Manipulation** del 3 de abril, botón **Red** (banda B8A). Arriba a la derecha, las estadísticas de la banda (Min −0,1, Max 0,783); debajo de los deslizadores, el estiramiento que eligió SNAP: −0,00339 y 0,44. Contiene datos modificados de Copernicus Sentinel (2026).
```

**Atención: en la ventana hay dos grupos de números, y son cosas distintas.**

1. **En el recuadro de arriba a la derecha** (por ejemplo, `Min: -0.1`, `Max: 0.783`) están la reflectancia más pequeña y la más grande de todos los píxeles de la imagen. Son estadísticas de la banda, no el estiramiento. El aviso «Rough statistics!» significa que SNAP las ha calculado deprisa, con una parte de los píxeles.
2. **Debajo de los deslizadores** (por ejemplo, `-3.39E-3` y `0.44`) están el min y el max del estiramiento. **Son los que necesitamos.**

**Cómo se lee la notación con la letra E.** Así escriben los programas los números muy pequeños o muy grandes. La E significa «multiplicado por 10 elevado a»:

- `3.39E-3` = 3,39 × 10⁻³ = 3,39 × 0,001 = 0,00339. Así que `-3.39E-3` = −0,00339.
- `2.91E-4` = 2,91 × 0,0001 = 0,000291.
- `2.58E-2` = 2,58 × 0,01 = 0,0258.
- `2E-2` = 2 × 0,01 = 0,02.
- `1.67E-2` = 1,67 × 0,01 = 0,0167.
- `9.77E-6` = 9,77 × 0,000001 = 0,00000977, prácticamente cero.

Esto es lo que nos salió a nosotros (los números de debajo de los deslizadores, con la reflectancia redondeada a cuatro decimales):

| | B8A min | B8A max | B11 min | B11 max | B12 min | B12 max |
|---|---|---|---|---|---|---|
| 3 de abril | −0,0034 | 0,44 | −0,0003 | 0,27 | 0,00001 | 0,16 |
| 10 de abril | 0,0258 | 0,49 | 0,02 | 0,42 | 0,0167 | 0,39 |

Comparemos el max de cada banda: cuántas veces es mayor el max del 10 de abril que el del 3 de abril.

- B8A: 0,49 / 0,44 ≈ 1,1 veces.
- B11: 0,42 / 0,27 ≈ 1,6 veces.
- B12: 0,39 / 0,16 ≈ 2,4 veces.

**La mayor diferencia está en la banda B12, que en pantalla es la azul.** Nos lo apuntamos.

De dónde sale tanta diferencia. SNAP coloca los deslizadores por su cuenta, a partir del histograma de toda la imagen. Y la imagen del 10 de abril es toda la escena, de 110 × 110 km, con un 43 % de nubes (lección 4.2). En las bandas SWIR, las nubes son muy brillantes. Añaden al histograma muchos valores altos y «tiran» del max hacia arriba. Sobre nuestra zona quemada no hay nubes, pero SNAP elige el estiramiento mirando toda la escena.

## Paso 3. Comprobamos la reflectancia en un punto fuera de lo quemado

Necesitamos un punto que seguro que no ha ardido. Nuestra marca de la lección 5.3 (Pin 1) está en el centro de lo quemado, así que no nos sirve. Ponemos una nueva.

1. **View → Tool Windows → Pin Manager → New pin**.
2. Escribimos Lat `43.3468` y Lon `-6.7000`. La latitud es la misma que la de Pin 1, y la longitud está más al oeste.
3. En el filtro de **Pin Manager** (el botón del embudo) marcamos `B8A`, `B11` y `B12`. Lo hacemos en las dos imágenes.
4. Apuntamos seis números: tres bandas en dos fechas. **Pin Manager** muestra los números de la imagen cuya ventana está activa en ese momento. Por eso hacemos clic en la ventana del 3 de abril y apuntamos, y luego en la del 10 de abril y apuntamos.

**A qué distancia de lo quemado está la marca nueva.** Calculemos cuántos kilómetros tiene un grado de longitud en nuestra latitud. En el ecuador, un grado de longitud mide 111,32 km. Hacia los polos, los meridianos se juntan y el grado se acorta. Se acorta tantas veces como indica el coseno de la latitud:

- 1° de longitud = 111,32 km × cos(latitud);
- cos(43,35°) ≈ 0,7272;
- 111,32 × 0,7272 ≈ **80,9 km**.

Ahora, las distancias:

- **De Pin 1 a la marca nueva:** −6,6746 − (−6,7000) = 0,0254°. 0,0254 × 80,9 ≈ **2,05 km** hacia el oeste.
- **Desde el borde oeste de lo quemado:** según el contorno de EFFIS, el borde oeste está en la longitud −6,6930. −6,6930 − (−6,7000) = 0,0070°. 0,0070 × 80,9 ≈ **0,57 km** fuera del borde de lo quemado.

Así que la marca está a más o menos medio kilómetro de lo quemado, y claramente fuera del contorno. Lo comprobamos en la imagen del 10 de abril: la marca 2 no está sobre el azul.

```{figure} ../../images/ch06-snap-own-stretch-pins-2026-04-03.jpg
:label: es-fig-ch06-snap-own-stretch-pins-2026-04-03
:alt: Las dos imágenes con el estiramiento de SNAP: a la izquierda, el 3 de abril (azulada); a la derecha, el 10 de abril (oliva anaranjado). Abajo, Pin Manager con los valores del 3 de abril para Pin 1 (dentro de lo quemado) y Pin 2 (fuera).
:width: 100%

Las dos imágenes con el estiramiento de SNAP: a la izquierda, el 3 de abril (azulada); a la derecha, el 10 de abril (oliva anaranjado). Abajo, **Pin Manager** con los valores del 3 de abril para Pin 1 (dentro de lo quemado) y Pin 2 (fuera). Contiene datos modificados de Copernicus Sentinel (2026).
```

Esto es lo que mostró **Pin Manager**:

| | B8A | B11 | B12 |
|---|---|---|---|
| Pin 2, 3 de abril | 0,2175 | 0,2059 | 0,1155 |
| Pin 2, 10 de abril | 0,2343 | 0,2172 | 0,1192 |

Calculemos cuánto ha cambiado la reflectancia. Diferencia = valor del 10 de abril − valor del 3 de abril. Cambio en porcentaje = diferencia / valor del 3 de abril × 100.

- **B8A:** 0,2343 − 0,2175 = 0,0168. 0,0168 / 0,2175 ≈ 0,077 → **+7,7 %**.
- **B11:** 0,2172 − 0,2059 = 0,0113. 0,0113 / 0,2059 ≈ 0,055 → **+5,5 %**.
- **B12:** 0,1192 − 0,1155 = 0,0037. 0,0037 / 0,1155 ≈ 0,032 → **+3,2 %**.

**La reflectancia en un punto fuera de lo quemado solo ha cambiado entre un 3 y un 8 %.** El terreno es casi el mismo.

Para comparar, la misma comprobación en el centro de lo quemado (Pin 1):

| | B8A | B11 | B12 |
|---|---|---|---|
| Pin 1, 3 de abril | 0,1773 | 0,2637 | 0,198 |
| Pin 1, 10 de abril | 0,1344 | 0,2207 | 0,2054 |

- **B8A:** 0,1344 − 0,1773 = −0,0429. −0,0429 / 0,1773 ≈ −0,242 → **−24 %**.

En lo quemado, la banda del infrarrojo cercano ha caído una cuarta parte. Es un cambio real: las plantas que reflejaban esa luz han ardido. Fuera de lo quemado no hay un cambio así.

## Paso 4. Calculamos de qué color ha mostrado SNAP el punto de fuera de lo quemado

Ahora tenemos todo lo necesario para comprobar la hipótesis 2 con un cálculo. Cogemos la reflectancia de Pin 2 (paso 3) y el min y el max que eligió SNAP (paso 2), y los metemos en la fórmula:

**brillo = (reflectancia − min) / (max − min) × 255**

**3 de abril, estiramiento de SNAP:**

- **Bombilla roja (B8A):** min = −0,0034, max = 0,44, reflectancia 0,2175.
  - reflectancia − min = 0,2175 − (−0,0034) = 0,2175 + 0,0034 = 0,2209;
  - max − min = 0,44 − (−0,0034) = 0,44 + 0,0034 = 0,4434;
  - 0,2209 / 0,4434 ≈ 0,498;
  - 0,498 × 255 ≈ **127**.
- **Bombilla verde (B11):** min = −0,0003, max = 0,27, reflectancia 0,2059.
  - 0,2059 + 0,0003 = 0,2062;
  - 0,27 + 0,0003 = 0,2703;
  - 0,2062 / 0,2703 ≈ 0,763;
  - 0,763 × 255 ≈ **195**.
- **Bombilla azul (B12):** min = 0,00001, max = 0,16, reflectancia 0,1155.
  - 0,1155 − 0,00001 ≈ 0,1155;
  - 0,16 − 0,00001 ≈ 0,16;
  - 0,1155 / 0,16 ≈ 0,722;
  - 0,722 × 255 ≈ **184**.

**10 de abril, estiramiento de SNAP:**

- **Roja (B8A):** min = 0,0258, max = 0,49, reflectancia 0,2343.
  - 0,2343 − 0,0258 = 0,2085;
  - 0,49 − 0,0258 = 0,4642;
  - 0,2085 / 0,4642 ≈ 0,449;
  - 0,449 × 255 ≈ **115**.
- **Verde (B11):** min = 0,02, max = 0,42, reflectancia 0,2172.
  - 0,2172 − 0,02 = 0,1972;
  - 0,42 − 0,02 = 0,40;
  - 0,1972 / 0,40 = 0,493;
  - 0,493 × 255 ≈ **126**.
- **Azul (B12):** min = 0,0167, max = 0,39, reflectancia 0,1192.
  - 0,1192 − 0,0167 = 0,1025;
  - 0,39 − 0,0167 = 0,3733;
  - 0,1025 / 0,3733 ≈ 0,275;
  - 0,275 × 255 ≈ **70**.

Lo resumimos en una tabla:

| Pin 2 | roja (B8A) | verde (B11) | azul (B12) | qué vemos |
|---|---|---|---|---|
| 3 de abril | 127 | 195 | 184 | azul claro: la verde y la azul brillan mucho |
| 10 de abril | 115 | 126 | 70 | oliva anaranjado: la azul casi se ha apagado |

El 3 de abril, la bombilla azul brilla 184 / 70 ≈ 2,6 veces más que el 10 de abril. Y la reflectancia de B12 solo se diferencia en un 3 %. **Todo el «azul claro» del 3 de abril es cosa del estiramiento de SNAP, no del terreno.**

## Paso 5. Ponemos el mismo estiramiento

Para que la comparación sea honesta, una misma reflectancia tiene que dar el mismo color en las dos imágenes. Es decir, el min y el max de cada banda tienen que ser iguales en las dos fechas.

¿Qué números cogemos? Necesitamos un intervalo en el que quepan los valores de las dos imágenes. Para cada banda:

- **min común** = el menor de los dos min (de la tabla del paso 2);
- **max común** = el mayor de los dos max.

Los elegimos con la tabla del paso 2:

- **B8A:** min −0,0034 y 0,0258 → el menor es **−0,0034**. Max 0,44 y 0,49 → el mayor es **0,49**.
- **B11:** min −0,0003 y 0,02 → el menor es **−0,0003**. Max 0,27 y 0,42 → el mayor es **0,42**.
- **B12:** min 0,00001 y 0,0167 → el menor es 0,00001. Escribimos **0**: una diferencia de 0,00001 cambia el brillo menos de una centésima de nivel. Max 0,16 y 0,39 → el mayor es **0,39**.

Lo que escribimos:

| Botón | Banda | min | max |
|---|---|---|---|
| Red | B8A | `-0.0034` | `0.49` |
| Green | B11 | `-0.0003` | `0.42` |
| Blue | B12 | `0` | `0.39` |

**Dónde se escriben.** Los números se escriben justo debajo de los deslizadores, pero es un sitio fácil de pasar por alto:

1. Hacemos clic en la ventana de la imagen del 3 de abril para activarla.
2. En **Colour Manipulation**, elegimos **Red**.
3. Hacemos clic en el número que hay debajo del deslizador izquierdo (el negro). Al lado se abre un pequeño campo con el valor actual.
4. Lo borramos, escribimos `-0.0034` y pulsamos Enter. El deslizador se mueve.
5. Hacemos clic en el número que hay debajo del deslizador derecho (el de color), escribimos `0.49` y pulsamos Enter.
6. Hacemos lo mismo en **Green** (`-0.0003`, `0.42`) y en **Blue** (`0`, `0.39`).
7. Hacemos clic en la ventana del 10 de abril y escribimos los mismos seis números.

```{figure} ../../images/ch06-colour-manip-edit-value.jpg
:label: es-fig-ch06-colour-manip-edit-value
:alt: Al hacer clic en el número de debajo del deslizador se abre un campo para escribir el valor; aquí, el min de B8A: -0.0034.
:width: 100%

Al hacer clic en el número de debajo del deslizador se abre un campo para escribir el valor; aquí, el min de B8A: `-0.0034`.
```

Los números se escriben con punto y con el guion normal para el signo menos, como en la tabla.

**Qué esperamos ver.** Calculemos de antemano el color de Pin 2 con el estiramiento común.

3 de abril:

- roja: (0,2175 + 0,0034) / (0,49 + 0,0034) × 255 = 0,2209 / 0,4934 × 255 ≈ 0,448 × 255 ≈ **114**;
- verde: (0,2059 + 0,0003) / (0,42 + 0,0003) × 255 = 0,2062 / 0,4203 × 255 ≈ 0,491 × 255 ≈ **125**;
- azul: (0,1155 − 0) / (0,39 − 0) × 255 = 0,1155 / 0,39 × 255 ≈ 0,296 × 255 ≈ **76**.

10 de abril:

- roja: (0,2343 + 0,0034) / 0,4934 × 255 = 0,2377 / 0,4934 × 255 ≈ 0,482 × 255 ≈ **123**;
- verde: (0,2172 + 0,0003) / 0,4203 × 255 = 0,2175 / 0,4203 × 255 ≈ 0,518 × 255 ≈ **132**;
- azul: 0,1192 / 0,39 × 255 ≈ 0,306 × 255 ≈ **78**.

| Pin 2, estiramiento común | roja | verde | azul |
|---|---|---|---|
| 3 de abril | 114 | 125 | 76 |
| 10 de abril | 123 | 132 | 78 |

La diferencia no pasa de 9 niveles de 255. A la vista es el mismo color. Así que, después del paso 5, la imagen del 3 de abril debería dejar de ser azulada y volverse color oliva, como la del 10 de abril.

Y en lo quemado (Pin 1), con el mismo estiramiento común:

- 3 de abril: roja (0,1773 + 0,0034) / 0,4934 × 255 ≈ **93**, verde (0,2637 + 0,0003) / 0,4203 × 255 ≈ **160**, azul 0,198 / 0,39 × 255 ≈ **129**;
- 10 de abril: roja (0,1344 + 0,0034) / 0,4934 × 255 ≈ **71**, verde (0,2207 + 0,0003) / 0,4203 × 255 ≈ **134**, azul 0,2054 / 0,39 × 255 ≈ **134**.

La roja ha bajado 22 niveles, y la azul brilla ya tanto como la verde. En lo quemado, el color se va hacia el azul. Este cambio se mantiene también con el estiramiento común, porque es real.

## Qué ha salido

**Las dos hipótesis se han cumplido.**

1. **El terreno apenas ha cambiado.** En el punto de fuera de lo quemado, la reflectancia ha subido entre un 3 y un 8 % en siete días (paso 3).
2. **El color distinto lo ha puesto SNAP.** Eligió el estiramiento de cada imagen por separado, mirando toda la escena. El 10 de abril, las nubes subieron el max: en la banda B12, de 0,16 a 0,39, 2,4 veces más. Por eso, en un mismo punto, la bombilla azul brillaba a 184 el 3 de abril y a 70 el 10 de abril (paso 4).

Después de escribir el mismo min y el mismo max, **las dos imágenes han quedado del mismo color**. Las laderas, los prados y los bosques de alrededor se ven igual en las dos fechas. Solo cambia lo quemado: el 10 de abril sale azul.

```{figure} ../../images/ch06-snap-common-stretch-2026-04-03-10.jpg
:label: es-fig-ch06-snap-common-stretch-2026-04-03-10
:alt: Las mismas dos imágenes con el estiramiento común: el terreno sin quemar tiene el mismo color el 3 y el 10 de abril; solo cambia lo quemado, azul el 10 de abril.
:width: 100%

Las mismas dos imágenes con el estiramiento común: el terreno sin quemar tiene el mismo color el 3 y el 10 de abril; solo cambia lo quemado, azul el 10 de abril. Contiene datos modificados de Copernicus Sentinel (2026).
```

Y una cosa más. Al este de lo quemado se ve una pequeña mancha azul oscuro que ya está el 3 de abril, antes de nuestro incendio. Con el estiramiento común se nota más. Qué es lo veremos en la lección 6.2.

## Si algo falla

1. **Hemos apuntado los números del recuadro de arriba a la derecha, no los de debajo de los deslizadores.** Los números del recuadro (Min, Max) son estadísticas de la banda. El estiramiento son los números de debajo de los deslizadores.
2. **No entendemos un número como `-3.39E-3`.** La E significa «multiplicado por 10 elevado a». `-3.39E-3` = −0,00339 (paso 2).
3. **No se abre el campo para escribir.** Hacemos clic justo en el número de debajo del deslizador, no en el deslizador. Si con un clic no funciona, probamos con doble clic.
4. **Hemos escrito los números y el color no ha cambiado.** Lo más probable es que los números hayan ido a la ventana de la otra imagen. **Colour Manipulation** siempre muestra la ventana activa: su nombre aparece en la pestaña de arriba (por ejemplo, Navigation − [3] RGB).
5. **SNAP no acepta el signo menos.** El menos se escribe con el guion normal `-`, y el separador decimal es el punto.

:::{tip} Dato curioso
En el recuadro de estadísticas de la imagen del 3 de abril, Min = −0,1. No es una reflectancia real. Son píxeles sin datos: en el archivo hay un 0, y con la fórmula de la lección 5.2, (0 − 1000) / 10 000 = −0,1. Hasta las estadísticas muestran con honestidad cómo está hecho el archivo.
:::

:::{admonition} Tus datos
- La marca de fuera de lo quemado la ponemos junto a nuestro propio incendio: con la misma latitud que la marca de dentro, y con una longitud que quede fuera del borde del contorno. La distancia se calcula igual: 111,32 km × cos(latitud) por cada grado de longitud.
- Con otros datos, el min y el max serán distintos: dependen de la escena, de las nubes y de la fecha. El orden es el mismo: apuntar los números de debajo de los deslizadores en las dos fechas → min común = el menor, max común = el mayor → escribirlos en las dos ventanas.
:::

## Resumen

**Conceptos nuevos**

- **Estiramiento del contraste** (*contrast stretch*): el paso de la reflectancia al brillo de la pantalla con dos números, min y max. Ejemplo: con min 0,05 y max 0,35, una reflectancia de 0,20 da un brillo de 128.
- **Histograma**: un gráfico que indica cuántos píxeles de la imagen tienen cada valor. Ejemplo: en **Colour Manipulation**, el pico alto de la izquierda son los píxeles oscuros del agua y de las sombras.
- **Mismo estiramiento**: el mismo min y el mismo max para cada banda en todas las imágenes que comparamos. Ejemplo: B12 con min 0 y max 0,39 el 3 y el 10 de abril.

**Lo esencial**

- El color en pantalla no depende solo de la reflectancia, sino también del min y del max del estiramiento.
- SNAP elige el estiramiento de cada imagen mirando toda la escena; unas nubes lejos de nuestra zona pueden cambiar el color de nuestra ladera.
- Las imágenes de «antes» y «después» solo se pueden comparar a ojo con el mismo estiramiento.
- Si necesitamos una respuesta y no una imagen, miramos los números de la reflectancia en **Pin Manager** o en **Pixel Info**.

## Preguntas para un ingeniero

1. ¿Por qué unas nubes lejanas, sobre el mar, han cambiado el color de nuestra ladera?

:::{dropdown} Respuesta
SNAP elige el min y el max con el histograma de toda la escena. Las nubes brillantes añaden muchos valores altos y suben el max. Cuanto mayor es el max, menos brilla la bombilla con la misma reflectancia.
:::

2. ¿Por qué el min común es el menor de los dos, y el max común, el mayor?

:::{dropdown} Respuesta
Así caben en el intervalo los valores de las dos imágenes, y en ninguna se «recorta» nada a 0 o a 255 más que en la otra.
:::

3. Con el mismo estiramiento, ¿se puede medir lo quemado por el color?

:::{dropdown} Respuesta
No. El estiramiento es solo para la vista. Para los cálculos usamos los propios números de la reflectancia; en el capítulo 8 construiremos con ellos un índice.
:::


## Ejercicios

1. **Entender:** ¿por qué no se pueden comparar a ojo las imágenes de «antes» y «después» si el programa ha ajustado por su cuenta el contraste de cada una?
2. **Corregir:** «En la imagen del 10 de abril, la ladera que no ha ardido sale más clara, así que su reflectancia ha subido después del incendio». ¿Qué falla?
3. **Repaso de la lección anterior (5.3):** ¿por qué usamos el L2A, y no el L1C, para comparar «antes» y «después»?

Las respuestas están en la página [Soluciones](../solutions.md).

## La pregunta que queda abierta

Con el mismo estiramiento, al este de lo quemado se ve una mancha azul oscuro que ya estaba el 3 de abril, antes del incendio. Parece una zona quemada más antigua. ¿Entra en nuestro marco? ¿La confundiremos con lo que ardió el 6 de abril? Lo veremos en la lección 6.2, donde además dibujaremos un contorno rápido de lo quemado.

---

## Notas y fuentes

- Imágenes Sentinel-2 L2A del 3 y del 10 de abril de 2026, tesela T29TPJ, órbita R037 (Copernicus Data Space Ecosystem), abiertas en SNAP 14.
- Contorno de lo quemado de EFFIS, registro 294223: borde oeste en −6,6930. https://api.effis.emergency.copernicus.eu/rest/2/burntareas/current/294223/ (consultado el 21/11/2026)
- Lo que mide un grado de longitud: 111,32 km × cos(latitud), con un modelo esférico de la Tierra; para nuestras distancias, la precisión es suficiente.
