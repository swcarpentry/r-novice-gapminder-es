---
title: Explorando data frames
teaching: 20
exercises: 10
source: Rmd
---

::::::::::::::::::::::::::::::::::::::: objectives

- Poder agregar y quitar filas y columnas.
- Poder quitar filas con valores `NA`.
- Poder anexar dos *data frames*.
- Poder articular qué es un `factor` y cómo convertir entre `factor` y `character`.
- Poder entender las propiedades básicas de un *data frame*, incluyendo tamaño, clase o tipo de columnas, nombres y primeras filas.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo manipular un *data frame*?

::::::::::::::::::::::::::::::::::::::::::::::::::



A esta altura, ya viste los tipos y estructuras de datos básicos de R y todo lo que hagas va a ser una manipulación de esas herramientas. Ahora pasaremos a aprender un par de cosas sobre cómo trabajar con la clase *data frame* (la estructura de datos que usarás la mayoría del tiempo y que será la estrella del show). Un *data frame* es la tabla que creamos al cargar información de un archivo csv.

:::::::::::::::::::::::::::::::::::::::  checklist

## Palabras clave

Comando : Traducción

`nrow`: número de filas

`ncol`: número de columnas

`rbind`: combinar filas

`cbind`: combinar columnas

::::::::::::::::::::::::::::::::::::::::::::::::::

## Agregando columnas y filas a un data frame

Aprendimos que las columnas en un *data frame* son vectores. Por lo tanto, sabemos que nuestros datos son consistentes con el tipo de dato dentro de esa columna. Si queremos agregar una nueva columna, podemos empezar por crear un nuevo vector:


```r
gatos
```

```output
     color peso legusta_la_cuerda
1    mixto  2.1                 1
2    negro  5.0                 0
3 atigrado  3.2                 1
```

```r
edad <- c(2,3,5)
```

Podemos entonces agregarlo como una columna via:


```r
cbind(gatos, edad)
```

```output
     color peso legusta_la_cuerda edad
1    mixto  2.1                 1    2
2    negro  5.0                 0    3
3 atigrado  3.2                 1    5
```

Tenga en cuenta que fallará si tratamos de agregar un vector con un número diferente de entradas que el número de filas en el marco de datos.


```r
edad <- c(2, 3, 5, 12)
cbind(gatos, edad)
```

```error
Error in data.frame(..., check.names = FALSE): arguments imply differing number of rows: 3, 4
```

```r
edad <- c(2, 3)
cbind(gatos, edad)
```

```error
Error in data.frame(..., check.names = FALSE): arguments imply differing number of rows: 3, 2
```

¿Por qué no funcionó? Claro, R quiere ver un elemento en nuestra nueva columna para cada fila de la tabla:

Para que funcione, debemos tener `nrow(gatos)` = `length(edad)`. Vamos a sobrescribir el contenido de los gatos con nuestro nuevo marco de datos.


```r
edad <- c(2, 3, 5)
gatos <- cbind(gatos, edad)
gatos
```

```output
     color peso legusta_la_cuerda edad
1    mixto  2.1                 1    2
2    negro  5.0                 0    3
3 atigrado  3.2                 1    5
```

Ahora, qué tal si agregamos filas, en este caso, la última vez vimos que las filas de un *data frame* están compuestas por listas:


```r
nueva_fila <- list("carey", 3.3, TRUE, 9)
gatos <- rbind(gatos, nueva_fila)
```

