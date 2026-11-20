---
title: "5.1. Descargamos la imagen"
---

## Dónde lo dejamos

Ya tenemos la pareja de imágenes: la del 3 de abril de 2026 («antes») y la del 10 de abril de 2026 («después»). Hasta ahora solo las hemos mirado en Copernicus Browser. El navegador nos enseñaba una imagen, pero con él no podemos trabajar con los números. Para eso necesitamos los archivos en nuestro ordenador.

En esta lección hacemos una sola cosa: descargamos la imagen del 3 de abril y vemos qué aparece en la carpeta.

## Qué queremos saber

**La pregunta:** ¿qué recibimos exactamente cuando descargamos una imagen de Sentinel-2?

**Nuestra hipótesis antes de empezar:**

1. Recibiremos un solo archivo comprimido de alrededor de 1 GB. Es lo que indicaba el catálogo.
2. Dentro no habrá una sola imagen, sino muchos archivos: uno por cada banda. Al fin y al cabo, el satélite mide las 13 bandas por separado.
3. Los archivos estarán ordenados por tamaño de píxel: 10, 20 y 60 metros.

**Cómo sabremos que nos hemos equivocado:** si hay menos archivos o más de los que esperamos, o si están organizados de otra manera.

## Paso 1. Cuál de los dos productos descargamos

Recordemos que el incendio está en el límite entre dos teselas, la 29TPH y la 29TPJ. Para cada fecha hay dos productos. No hace falta descargar los dos si nuestro marco cabe entero en uno.

1. En Copernicus Browser, abrimos la pestaña Search.
2. Elegimos Sentinel-2 L2A y la fecha del 3 de abril de 2026, y pulsamos Search.
3. En la lista aparecen dos productos. Cada uno tiene un icono de diana. Lo pulsamos y el contorno del producto aparece en el mapa.
4. Miramos si nuestro marco amarillo queda entero dentro del contorno. Primero comprobamos un producto y luego el otro.

Descargamos el producto en el que el marco cabe entero.

```{figure} ../../images/ch05-search-2026-04-03-tile-29TPH.jpg
:label: es-fig-ch05-search-2026-04-03-tile-29TPH
:alt: Contorno del producto 29TPH del 3 de abril de 2026 (verde): su borde norte cruza el marco (amarillo).
:width: 100%

Contorno del producto 29TPH del 3 de abril de 2026 (verde): su borde norte cruza el marco (amarillo). Contiene datos modificados de Copernicus Sentinel (2026).
```

```{figure} ../../images/ch05-search-2026-04-03-tile-29TPJ.jpg
:label: es-fig-ch05-search-2026-04-03-tile-29TPJ
:alt: Contorno del producto 29TPJ del 3 de abril de 2026 (verde): el marco (amarillo) queda entero dentro.
:width: 100%

Contorno del producto 29TPJ del 3 de abril de 2026 (verde): el marco (amarillo) queda entero dentro. Contiene datos modificados de Copernicus Sentinel (2026).
```

## Paso 2. Descargamos

1. En el producto elegido, pulsamos el icono de descarga (la flecha hacia abajo).
2. Guardamos el archivo en la carpeta del proyecto `data`, dentro de la subcarpeta `sentinel2`. Si no existe, la creamos.
3. Esperamos a que termine la descarga. El archivo es grande, así que puede tardar unos minutos.

## Paso 3. Descomprimimos

El archivo descargado es un comprimido que termina en `.zip`. Lo abrimos con un doble clic en Finder. A su lado aparece una carpeta cuyo nombre termina en `.SAFE`.

`.SAFE` es el «envoltorio» estándar de las imágenes Sentinel. El nombre de la carpeta coincide con el nombre del producto, que ya aprendimos a leer en el capítulo 4.

## Paso 4. Vemos qué hay dentro

Abrimos la carpeta `.SAFE` en Finder y bajamos por ella paso a paso.

