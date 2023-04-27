---
title: Vectorización
teaching: 10
exercises: 15
source: Rmd
---

::::::::::::::::::::::::::::::::::::::: objectives

- Entender las operaciones vertorizadas en R.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo operar sobre todos los elementos de un vector a la vez?

::::::::::::::::::::::::::::::::::::::::::::::::::



La mayoría de las funciones en R están vectorizadas, lo que significa que la función
operará sobre todos los elementos de un vector sin necesidad de hacer un bucle a través
de cada elemento y actuar sobre cada uno de ellos. Esto hace la escritura de código más
concisa, fácil de leer y menos propenso a errores.


```r
x <- 1:4
x * 2
```

```{.output}
[1] 2 4 6 8
```

La multiplicación se aplicó a cada elemento del vector.

También podemos sumar dos vectores juntos:


```r
y <- 6:9
x + y
```

```{.output}
[1]  7  9 11 13
```

Cada elemento de `x` fue sumado a su correspondiente elemento de `y`:


```r
x:  1  2  3  4
    +  +  +  +
y:  6  7  8  9
---------------
    7  9 11 13
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 1

Probemos esto en la columna `pop` del **dataset** `gapminder`.

Haz una nueva columna en el **data frame** `gapminder` que
contiene la población en unidades de millones de personas.
Comprueba el principio o el final del **data frame** para asegurar
que funcionó.

:::::::::::::::  solution

## Solución al desafío 1

Intenta esto en la columna `pop` del **dataset** `gapminder`.

Haz una nueva columna en el **data frame** `gapminder` que
contiene población en unidades de millones de personas.
Comprueba el principio o el final del **data frame** para asegurar
que funcionó.


```r
gapminder$pop_millions <- gapminder$pop / 1e6
head(gapminder)
```

```{.output}
      country year      pop continent lifeExp gdpPercap pop_millions
1 Afghanistan 1952  8425333      Asia  28.801  779.4453     8.425333
2 Afghanistan 1957  9240934      Asia  30.332  820.8530     9.240934
3 Afghanistan 1962 10267083      Asia  31.997  853.1007    10.267083
4 Afghanistan 1967 11537966      Asia  34.020  836.1971    11.537966
5 Afghanistan 1972 13079460      Asia  36.088  739.9811    13.079460
6 Afghanistan 1977 14880372      Asia  38.438  786.1134    14.880372
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 2

En una sola gráfica, traza la población, en
millones, en comparación con el año, para todos los países. No te preocupes en
identificar qué país es cuál.

Repite el ejercicio, graficando sólo para China, India, e
Indonesia. Nuevamente, no te preocupes acerca de cuál es cuál.

:::::::::::::::  solution

## Solución al desafío 2

Recuerda tus habilidades de graficación al crear una gráfica con la población en millones en comparación con el año.


```r
ggplot(gapminder, aes(x = year, y = pop_millions)) +
 geom_point()
```

<img src="fig/09-vectorization-rendered-ch2-sol-1.png" style="display: block; margin: auto;" />

```r
countryset <- c("China","India","Indonesia")
ggplot(gapminder[gapminder$country %in% countryset,],
       aes(x = year, y = pop_millions)) +
  geom_point()
```

<img src="fig/09-vectorization-rendered-ch2-sol-2.png" style="display: block; margin: auto;" />

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Operadores de comparación, operadores lógicos y muchas otras funciones también están
vectorizadas:

**Operadores de Comparación**


```r
x > 2
```

```{.output}
[1] FALSE FALSE  TRUE  TRUE
```

**Operadores Lógicos**


```r
a <- x > 3  # o, para más claridad, a <- (x > 3)
a
```

```{.output}
[1] FALSE FALSE FALSE  TRUE
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Sugerencia: algunas funciones útiles para vectores lógicos

`any()` devuelve `TRUE` si *algún* elemento del vector es `TRUE`
`all()` devuelve `TRUE` si *todos* los elementos del vector son `TRUE`


::::::::::::::::::::::::::::::::::::::::::::::::::

La mayoría de las funciones también operan elemento por elemento en los vectores:

**Funciones**


```r
x <- 1:4
log(x)
```

```{.output}
[1] 0.0000000 0.6931472 1.0986123 1.3862944
```

Operaciones vectorizadas en matrices:


```r
m <- matrix(1:12, nrow=3, ncol=4)
m * -1
```

```{.output}
     [,1] [,2] [,3] [,4]