```warning
Warning in `[<-.factor`(`*tmp*`, ri, value = "carey"): invalid factor level, NA
generated
```

Qué significa el error que nos da R? 'invalid factor level' nos dice algo acerca de factores (factors)... pero qué es un factor? Un factor es un tipo de datos en R. Un factor es una categoría (por ejemplo, color) con la que R puede hacer ciertas operaciones. Por ejemplo:


```r
colores <- factor(c("negro","canela","canela","negro"))
levels(colores)
```

```output
[1] "canela" "negro" 
```

```r
nlevels(colores)
```

```output
[1] 2
```

Se puede reorganizar el orden de los factores para que en lugar de que aparezcan por orden alfabético sigan el orden elegido por el usuario.


```r
colores ## el orden actual
```

```output
[1] negro  canela canela negro 
Levels: canela negro
```

```r
colores <- factor(colores, levels = c("negro", "canela"))
colores # despues de re-organizar
```

```output
[1] negro  canela canela negro 
Levels: negro canela
```

## Factores

Los objetos de la clase *factor* son otro tipo de datos que debemos usar con cuidado. Cuando R crea un *factor*, únicamente permite los valores que originalmente
estaban allí cuando cargamos los datos. Por ejemplo, en nuestro caso
'negro', 'canela' y 'atigrado'. Cualquier categoría nueva que no entre en esas categorías será rechazada (y se conviertirá en NA).

La advertencia (*Warning*) nos está diciendo que agregamos 'carey' a nuestro factor
*color*. Pero los otros valores, 3.3 (de tipo *numeric*), TRUE (de tipo *logical*), y 9 (de tipo *numeric*) se añadieron exitosamente a *peso*, *le\_gusta\_cuerda*, y *edad*, respectivamente, dado que esos valores no son de tipo *factor*. Para añadir una nueva categoría 'carey' al *data frame* gatos en la columna *color*, debemos agregar explícitamente a 'carey' como un nuevo nivel (*level*) en el factor:


```r
levels(gatos$color)
```

```output
[1] "atigrado" "mixto"    "negro"   
```

```r
levels(gatos$color) <- c(levels(gatos$color), 'carey')
gatos <- rbind(gatos, list("carey", 3.3, TRUE, 9))
```

De manera alternativa, podemos cambiar la columna a tipo *character*. En este caso, perdemos las categorías, pero a partir de ahora podemos incorporar cualquier palabra a la columna, sin problemas con los niveles del factor.


```r
str(gatos)
```

```output
'data.frame':	5 obs. of  4 variables:
 $ color            : Factor w/ 4 levels "atigrado","mixto",..: 2 3 1 NA 4
 $ peso             : num  2.1 5 3.2 3.3 3.3
 $ legusta_la_cuerda: num  1 0 1 1 1
 $ edad             : num  2 3 5 9 9
```

```r
gatos$color <- as.character(gatos$color)
str(gatos)
```

```output
'data.frame':	5 obs. of  4 variables:
 $ color            : chr  "mixto" "negro" "atigrado" NA ...
 $ peso             : num  2.1 5 3.2 3.3 3.3
 $ legusta_la_cuerda: num  1 0 1 1 1
 $ edad             : num  2 3 5 9 9
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 1

Imaginemos que, como los perros, 1 año humano es equivalente a 7 años en los gatos (La compañía Purina usa [un algoritmo más sofisticado](https://www.proplan.com/gatos/cat-edad-calculator)).

1. Crea un vector llamado `human.edad` multiplicando `gatos$edad` por 7.
2. Convierte `human.edad` a *factor*.
3. Convierte `human.edad` de nuevo a un vector numérico usando la función `as.numeric()`. Ahora, divide por 7 para regresar a las edades originales. Explica lo sucedido.

:::::::::::::::  solution

## Solución al Desafío 1

1. `human.edad <- gatos$edad * 7`
2. `human.edad <- factor(human.edad)` o `as.factor(human.edad)` las dos opciones funcionan igual de bien.
3. `as.numeric(human.edad)` produce `1 2 3 4 4` porque los factores se guardan como objetos de tipo entero *integer* (1:4), cada uno de los cuales tiene asociado una etiqueta *label* (28, 35, 56, y 63). Convertir un objeto de un tipo de datos a otro, por ejemplo de *factor* a *numeric* nos dá los enteros, no las etiquetas *labels*. Si queremos los números originales, necesitamos un paso intermedio, debemos convertir `human.edad` al tipo *character* y luego a *numeric* (¿cómo funciona esto?). Esto aparece en la vida real cuando accidentalmente incluimos un *character* en alguna columna de nuestro archivo .csv, que se suponía que únicamente contendría números. Tendremos este problema, si al leer el archivo olvidamos incluir `stringsAsFactors=FALSE`.
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Quitando filas

Ahora sabemos cómo agregar filas y columnas a nuestro *data frame* en R, pero en nuestro primer intento para agregar un gato llamado 'carey' agregamos una fila que no sirve.


```r
gatos
```

```output
     color peso legusta_la_cuerda edad
1    mixto  2.1                 1    2
2    negro  5.0                 0    3
3 atigrado  3.2                 1    5
4     <NA>  3.3                 1    9
5    carey  3.3                 1    9
```

Podemos pedir el *data frame* sin la fila errónea:


```r
gatos[-4,]
```

```output
     color peso legusta_la_cuerda edad
1    mixto  2.1                 1    2
2    negro  5.0                 0    3
3 atigrado  3.2                 1    5
5    carey  3.3                 1    9
```

Notar que -4 significa que queremos remover la cuarta fila, la coma sin nada detrás indica que se aplica a todas las columnas. Podríamos remover ambas filas en un llamado usando ambos números dentro de un vector: `gatos[c(-4,-5),]`

Alternativamente, podemos eliminar filas que contengan valores `NA`:


```r
na.omit(gatos)
```

```output
     color peso legusta_la_cuerda edad
1    mixto  2.1                 1    2
2    negro  5.0                 0    3
3 atigrado  3.2                 1    5
5    carey  3.3                 1    9
```

Volvamos a asignar el nuevo resultado *output* al *data frame* `gatos`, así nuestros cambios son permanentes:


```r
gatos <- na.omit(gatos)
```

## Eliminando columnas

También podemos eliminar columnas en un *data frame*. Hay dos formas de eliminar una columna: por número o nombre de índice.


```r
gatos[,-4]
```

```output
     color peso legusta_la_cuerda
1    mixto  2.1                 1
2    negro  5.0                 0
3 atigrado  3.2                 1
5    carey  3.3                 1
```

Observa la coma sin nada antes, lo que indica que queremos mantener todas las filas.

Alternativamente, podemos quitar la columna usando el nombre del índice.


```r
drop <- names(gatos) %in% c("edad")
gatos[,!drop]
```

```output
     color peso legusta_la_cuerda
1    mixto  2.1                 1
2    negro  5.0                 0
3 atigrado  3.2                 1
5    carey  3.3                 1
```

## Añadiendo filas o columnas a un data frame

La clave que hay que recordar al añadir datos a un *data frame* es que *las columnas son vectores o factores, mientras que las filas son listas*. Podemos pegar dos *data frames* usando `rbind` que significa unir las filas (verticalmente):


```r
gatos <- rbind(gatos, gatos)
gatos
```

```output
      color peso legusta_la_cuerda edad
1     mixto  2.1                 1    2
2     negro  5.0                 0    3
3  atigrado  3.2                 1    5
5     carey  3.3                 1    9
11    mixto  2.1                 1    2
21    negro  5.0                 0    3
31 atigrado  3.2                 1    5
51    carey  3.3                 1    9
```

Pero ahora los nombres de las filas *rownames* son complicados. Podemos removerlos y R los nombrará nuevamente, de manera secuencial:


```r
rownames(gatos) <- NULL
gatos
```

```output
     color peso legusta_la_cuerda edad
1    mixto  2.1                 1    2
2    negro  5.0                 0    3
3 atigrado  3.2                 1    5
4    carey  3.3                 1    9
5    mixto  2.1                 1    2
6    negro  5.0                 0    3
7 atigrado  3.2                 1    5
8    carey  3.3                 1    9
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 2

Puedes crear un nuevo *data frame* desde R con la siguiente sintaxis:


```r
df <- data.frame(id = c('a', 'b', 'c'),
                 x = 1:3,
                 y = c(TRUE, TRUE, FALSE),
                 stringsAsFactors = FALSE)
```

Crear un data frame que contenga la siguiente información personal:

- nombre
- apellido
- número favorito

Luego usa `rbind` para agregar una entrada para la gente sentada alrededor tuyo.
Finalmente, usa `cbind` para agregar una columna con espacio para que cada persona conteste a la siguiente pregunta: "¿Es hora de una pausa?"

:::::::::::::::  solution

## Solución al Desafío 2


```r
df <- data.frame(first = c('Grace'),
                 apellido = c('Hopper'),
                 numero_favorito = c(0),
                 stringsAsFactors = FALSE)
df <- rbind(df, list('Marie', 'Curie', 238) )
df <- cbind(df, cafe = c(TRUE,TRUE))
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Ejemplo realista

Hasta ahora, hemos visto las manipulaciones básicas que pueden hacerse en un *data frame*. Ahora, vamos a extender esas habilidades con un ejemplo más real. Vamos a importar el **gapminder dataset** que descargamos previamente:

La función `read.table` se usa para leer datos tabulares que están guardados en un archivo de texto,
donde las columnas de datos están separadas por un signo de puntuación como en los archivos
CSV (donde **csv** es **comma-separated values** en inglés, es decir, valores separados por comas).

Los signos de puntuación más comunmente usados para separar o delimitar datos en archivos de texto son tabuladores y comas.
Por conveniencia, R provee dos versiones de la función `read.table`. Estas versiones son: `read.csv`
para archivos donde los datos están separados por comas y `read.delim` para archivos donde los datos están separados
por tabuladores. De las tres variantes, `read.csv` es la más comúnmente usada. De ser necesario, es posible sobrescribir
el signo de puntuación usado por defecto para ambas funciones: `read.csv` y `read.delim`.


```r
gapminder <- read.csv("data/gapminder-FiveYearData.csv")
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Tips misceláneos

- Otro tipo de archivo que puedes encontrar es el separado por tabuladores (.tsv). Para especificar este separador, usa `"\t"` o `read.delim()`.

- Los archivos pueden descargarse de Internet a una carpeta local usando `download.file`.
  La función `read.csv` puede ser ejecutada para leer el archivo descargado, por ejemplo:


```r
download.file("https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder-FiveYearData.csv", destfile = "data/gapminder-FiveYearData.csv")
gapminder <- read.csv("data/gapminder-FiveYearData.csv")
```

- De manera alternativa, puedes leer los archivos directamente en R, usando una dirección web y `read.csv`. Es importante notar que, si se hace esto último, no habrá una copia local del archivo csv en tu computadora. Por ejemplo,


```r
gapminder <- read.csv("https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder-FiveYearData.csv")
```

- Puedes leer directamente planillas de Excel sin necesidad de convertirlas a texto plano usando el paquete [readxl](https://cran.r-project.org/package=readxl).
  

::::::::::::::::::::::::::::::::::::::::::::::::::

Vamos a investigar gapminder un poco; lo primero que hay que hacer siempre es ver cómo se ve el dataset usando `str`:


```r
str(gapminder)
```

```output
'data.frame':	1704 obs. of  6 variables:
 $ country  : chr  "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
 $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
 $ pop      : num  8425333 9240934 10267083 11537966 13079460 ...
 $ continent: chr  "Asia" "Asia" "Asia" "Asia" ...
 $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
 $ gdpPercap: num  779 821 853 836 740 ...
```

También podemos examinar columnas individuales del *data frame* con la función `typeof`:


```r
typeof(gapminder$year)
```

```output
[1] "integer"
```

```r
typeof(gapminder$country)
```

```output
[1] "character"
```

```r
str(gapminder$country)
```

```output
 chr [1:1704] "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
```

También podemos interrogar al *data frame* por la información sobre sus dimensiones;
recordando que `str(gapminder)` dijo que había 1704 observaciones de 6 variables en gapminder, ¿qué piensas que el siguiente código producirá y por qué?


```r
length(gapminder)
```

```output
[1] 6
```

Un intento certero hubiera sido decir que el largo (`length`) de un *data frame* es el número de filas (1704), pero no es el caso; recuerda, un *data frame es una lista de vectores y factors*.


```r
typeof(gapminder)
```

```output
[1] "list"
```

Cuando `length` devuelve 6, es porque gapminder está construida por una lista de 6 columnas. Para conseguir el número de filas, intenta:


```r
nrow(gapminder)
```

```output
[1] 1704
```

```r
ncol(gapminder)
```

```output
[1] 6
```

O, para obtener ambos de una vez:


```r
dim(gapminder)
```

```output
[1] 1704    6
```

Probablemente queremos saber los nombres de las columnas. Para hacerlo, podemos pedir:


```r
colnames(gapminder)
```

```output
[1] "country"   "year"      "pop"       "continent" "lifeExp"   "gdpPercap"
```

A esta altura, es importante preguntarnos si la estructura de R está en sintonía con nuestra intuición y nuestras expectativas, ¿tienen sentido los tipos de datos reportados para cada columna? Si no lo tienen, necesitamos resolver cualquier problema antes de que se conviertan en sorpresas ingratas luego. Podemos hacerlo usando lo que aprendimos sobre cómo R interpreta los datos y la importancia de la estricta consistencia con la que registramos los datos.

Una vez que estamos contentos con el tipo de datos y que la estructura parece razonable, es tiempo de empezar a investigar nuestros datos. Mira las siguientes líneas:


```r
head(gapminder)
```

```output
      country year      pop continent lifeExp gdpPercap
1 Afghanistan 1952  8425333      Asia  28.801  779.4453
2 Afghanistan 1957  9240934      Asia  30.332  820.8530
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
4 Afghanistan 1967 11537966      Asia  34.020  836.1971
5 Afghanistan 1972 13079460      Asia  36.088  739.9811
6 Afghanistan 1977 14880372      Asia  38.438  786.1134
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 3

También es útil revisar algunas líneas en el medio y el final del **data frame** ¿Cómo harías eso?

Buscar líneas exactamente en el medio no es tan difícil, pero simplemente revisar algunas lineas al azar es suficiente. ¿cómo harías eso?

:::::::::::::::  solution

## Solución al desafío 3

Para revisar las últimas líneas del *data frame* R tiene una función para esto:


```r
tail(gapminder)
```

```output
      country year      pop continent lifeExp gdpPercap
1699 Zimbabwe 1982  7636524    Africa  60.363  788.8550
1700 Zimbabwe 1987  9216418    Africa  62.351  706.1573
1701 Zimbabwe 1992 10704340    Africa  60.377  693.4208
1702 Zimbabwe 1997 11404948    Africa  46.809  792.4500
1703 Zimbabwe 2002 11926563    Africa  39.989  672.0386
1704 Zimbabwe 2007 12311143    Africa  43.487  469.7093
```

```r
tail(gapminder, n = 15)
```

```output
      country year      pop continent lifeExp gdpPercap
1690   Zambia 1997  9417789    Africa  40.238 1071.3538
1691   Zambia 2002 10595811    Africa  39.193 1071.6139
1692   Zambia 2007 11746035    Africa  42.384 1271.2116
1693 Zimbabwe 1952  3080907    Africa  48.451  406.8841
1694 Zimbabwe 1957  3646340    Africa  50.469  518.7643
1695 Zimbabwe 1962  4277736    Africa  52.358  527.2722
1696 Zimbabwe 1967  4995432    Africa  53.995  569.7951
1697 Zimbabwe 1972  5861135    Africa  55.635  799.3622
1698 Zimbabwe 1977  6642107    Africa  57.674  685.5877
1699 Zimbabwe 1982  7636524    Africa  60.363  788.8550
1700 Zimbabwe 1987  9216418    Africa  62.351  706.1573
1701 Zimbabwe 1992 10704340    Africa  60.377  693.4208
1702 Zimbabwe 1997 11404948    Africa  46.809  792.4500
1703 Zimbabwe 2002 11926563    Africa  39.989  672.0386
1704 Zimbabwe 2007 12311143    Africa  43.487  469.7093
```

Para revisar algunas lineas al azar?

## sugerencia: Hay muchas maneras de hacer esto

La solución que presentamos aquí utiliza funciones anidadas, por ejemplo una función es el argumento de otra función. Esto te puede parecer nuevo, pero ya lo haz usado.
Recuerda *my\_dataframe[rows, cols]* imprime el *data frame* con la sección de filas y columnas definidas (incluso puedes seleccionar un rando de filas y columnas usando **:** por ejemplo). Para obtener un número al azar o varios números al azar R tiene una función llamada *sample*.


```r
gapminder[sample(nrow(gapminder), 5), ]
```

```output
       country year      pop continent lifeExp  gdpPercap
1649   Vietnam 1972 44655014      Asia  50.254   699.5016
607  Guatemala 1982  6395630  Americas  58.137  4820.4948
499    Eritrea 1982  2637297    Africa  43.890   524.8758
726       Iran 1977 35480679      Asia  57.702 11888.5951
768     Israel 2007  6426679      Asia  80.745 25523.2771
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Para que nuestro análisis sea reproducible debemos poner el código en un *script*
al que podremos volver y editar en el futuro.

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 4

Ve a Archivo -> nuevo -> R script, y crea un script de R llamado load-gapminder.R
para cargar el dataset gapminder. Ponlo en el directorio `scripts/`
y agrégalo al control de versiones.

Ejecuta el script usando la función `source`, usando el path como su argumento
o apretando el botón de "source" en RStudio.

:::::::::::::::  solution

## Solución al desafío 4

Los contenidos de `scripts/load-gapminder.R`:


```r
download.file("https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder-FiveYearData.csv", destfile = "data/gapminder-FiveYearData.csv")
gapminder <- read.csv(file = "data/gapminder-FiveYearData.csv")
```

Para ejecutar el script y cargar los archivos en la variable `gapminder`:

Para ejecutar el script y cargar los archivos en la variable `gapminder`:


```r
source(file = "scripts/load-gapminder.R")
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 5

Leer el output de `str(gapminder)` de nuevo;
esta vez, usar lo que has aprendido de factores, listas y vectores, las funciones como `colnames` y `dim`
para explicar qué significa el output de `str`.
Si hay partes que no puedes entender, discútelo con tus compañeros.

:::::::::::::::  solution

## Solución desafío 5

El objeto `gapminder` es un data frame con columnas

- `country` y `continent` como *factors*.
- `year` como *integer vector*.
- `pop`, `lifeExp`, and `gdpPercap` como *numeric vectors*.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- Usar `cbind()` para agregar una nueva columna a un *data frame*
- Usar `rbind()` para agregar una nueva fila a un *data frame*
- Quitar filas de un *data frame*
- Usar `na.omit()` para remover filas de un *data frame* con valores `NA`
- Usar `levels()` y `as.character()` para explorar y manipular columnas de clase *factor*
- Usar `str()`, `nrow()`, `ncol()`, `dim()`, `colnames()`, `rownames()`, `head()` y `typeof()` para entender la estructura de un *data frame*
- Leer un archivo csv usando `read.csv()`
- Entender el uso de `length()` en un *data frame*

::::::::::::::::::::::::::::::::::::::::::::::::::