1. Arriba hay varias carpetas y archivos. Nos interesan dos:
   - el archivo `MTD_MSIL2A.xml`: la ficha de todo el producto;
   - la carpeta `GRANULE`: los datos en sí.
2. Abrimos `GRANULE`. Dentro hay una sola carpeta con el nombre de la tesela, por ejemplo `L2A_T29TPJ_...`.
3. La abrimos. Ahí están la carpeta `IMG_DATA`, con las imágenes, y el archivo `MTD_TL.xml`, la ficha de la tesela. En ella aparecen la altura y el acimut del sol en el momento de la toma.
4. Abrimos `IMG_DATA`. Dentro hay tres carpetas: `R10m`, `R20m` y `R60m`. El número es el tamaño del píxel.
5. Abrimos `R20m` y contamos cuántos archivos hay.

```{figure} ../../images/ch05-safe-tree-2026-04-03.jpg
:label: es-fig-ch05-safe-tree-2026-04-03
:alt: La carpeta .SAFE del 3 de abril de 2026 en Finder.
:width: 100%

La carpeta `.SAFE` del 3 de abril de 2026 en Finder.
```

Antes de contar, apuntamos lo que esperamos. En el capítulo 3 vimos que las bandas B05, B06, B07, B8A, B11 y B12 tienen píxeles de 20 metros. Así que en la carpeta `R20m` esperamos 6 archivos de bandas.

Cada archivo se llama más o menos así: `T29TPJ_20260403T112109_B12_20m.jp2`. Se lee así:

| Parte | Qué significa |
|---|---|
| T29TPJ | tesela |
| 20260403T112109 | fecha y hora de la toma |
| B12 | banda |
| 20m | tamaño del píxel |
| .jp2 | formato del archivo (JPEG 2000) |

## Qué ha salido

**La hipótesis se ha cumplido a medias: acertamos con la organización de las carpetas, pero no con el número de archivos.**

**Qué producto.** Nuestro marco solo queda entero dentro de la tesela 29TPJ. El borde norte de la tesela 29TPH cruza justo por el marco, y parte de lo quemado se queda fuera. Así que para nuestro incendio basta con un producto, el de la 29TPJ, y no hace falta descargar los dos.

**Tamaño.** El comprimido del 3 de abril pesa 887 MB, algo menos de lo que esperábamos. La tesela vecina, la 29TPH, pesa 1151 MB en la misma fecha. El tamaño también cambia de una fecha a otra: la misma 29TPJ pesa entre 911 y 991 MB el 8, el 10 y el 20 de abril. El formato JPEG 2000 comprime la imagen, y lo que ocupa el archivo depende de lo que haya en ella: mar, nubes, montañas.

**Qué hay arriba en la carpeta `.SAFE`.** Además de `MTD_MSIL2A.xml` y `GRANULE`, hay:

- las carpetas `DATASTRIP`, `HTML` y `rep_info`;
- los archivos `manifest.safe` e `INSPIRE.xml`;
- una pequeña imagen de vista previa que termina en `-ql.jpg`.

Son archivos de servicio: la descripción de la toma, la lista del contenido y los esquemas para validar las fichas. Para trabajar con la imagen no los necesitamos.

**La carpeta de la tesela** se llama `L2A_T29TPJ_A047396_20260403T112705`. Su nombre tiene tres partes:

- la tesela: T29TPJ;
- el número de vuelta del satélite desde que empezó a funcionar: A047396;
- la hora de inicio de la franja de toma.

```{figure} ../../images/ch05-r10m-r20m-2026-04-03.jpg
:label: es-fig-ch05-r10m-r20m-2026-04-03
:alt: Contenido de las carpetas R10m y R20m del 3 de abril de 2026.
:width: 100%

Contenido de las carpetas `R10m` y `R20m` del 3 de abril de 2026.
```

**Cuántos archivos hay en `R20m`.** Esperábamos 6 y hay 14:

```text
T29TPJ_20260403T112109_AOT_20m.jp2
T29TPJ_20260403T112109_B01_20m.jp2
T29TPJ_20260403T112109_B02_20m.jp2
T29TPJ_20260403T112109_B03_20m.jp2
T29TPJ_20260403T112109_B04_20m.jp2
T29TPJ_20260403T112109_B05_20m.jp2
T29TPJ_20260403T112109_B06_20m.jp2
T29TPJ_20260403T112109_B07_20m.jp2
T29TPJ_20260403T112109_B11_20m.jp2
T29TPJ_20260403T112109_B12_20m.jp2
T29TPJ_20260403T112109_B8A_20m.jp2
T29TPJ_20260403T112109_SCL_20m.jp2
T29TPJ_20260403T112109_TCI_20m.jp2
T29TPJ_20260403T112109_WVP_20m.jp2
```

Veamos de dónde salen los ocho que sobran:

1. **6 bandas con su propio píxel de 20 m:** B05, B06, B07, B8A, B11 y B12. Son las que esperábamos.
2. **4 bandas remuestreadas desde otro tamaño de píxel.** B02, B03 y B04 se toman con píxel de 10 m, y B01, con píxel de 60 m. Aquí están sus copias pasadas a la rejilla de 20 m. Así es fácil compararlas píxel a píxel con las demás bandas.
3. **4 archivos que no son bandas:**
   - SCL: la clasificación de la escena, la misma capa de la lección 4.2;
   - TCI: una imagen ya hecha en color natural, solo para mirar;
   - AOT: un mapa de aerosoles, es decir, de lo turbio que estaba el aire;
   - WVP: un mapa del vapor de agua en la atmósfera.

AOT y WVP los calculó el propio procesador cuando recalculó la imagen «como si no hubiera atmósfera».

**Lo que no está en `R20m`:**

- B08: en su lugar está la banda estrecha B8A.
- B09: solo está en `R60m`.
- B10: no está en ningún sitio. Esta banda mira las nubes altas de tipo cirro y casi no llega al suelo, así que no se incluye en el producto L2A.

**La diferencia principal con lo que esperábamos:** una misma banda puede aparecer varias veces en el producto, con distintos tamaños de píxel. Por eso «un archivo, una banda» no es correcto. Lo correcto es: un archivo, una banda en un tamaño de píxel.

```{figure} ../../images/ch05-four-safe-folders.jpg
:label: es-fig-ch05-four-safe-folders
:alt: Las cuatro fechas descargadas en data/sentinel2: 3, 8, 10 y 20 de abril de 2026, tesela 29TPJ.
:width: 100%

Las cuatro fechas descargadas en `data/sentinel2`: 3, 8, 10 y 20 de abril de 2026, tesela 29TPJ.
```

**Hemos descargado cuatro fechas.** Además del 3 de abril, en la carpeta `data/sentinel2` ya tenemos el 8, el 10 y el 20 de abril, todas de la tesela 29TPJ y de la órbita R037:

- el 10 de abril es nuestra imagen de «después»;
- el 8 de abril es la de reserva;
- el 20 de abril nos hará falta cuando veamos cómo cambia lo quemado con el tiempo.

## Si algo falla

1. **El botón de descarga no funciona.** Solo pueden descargar los usuarios que han iniciado sesión en Copernicus Browser con su cuenta. Iniciamos sesión y volvemos a probar.
2. **El marco no cabe en ninguna tesela.** Pasa cuando lo quemado está justo en el límite. En ese caso, descargamos los dos productos de la misma fecha y más adelante los unimos. Las teselas vecinas se solapan: cada tesela es un cuadrado de 110 × 110 km, y la separación entre ellas es de 100 km.
3. **El tamaño no coincide con el del catálogo o con el de otra fecha.** Es normal: la compresión depende de lo que haya en la imagen.

:::{tip} Dato curioso
Más de la mitad del producto la ocupa la carpeta `R10m`: 541 de 888 MB. Casi todo ese espacio son las cuatro bandas con píxel de 10 m: B02, B03, B04 y B08. Un píxel la mitad de ancho significa cuatro veces más píxeles.
:::