[1,]   -1   -4   -7  -10
[2,]   -2   -5   -8  -11
[3,]   -3   -6   -9  -12
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Sugerencia: multiplicación elemento por elemento vs. multiplicación de matriz

Muy importante: el operador`*` te da una multiplicación de elemento por elemento!
Para hacer multiplicación de matrices, necesitás usar el operador `%*%`:


```r
m %*% matrix(1, nrow=4, ncol=1)
```

```{.output}
     [,1]
[1,]   22
[2,]   26
[3,]   30
```

```r
matrix(1:4, nrow=1) %*% matrix(1:4, ncol=1)
```

```{.output}
     [,1]
[1,]   30
```

Para saber más sobre Álgebra de matrices, ver [Quick-R reference guide](https://www.statmethods.net/advstats/matrix.html)


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 3

Dada la siguiente matriz:


```r
m <- matrix(1:12, nrow=3, ncol=4)
m
```

```{.output}
     [,1] [,2] [,3] [,4]
[1,]    1    4    7   10
[2,]    2    5    8   11
[3,]    3    6    9   12
```

Escribe lo que crees que sucederá cuando se ejecute:

1. `m ^ -1`
2. `m * c(1, 0, -1)`
3. `m > c(0, 20)`
4. `m * c(1, 0, -1, 2)`

¿Obtuviste la salida que esperabas? Si no, pregunta a un ayudante!

:::::::::::::::  solution

## Solución al desafío 3

Dada la siguiente matriz:


```r
m <- matrix(1:12, nrow=3, ncol=4)
m
```

```{.output}
     [,1] [,2] [,3] [,4]
[1,]    1    4    7   10
[2,]    2    5    8   11
[3,]    3    6    9   12
```

Escribe lo que piensas que sucederá cuando ejecutes:

1. `m ^ -1`


```{.output}
          [,1]      [,2]      [,3]       [,4]
[1,] 1.0000000 0.2500000 0.1428571 0.10000000
[2,] 0.5000000 0.2000000 0.1250000 0.09090909
[3,] 0.3333333 0.1666667 0.1111111 0.08333333
```

2. `m * c(1, 0, -1)`


```{.output}
     [,1] [,2] [,3] [,4]
[1,]    1    4    7   10
[2,]    0    0    0    0
[3,]   -3   -6   -9  -12
```

3. `m > c(0, 20)`


```{.output}
      [,1]  [,2]  [,3]  [,4]
[1,]  TRUE FALSE  TRUE FALSE
[2,] FALSE  TRUE FALSE  TRUE
[3,]  TRUE FALSE  TRUE FALSE
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 4

Estamos interesados en encontrar la suma de la
siguiente secuencia de fracciones:


```r
 x = 1/(1^2) + 1/(2^2) + 1/(3^2) + ... + 1/(n^2)
```

Esto sería tedioso de escribir, e imposible para valores altos de
n. Usa vectorización para calcular x cuando n=100. ¿Cuál es la suma cuando
n=10.000?

:::::::::::::::  solution

## Solución al desafío 4

Estamos interesados en encontrar la suma de la
siguiente secuencia de fracciones:


```r
 x = 1/(1^2) + 1/(2^2) + 1/(3^2) + ... + 1/(n^2)
```

Esto sería tedioso de escribir, e imposible para
valores altos de n.
¿Puedes usar vectorización para calcular x, cuando n=100?
¿Qué tal cuando n=10,000?


```r
sum(1/(1:100)^2)
```

```{.output}
[1] 1.634984
```

```r
sum(1/(1:1e04)^2)
```

```{.output}
[1] 1.644834
```

```r
n <- 10000
sum(1/(1:n)^2)
```

```{.output}
[1] 1.644834
```

Podemos obtener el mismo resultado usando una función:


```r
inverse_sum_of_squares <- function(n) {
  sum(1/(1:n)^2)
}
inverse_sum_of_squares(100)
```

```{.output}
[1] 1.634984
```

```r
inverse_sum_of_squares(10000)
```

```{.output}
[1] 1.644834
```

```r
n <- 10000
inverse_sum_of_squares(n)
```

```{.output}
[1] 1.644834
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- Uso de operaciones vectorizadas en lugar de bucles.

::::::::::::::::::::::::::::::::::::::::::::::::::


