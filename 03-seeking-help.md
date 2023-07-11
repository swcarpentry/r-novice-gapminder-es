---
title: Buscando ayuda
teaching: 10
exercises: 10
source: Rmd
---

::::::::::::::::::::::::::::::::::::::: objectives

- Poder leer archivos de ayuda de R, para funciones y operadores especiales
- Poder usar vistas de tareas CRAN para identificar paquetes para resolver un problema
- Para poder buscar ayuda de tus compañeros

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo obtener ayuda en R?

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::  checklist

## Palabras clave

Comando : Traducción

`help` : ayuda

`vignette` : viñeta

::::::::::::::::::::::::::::::::::::::::::::::::::

## Lectura de archivos de ayuda

R, y cada paquete, proporciona archivos de ayuda para las funciones. La sintaxis general
para buscar ayuda en cualquier función, "function\_name", de una función específica que esté en un paquete
cargado dentro de tu **namespace** (tu sesión interactiva en R):


```r
?function_name
help(function_name)
```

Esto cargará una página de ayuda en RStudio (o como texto sin formato en R por sí mismo).

Cada página de ayuda se divide en secciones:

- Descripción: una descripción extendida de lo que hace la función.
- Uso: los argumentos de la función y sus valores predeterminados.
- Argumentos: una explicación de los datos que espera cada argumento.
- Detalles: cualquier detalle importante a tener en cuenta.
- Valor: los datos que regresa la función.
- Ver también: cualquier función relacionada que pueda serte útil.
- Ejemplos: algunos ejemplos de cómo usar la función.

Las diferentes funciones pueden tener diferentes secciones, pero estas son las principales que debes tener en cuenta.

:::::::::::::::::::::::::::::::::::::::::  callout

## Sugerencia: Lectura de archivos de ayuda

Uno de los aspectos más desalentadores de R es la gran cantidad de funciones
disponibles. Es muy difícil, si no imposible, recordar el
uso correcto para cada función que usas. Afortunadamente, están los archivos de ayuda
¡lo que significa, que no tienes que hacerlo!


::::::::::::::::::::::::::::::::::::::::::::::::::

## Operadores especiales

Para buscar ayuda en operadores especiales, usa comillas:


```r
?"<-"
```

## Obteniendo ayuda en los paquetes

Muchos paquetes vienen con "viñetas": tutoriales y documentación de ejemplo extendida.
Sin ningún argumento, `vignette()` listará todas las viñetas disponibles para todos los paquetes instalados;
`vignette(package="package-name")` listará todas las viñetas disponibles para
`package-name`, y `vignette("vignette-name")` abrirá la viñeta especificada.

Si un paquete no tiene viñetas, generalmente puedes encontrar ayuda escribiendo
`help("package-name")`.

## Cuando recuerdas un poco sobre la función

Si no estás seguro de en qué paquete está una función, o cómo se escribe específicamente, puedes hacer una búsqueda difusa:


```r
??function_name
```

## Cuando no tienes idea de dónde comenzar