:::{admonition} Tus datos
Para nuestro propio incendio: buscamos nuestra fecha en la pestaña Search, comprobamos el contorno del producto respecto a nuestro marco y descargamos el que lo cubre entero. La carpeta `.SAFE` está organizada igual en todas las imágenes Sentinel-2 L2A.
:::

## Resumen

**Conceptos nuevos**

- **`.SAFE`**: el envoltorio estándar de un producto Sentinel, una carpeta con los datos y las fichas. Ejemplo: `S2B_MSIL2A_20260403T112109_N0512_R037_T29TPJ_20260403T153931.SAFE`.
- **Ficha del producto**: el archivo `MTD_MSIL2A.xml`, que describe todo el producto.
- **Ficha de la tesela**: el archivo `MTD_TL.xml`. Entre otras cosas, recoge la altura y el acimut del sol.
- **JPEG 2000 (`.jp2`)**: el formato comprimido en el que vienen las bandas.
- **Remuestreo**: pasar una banda a una rejilla con otro tamaño de píxel. Ejemplo: `B04_20m.jp2` es la banda B04 remuestreada de 10 m a 20 m.
- **SCL, TCI, AOT, WVP**: archivos del producto L2A que no son bandas: la clasificación de la escena, la imagen en color para mirar, el mapa de aerosoles y el mapa de vapor de agua.

**Lo esencial**

- Para nuestra zona quemada basta con un producto por fecha: la tesela 29TPJ.
- Una misma banda puede aparecer en el producto con varios tamaños de píxel.
- Para encontrar el archivo que necesitamos, leemos su nombre: tesela, fecha, banda y tamaño del píxel.

## Preguntas para un ingeniero

1. B04 está tanto en `R20m` como en `R10m`. ¿Cuál cogemos?

:::{dropdown} Respuesta
Depende de lo que vayamos a hacer. Si calculamos algo junto con bandas de 20 m (por ejemplo, con B12), cogemos `B04_20m`: así todos los píxeles tienen el mismo tamaño y coinciden. Si queremos la imagen más detallada, cogemos `B04_10m`. El remuestreo no añade más detalle del que captó el satélite.
:::

2. ¿Por qué no trabajamos directamente con TCI, si ya está en color?

:::{dropdown} Respuesta
Porque TCI no contiene medidas, sino una imagen para la vista. Sus valores están comprimidos al rango de brillo de la pantalla, así que con ellos no se puede calcular un índice.
:::

3. ¿Para qué hemos descargado el 8 y el 20 de abril, si la pareja ya está elegida?

:::{dropdown} Respuesta
El 8 de abril es la imagen de «después» de reserva. El 20 de abril hace falta para la segunda pregunta de la investigación: a qué ritmo se debilita la huella del incendio con el tiempo.
:::

## Ejercicios

1. Recordar: ¿cómo termina el nombre de la carpeta donde queda una imagen de Sentinel-2 después de descomprimirla?
2. Corregir: en el nombre de archivo `T29TPJ_20260403T112109_B12_10m.jp2` hay un error. ¿Cuál?
3. Repaso de la lección 4.2: ¿por qué no usamos la capa Scene classification como máscara de nubes sobre nuestra zona quemada?

## La pregunta que queda abierta

Ya sabemos dónde está la banda B12 y cómo se llama su archivo. Pero ¿qué hay guardado en cada píxel? Todavía no es una reflectancia entre 0 y 1, sino un número entero. Qué número es y cómo se convierte en reflectancia lo veremos en la lección 5.2, cuando abramos la banda en SNAP.

---

## Notas y fuentes

[Copernicus SentiWiki, «S2 Products»](https://sentiwiki.copernicus.eu/web/s2-products) (en inglés), consultado el 19/11/2026. De ahí hemos tomado:

- la composición del producto L2A en las carpetas de 10, 20 y 60 m;
- que B08 no está en la carpeta de 20 m y que B10 no está en el L2A;
- el formato SAFE y JPEG 2000;
- las teselas de 110 × 110 km.
