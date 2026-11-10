---
title: "Prólogo. Cuando arde el monte"
---

## Qué pasó el 6 de abril de 2026

El 6 de abril de 2026 hacía calor en Asturias: más de 30 grados y viento del sur. En un solo día se declararon 26 incendios[^1].

Nos quedamos con el mayor. Ardió junto a la aldea de Bustantigo, en el concejo de Allande, en el límite con Tineo[^2]. Es una parroquia de montaña donde viven 18 personas[^3].

No ardió bosque. Casi el 99 % de la superficie quemada es matorral abierto: brezo, tojo y pasto[^4].

Y no es la primera vez que este sitio arde:

1. **Abril de 2017:** 720 ha[^5].
2. **Finales de marzo de 2023:** unas 1200 ha[^6].
3. **Abril de 2026:** otra vez Bustantigo.

**Para estas laderas, el fuego no es un accidente, sino algo que se repite.**

## Por qué Asturias arde en primavera

En Asturias los grandes incendios no llegan en verano, como en el sur de España, sino a finales del invierno y en primavera. En los últimos 40 años, más de la mitad de los grandes incendios, de más de 500 hectáreas cada uno, ocurrieron en febrero, marzo y abril[^7].

La razón es sencilla. Después del invierno, las laderas están llenas de hierba seca y ramas secas, y el verde nuevo todavía no ha brotado.

Así que el incendio típico de Asturias es esto: primavera, matorral y pendiente fuerte. Y la mayoría de los métodos para detectar áreas quemadas se diseñaron para otra cosa: incendios de verano en bosque.

**Por eso no damos estos métodos por buenos: los comprobamos.**

## Para qué saber cuánto ardió

De la superficie y del perímetro del área quemada dependen decisiones reales:

1. **La ley.** Un terreno forestal quemado no puede cambiar de uso durante 30 años[^8]. Para eso hay que saber con exactitud por dónde pasa el límite del área quemada.
2. **Estadísticas y planes.** El plan regional contra incendios se basa en la superficie de los incendios anteriores[^7].
3. **Recuperación.** Con el mapa del área quemada se decide dónde proteger las laderas de la erosión antes de las lluvias de otoño.

**Un error en la superficie no se queda en el papel. Pasa a la ley, a los planes y a las decisiones.**

## Un incendio, varias cifras

¿Cuánto ardió en Bustantigo? Depende de a quién se lo preguntes:

- el catálogo abierto de grandes incendios de España da **681 ha**, y su propio autor advierte de que el perímetro puede desviarse cientos de metros[^9];
- el servicio europeo EFFIS da **700 ha**[^4];
- un perímetro oficial en acceso abierto no lo hemos encontrado.

El problema no es que las cifras no coincidan. El problema es que ninguna lleva margen de error. No sabemos si 681 significa «entre 670 y 690» o «entre 500 y 850». Y una medida sin margen de error no se puede comprobar.

**La respuesta correcta a «cuánto ardió» es una cifra con su intervalo y la explicación de cómo se obtuvo.**

## Por qué el satélite se equivoca en la montaña

El satélite no ve el fuego. Mide la luz que refleja el suelo. Una ladera quemada refleja la luz de forma distinta a una ladera viva, y por esa diferencia encontramos el área quemada.

Pero en la montaña, la cantidad de luz depende de hacia dónde mira la ladera y de lo alto que esté el sol. El satélite Sentinel-2 toma imágenes de Asturias hacia mediodía. Esta es la luz directa que recibe la superficie en ese momento, donde 1 es el sol justo en perpendicular y 0 es la luz rozando la ladera[^10]:

| Fecha | Altura del sol | Terreno llano | Ladera norte de 25° | Ladera sur de 25° |
|---|---|---|---|---|
| 20 de febrero | 32° | 0,54 | 0,16 | 0,81 |
| 8 de abril | 51° | 0,77 | 0,46 | 0,94 |
| 21 de junio | 66° | 0,91 | 0,69 | 0,96 |

Qué vemos aquí:

1. **La ladera sur** recibe casi la misma luz todo el año.
2. **La ladera norte** recibe en junio cuatro veces más luz que en febrero.
3. En febrero, **las laderas norte más empinadas** quedan directamente en su propia sombra.

Ahora pensemos en un incendio de primavera. La imagen «antes» se toma en invierno, con el sol bajo. Las imágenes «después» se toman en primavera y verano, con el sol cada vez más alto. La ladera norte sale más clara en cada imagen nueva solo porque le llega más luz, aunque todavía no haya crecido nada.

El procesado estándar de las imágenes Sentinel-2 corrige esto en parte. Pero en las laderas oscuras, según su propia documentación, corrige de más[^11]. Así que el problema sigue ahí.

**Si no tenemos en cuenta la luz, el satélite confundirá el sol de primavera con hierba rebrotada.**

## Lo que ya se sabe

Por partes, todo esto ya se conoce:

1. **Cómo detectar el área quemada.** Se comparan imágenes de antes y después del incendio. Los propios autores del método recomiendan usar imágenes de la misma estación[^12].
2. **Que la huella se debilita con el tiempo.** En Portugal calcularon que, entre 3 y 4 meses después del incendio, una zona quemada con baja severidad puede parecer ya sin quemar en la imagen[^13].
3. **Que el relieve y la luz interfieren.** Se ha demostrado en Alaska[^14] y en Grecia[^15].

Pero no hemos encontrado ningún trabajo que, para incendios de primavera en matorral de montaña, separe el efecto de la luz de lo que de verdad ha rebrotado en el área quemada.

## Qué vamos a hacer

Vamos a responder a dos preguntas:

1. **Cuánto ardió en Bustantigo**, con su margen de error, y cuánto depende esa cifra de la iluminación de las laderas.
2. **Con qué rapidez desaparece la huella del incendio en las imágenes** y qué parte de esa desaparición es solo luz y no hierba rebrotada. Lo comprobaremos en el incendio de Bustantigo y en otros cuatro incendios de esa misma primavera.

Trabajaremos con imágenes abiertas de Sentinel-2, en Copernicus Browser y QGIS.

Cada resultado lo comprobaremos de tres maneras:

1. **Con puntos aleatorios** sobre imágenes de alta resolución.
2. **Sobre el terreno:** iremos al lugar del incendio.
3. **En otoño.** En octubre el sol vuelve a estar tan bajo como en marzo. Si la huella desaparecía por la luz, en otoño volverá en parte. Si allí ha rebrotado la hierba, no volverá.

**Lo que no afirmamos:**

- nada sobre cuánto dañó el fuego el suelo: para eso hacen falta mediciones sobre el terreno justo después del incendio, y no las hay;
- nada sobre las causas de los incendios;
- nada sobre los incendios en general: cinco incendios de una primavera siguen siendo cinco incendios.

Cualquier respuesta será un resultado, incluso «la luz y la hierba no se pueden separar».

Todo esto se puede repetir en cualquier incendio: las imágenes Sentinel-2 son abiertas y gratuitas para cualquier punto de la Tierra. Donde haya que poner tus propios datos, lo indicaremos.

Recorreremos juntos todo el camino: cómo buscamos las imágenes, cómo razonamos, dónde nos equivocamos y cómo lo comprobamos.

**En la montaña asturiana, el satélite puede confundir el sol de primavera con hierba rebrotada. Aprenderemos a distinguirlo y diremos con honestidad cuánto ardió de verdad.**

---

## Notas y fuentes