Si no sabes qué función o paquete necesitas usar, utiliza
[CRAN Task Views](https://cran.at.r-project.org/web/views)
es una lista especialmente mantenida de paquetes agrupados en
campos. Este puede ser un buen punto de partida.

## Cuando tu código no funciona: busca ayuda de tus compañeros

Si tienes problemas para usar una función, 9 de cada 10 veces,
las respuestas que estas buscando ya han sido respondidas en
[Stack Overflow](https://stackoverflow.com/). Puedes buscar usando
la etiqueta `[r]`.

Si no puedes encontrar la respuesta, hay algunas funciones útiles para
ayudarte a hacer una pregunta a tus compañeros:


```r
?dput
```

Descargará los datos con los que estás trabajando en un formato para que puedan
ser copiados y pegados por cualquier otra persona en su sesión de R.


```r
sessionInfo()
```

```{.output}
R version 4.3.1 (2023-06-16)
Platform: x86_64-pc-linux-gnu (64-bit)
Running under: Ubuntu 22.04.2 LTS

Matrix products: default
BLAS:   /usr/lib/x86_64-linux-gnu/blas/libblas.so.3.10.0 
LAPACK: /usr/lib/x86_64-linux-gnu/lapack/liblapack.so.3.10.0

locale:
 [1] LC_CTYPE=C.UTF-8       LC_NUMERIC=C           LC_TIME=C.UTF-8       
 [4] LC_COLLATE=C.UTF-8     LC_MONETARY=C.UTF-8    LC_MESSAGES=C.UTF-8   
 [7] LC_PAPER=C.UTF-8       LC_NAME=C              LC_ADDRESS=C          
[10] LC_TELEPHONE=C         LC_MEASUREMENT=C.UTF-8 LC_IDENTIFICATION=C   

time zone: UTC
tzcode source: system (glibc)

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

loaded via a namespace (and not attached):
[1] compiler_4.3.1    tools_4.3.1       rstudioapi_0.15.0 knitr_1.43       
[5] xfun_0.39         renv_1.0.0        evaluate_0.21    
```

Imprimirá tu versión actual de R, así como cualquier paquete que hayas
cargado. Esto puede ser útil para otros para ayudar a reproducir y depurar
tu problema.

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 1

Buscar la ayuda para la función `c`. ¿Qué tipo de vector
crees que crearás si evalúas lo siguiente?:


```r
c(1, 2, 3)
c('d', 'e', 'f')
c(1, 2, 'f')
```

:::::::::::::::  solution

## Solución al desafío 1

La función `c()` crea un vector, en el cual todos los elementos son
del mismo tipo. En el primer caso, los elementos son numéricos, en el
segundo, son **character**, y en el tercero son **character**:
los valores numéricos son "forzados" para ser **characters**.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 2

Buscar la ayuda para la función `paste`. Tendrás que usar esto más tarde.
¿Cuál es la diferencia entre los argumentos `sep` y `collapse`?

:::::::::::::::  solution

## Solución para el desafío 2

Busca la ayuda de la función `paste()`, usa:


```r
help("paste")
?paste
```

La diferencia entre `sep` y `collapse` es un poco
complicada. La función `paste` acepta cualquier número de argumentos, cada uno
de los cuales puede ser un vector de cualquier longitud. El argumento `sep` especifica la cadena
usada entre términos concatenados — por defecto, un espacio.  El resultado es un
vector tan largo como el argumento más largo proporcionado a `paste`. En cambio,
`collapse` especifica que después de la concatenación los elementos son *colapsados*
juntos utilizando el separador dado, y el resultado es una sola cadena.
e.g.


```r
paste(c("a","b"), "c")
```

```{.output}
[1] "a c" "b c"
```

```r
paste(c("a","b"), "c", sep = ",")
```

```{.output}
[1] "a,c" "b,c"
```

```r
paste(c("a","b"), "c", collapse = "|")
```

```{.output}
[1] "a c|b c"
```

```r
paste(c("a","b"), "c", sep = ",", collapse = "|")
```

```{.output}
[1] "a,c|b,c"
```

(Para más información,
ve a la parte inferior de la página de ayuda `?paste` y busca los
ejemplos, o prueba `example('paste')`.)



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 3

Usa la ayuda para encontrar una función (y sus parámetros asociados) que tu puedas
usar para cargar datos de un archivo csv en los cuales las columnas están delimitadas con "\\ t"
(tab) y el punto decimal es un "." (punto). Esta comprobación para el separador decimal
es importante, especialmente si estás trabajando con colegas internacionales
ya que diferentes países tienen diferentes convenciones para el
punto decimal (i.e. coma vs. punto).
sugerencia: usa `??csv` para buscar funciones relacionadas con csv.

:::::::::::::::  solution

## Solución para el desafío 3

La función R estándar para leer archivos delimitados por tabuladores con un separador
de punto decimal es `read.delim()`. Tu puedes hacer esto también con
`read.table(file, sep="\t")` (el punto es el separador
decimal por defecto para `read.table()`, aunque es posible que tengas que cambiar también el argumento
`comment.char` si tu archivo de datos contiene caracteres
numeral (#)



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Otros recursos útiles

- [Quick R](https://www.statmethods.net/)
- [RStudio cheat sheets](https://www.rstudio.com/resources/cheatsheets/)
- [Cookbook for R](https://www.cookbook-r.com/)



:::::::::::::::::::::::::::::::::::::::: keypoints

- Usar `help()` para obtener ayuda online de R.

::::::::::::::::::::::::::::::::::::::::::::::::::