[^1]: [RTPA, «Preocupan los incendios del suroccidente», 7 de abril de 2026](https://www.rtpa.es/noticias-asturias/2026-04-07/Preocupan-los-incendios-del-suroccidente_111775542887.html).
[^2]: [La Voz del Trubia, 7 de abril de 2026](https://lavozdeltrubia.es/2026/04/07/se-dispara-en-extension-el-incendio-de-belmonte-y-en-tineo-el-fuego-corta-la-as-15-2/); [elDiario.es, 8 de abril de 2026](https://www.eldiario.es/asturias/asturias-sufre-nueva-oleada-incendios-principado-atribuye-mayoria-accion-delincuentes_1_13125911.html).
[^3]: [Wikipedia, «Bustantigo»](https://en.wikipedia.org/wiki/Bustantigo) (en inglés), población a 1 de enero de 2024.
[^4]: EFFIS, sistema europeo de información sobre incendios forestales: área quemada 294223, Allande, inicio el 6 de abril de 2026 a la 01:30, actualizada el 9 de abril de 2026; 700 ha, 98,9 % de otra vegetación natural y 1,1 % de frondosas. [API de áreas quemadas de EFFIS](https://api.effis.emergency.copernicus.eu/rest/2/burntareas/current/).
[^5]: [ORT Noticias, 29 de junio de 2017](https://ort-ort.com/allande-ibias-y-grandas-de-salime-victimas-de-los-3-grandes-incendios-forestales-que-ha-sufrido-asturias-en-los-cinco-primeros-meses-del-ano/): incendio de Bustantigo (Allande), 720,62 ha.
[^6]: [elDiario.es, 5 de mayo de 2023](https://www.eldiario.es/asturias/fiscalia-pide-ingreso-prision-causante-incendio-allande-quemo-1-200-hectareas_1_10179347.html): incendio del 28 de marzo de 2023 en Bustantigo, 1200 ha.
[^7]: [Principado de Asturias, EPLIFA 2026–2030](https://www.asturias.es/documents/d/guest/eplifa_2026-2030-con-anejos_03062026): 40 de los 73 grandes incendios de 1984–2024 ocurrieron en febrero, marzo y abril (54,8 % de los incendios y 57,3 % de su superficie).
[^8]: [Ley 43/2003, de 21 de noviembre, de Montes, artículo 50](https://www.boe.es/buscar/act.php?id=BOE-A-2003-21339#a50).
[^9]: [edu.forestry.es, «Grandes Incendios Forestales 2026 en España»](https://edu.forestry.es/p/gif2026.html): Allande, 6 de abril de 2026, 681 ha, perimetración sobre imagen Sentinel-2 del 8 de abril de 2026. El autor advierte: «Las delimitaciones pueden contener errores de cientos de metros».
[^10]: Cálculo propio para 43,36° N, 6,67° O a las 11:20 UTC, hora aproximada de paso de Sentinel-2. La posición del sol se calcula con las fórmulas de NOAA; la fracción de luz directa es el coseno del ángulo de incidencia de los rayos sobre la ladera.
[^11]: [ESA, *Sen2Cor Level-2A Algorithm Theoretical Basis Document*, v2.10](https://step.esa.int/thirdparties/sen2cor/2.10.0/docs/S2-PDGS-MPC-L2A-ATBD-V2.10.0.pdf) (en inglés), apartado sobre terreno montañoso; véase también el [foro de Copernicus Data Space, 2024](https://forum.dataspace.copernicus.eu/t/please-make-sentinel-2-l2a-available-without-the-terrain-over-correction/417) (en inglés).
[^12]: Key, C. H. y Benson, N. C. (2006). *Landscape Assessment (LA)*. USDA Forest Service, RMRS-GTR-164-CD (en inglés).
[^13]: [Jahanianfard, D. et al. (2025). *Earth System Science Data* 17: 4957](https://doi.org/10.5194/essd-17-4957-2025) (en inglés): con cada día de retraso de la imagen, el dNBR baja unas 0,0009, y a los 110 días el error supera 0,1, que en la escala de Key y Benson (2006) es el límite entre «sin quemar» y «severidad baja».
[^14]: [Verbyla, D. et al. (2008). *International Journal of Wildland Fire* 17: 527](https://doi.org/10.1071/WF08038) (en inglés).
[^15]: [Veraverbeke, S. et al. (2010). *International Journal of Applied Earth Observation and Geoinformation* 12: 60–70](https://doi.org/10.1016/j.jag.2009.10.004) (en inglés).
