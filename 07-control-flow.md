---
title: Control de flujo
teaching: 45
exercises: 20
source: Rmd
---

::::::::::::::::::::::::::::::::::::::: objectives

- Escribir declaraciones condicionales utilizando `if()` y `else()`.
- Escribir y entender los bucles con `for()`.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo hacer elecciones dependiendo de mis datos en R?
- ¿Cómo puedo repetir operaciones en R?

::::::::::::::::::::::::::::::::::::::::::::::::::

Cuando estamos programando puede que queramos controlar el flujo de nuestras acciones. Esto se puede realizar
estableciendo acciones que ocurran solo si se cumple una condición o un conjunto de condiciones.
A su vez, podemos hacer que una acción ocurra un número determinado de veces.

Hay varias maneras de controlar el flujo en R.
Para declaraciones condicionales, los enfoques más comúnmente utilizados son los **constructs**:


``` r
# if
if (la condición es verdad) {
  realizar una acción
}

# if ... else
if (la condición es verdad) {
  realizar una acción
} else {  # es decir, si la condición es falsa,
  realizar una acción alternativa
}
```

Digamos, por ejemplo, que queremos que R imprima un mensaje si una variable `x` tiene un valor en particular:


``` r
x <- 8

if (x >= 10) {
  print("x es mayor o igual que 10")
}

x
```

``` output
[1] 8
```

La sentencia **print**  "x es mayor o igual que 10" no aparece en la consola porque x no es mayor o igual a 10. Para imprimir un mensaje diferente para numeros menores a 10, podemos agregar una sentencia **else**


``` r
x <- 8

if (x >= 10) {
  print("x es mayor o igual a 10")
} else {
  print("x es menor a 10")
}
```

``` output
[1] "x es menor a 10"
```

También podemos testear múltiples condiciones usando **else if**


``` r
x <- 8

if (x >= 10) {
  print("x es mayor o igual a 10")
} else if (x > 5) {
  print("x es mayor a 5, pero menor a 10")
} else{
  print("x es menor a 5")
}
```

``` output
[1] "x es mayor a 5, pero menor a 10"
```

**Importante:** cuando R evalúa las condiciones dentro de `if()` esta buscando
elementos lógicos como `TRUE` o `FALSE`. Entender esto puede ser un dolor de cabeza para
los principiantes. Por ejemplo:


``` r
x  <-  4 == 3
if (x) {
  "4 igual a 3"
} else {
  "4 no es igual a 3"
}
```

``` output
[1] "4 no es igual a 3"
```

Como podemos observar se muestra el mensaje es igual porque el vector x es `FALSE`


``` r
x <- 4 == 3
x
```

``` output
[1] FALSE
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 1

Usa una declaración `if()` para mostrar un mensaje adecuado
reportando si hay algún registro del año 2002 en
el **dataset** **`gapminder`**.
Luego haz lo mismo para el año 2012.

:::::::::::::::  solution

## Solución al Desafío 1

Primero veremos una solución al Desafío 1 que no usa la función `any()`.
Primero obtenemos un vector lógico que describe que el elemento `gapminder$year` es igual a `2002`:


``` r
gapminder[(gapminder$year == 2002),]
```

Luego, contamos el número de filas del data.frame `gapminder` que corresponde al año 2002:


``` r
rows2002_number <- nrow(gapminder[(gapminder$year == 2002),])
```

La presencia de cualquier registro para el año 2002 es equivalente a la petición de que `rows2002_number` sea mayor o igual a uno:


``` r
rows2002_number >= 1
```

Entonces podríamos escribir:


``` r
if(nrow(gapminder[(gapminder$year == 2002),]) >= 1){
   print("Se encontraron registro(s) para el año 2002.")
}
```

Todo esto se puede hacer más rápido con `any()`. En dicho caso la condición lógica se puede expresar como:


``` r
if(any(gapminder$year == 2002)){
   print("Se encontraron registro(s) para el año 2002.")
}
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

¿Alguien recibió un mensaje de advertencia como este?


``` error
Error: object 'gapminder' not found
```

Si tu condición se evalúa como un vector con más de un elemento lógico,
la función `if()` todavía se ejecutará, pero solo evaluará la condición en el primer
elemento. Aquí debes asegurarte que tu condición sea de longitud 1.

:::::::::::::::::::::::::::::::::::::::::  callout

## Tip: `any()` y `all()`

La función `any()` devolverá TRUE si hay al menos un valor
TRUE dentro del vector, en caso contrario devolverá `FALSE`.
Esto se puede usar de manera similar al operador `%in%`.
La función `all()`, como el nombre sugiere, devolvera `TRUE` siempre y cuando todos los valores en
el vector son `TRUE`.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Operaciones repetidas

Si quieres iterar sobre un conjunto de valores, el orden de la iteración es importante y debes realizar
la misma operación en cada uno, un bucle `for()` es lo que estas buscando.
Vimos los bucles `for()` en las lecciones anteriores de terminal. Si bien esta es la
operación de bucle más flexible es también la más difícil de usar correctamente.
Evita usar bucles `for()` a menos que el orden de la iteración sea importante
como cuando el cálculo de cada iteración dependa del resultado de la iteración previa.

La estructura básica de un bucle `for()` es:


``` r
for(iterador in conjunto de valores){
  haz alguna acción
}
```

Por ejemplo:


``` r
for(i in 1:10){
  print(i)
}
```

``` output
[1] 1
[1] 2
[1] 3
[1] 4
[1] 5
[1] 6
[1] 7
[1] 8
[1] 9
[1] 10
```

El rango `1:10`  crea un vector sobre la marcha; puedes iterar
sobre cualquier otro vector también.

Podemos usar un bucle `for()`  anidado con otro bucle `for()` para iterar sobre dos cosas
a la vez.


``` r
for(i in 1:5){
  for(j in c('a', 'b', 'c', 'd', 'e')){
    print(paste(i,j))
  }
}
```

``` output
[1] "1 a"
[1] "1 b"
[1] "1 c"
[1] "1 d"
[1] "1 e"
[1] "2 a"
[1] "2 b"
[1] "2 c"
[1] "2 d"
[1] "2 e"
[1] "3 a"
[1] "3 b"
[1] "3 c"
[1] "3 d"
[1] "3 e"
[1] "4 a"
[1] "4 b"
[1] "4 c"
[1] "4 d"
[1] "4 e"
[1] "5 a"
[1] "5 b"
[1] "5 c"
[1] "5 d"
[1] "5 e"
```

En lugar de mostrar los resultados en la pantalla podríamos guardarlos en un nuevo objeto.


``` r
output_vector <- c()
for(i in 1:5){
  for(j in c('a', 'b', 'c', 'd', 'e')){
    temp_output <- paste(i, j)
    output_vector <- c(output_vector, temp_output)
  }
}
output_vector
```

``` output
 [1] "1 a" "1 b" "1 c" "1 d" "1 e" "2 a" "2 b" "2 c" "2 d" "2 e" "3 a" "3 b"
[13] "3 c" "3 d" "3 e" "4 a" "4 b" "4 c" "4 d" "4 e" "5 a" "5 b" "5 c" "5 d"
[25] "5 e"
```

Este enfoque puede ser útil, pero aumentar o incrementar tus resultados (es decir, construir el objeto resultante de forma incremental) es computacionalmente ineficiente por lo que conviene evitarlo cuando estés iterando a través de muchos valores.

:::::::::::::::::::::::::::::::::::::::::  callout

## Tip: no incrementes tus resultados

Una de las cosas que más frecuentemente hace tropezar tanto a los principiantes como
a los usuarios experimentados de R es la construcción de un objeto de resultados
(vector, lista, matriz, data frame) a medida que tu bucle for progresa.
Las computadoras son muy malas para manejar esto lo cual puede hacer que tus cálculos
se enlentezcan rápidamente. En este caso es mejor definir un objeto de
resultados vacío con las dimensiones apropiadas.
Si sabes que el resultado final se almacenará en una matriz como la
anterior es una buena idea crear una matriz vacía con 5 filas y 5 columnas y luego en cada iteración
almacenar los resultados en la ubicación adecuada.


::::::::::::::::::::::::::::::::::::::::::::::::::

Una mejor manera es definir el objeto de salida (vacío) antes de completar los valores.
Aunque para este ejemplo parece más complicado, es aún más eficiente.


``` r
output_matrix <- matrix(nrow=5, ncol=5)
j_vector <- c('a', 'b', 'c', 'd', 'e')
for(i in 1:5){
  for(j in 1:5){
    temp_j_value <- j_vector[j]
    temp_output <- paste(i, temp_j_value)
    output_matrix[i, j] <- temp_output
  }
}
output_vector2 <- as.vector(output_matrix)
output_vector2
```

``` output
 [1] "1 a" "2 a" "3 a" "4 a" "5 a" "1 b" "2 b" "3 b" "4 b" "5 b" "1 c" "2 c"
[13] "3 c" "4 c" "5 c" "1 d" "2 d" "3 d" "4 d" "5 d" "1 e" "2 e" "3 e" "4 e"
[25] "5 e"
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Tip: Bucles While

Algunas veces tendrás la necesidad de repetir una operación hasta que
cierta condición se cumpla. Puedes hacer esto con un bucle `while()`.


``` r
while(mientras esta condición es verdad){
  haz algo
}
```

A modo de ejemplo aquí hay un bucle while que genera números aleatorios a
partir de una distribución uniforme (la función `runif()` ) entre 0 y 1 hasta
que obtiene uno que es menor a 0.1.


``` r
z <- 1
while(z > 0.1){
  z <- runif(1)
  print(z)
}
```

Los bucles `while()` no siempre serán la elección apropiada. Debes ser
particularmente cuidadoso de que tu condición se cumpla y no terminar en un
bucle infinito.


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 2

Compara los objetos output\_vector y output\_vector2. ¿Son lo mismo? Si no, ¿por qué no?
¿Cómo cambiarías el último bloque de código para hacer output\_vector2 igual a output\_vector?

:::::::::::::::  solution

## Solución al Desafío 2

Podemos verificar si dos vectores son idénticos usando la función `all()` :


``` r
all(output_vector == output_vector2)
```

Sin embargo todos los elementos de `output_vector` se pueden encontrar en `output_vector2`:


``` r
all(output_vector %in% output_vector2)
```

y viceversa:


``` r
all(output_vector2 %in% output_vector)
```

Por lo tanto, los elementos en `output_vector` y `output_vector2` están en distinto orden.
Esto es porque `as.vector ()` genera los elementos leyendo la matriz de entrada por columnas.
Si observamos `output_matrix` podemos notar que deseamos obtener sus elementos ordenados por filas.
La solución es transponer la `output_matrix`. Podemos hacerlo llamando a la función de transposición
`t ()` o ingresando los elementos en el orden correcto.
La primera solución requiere cambiar el original


``` r
output_vector2 <- as.vector(output_matrix)
```

por


``` r
output_vector2 <- as.vector(t(output_matrix))
```

La segunda solución requiere cambiar


``` r
output_matrix[i, j] <- temp_output
```

por


``` r
output_matrix[j, i] <- temp_output
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 3

Escribe un **script** que a través de bucles recorra los datos `gapminder` por continente e imprima
si la esperanza de vida media es menor o mayor de 50
años.

:::::::::::::::  solution

## Solución al Desafío 3

**Paso 1**: Queremos asegurarnos de que podamos extraer todos los valores únicos del vector continente


``` r
gapminder <- read.csv("data/gapminder-FiveYearData.csv")
unique(gapminder$continent)
```

**Paso 2**: También tenemos que recorrer cada uno de estos continentes y calcular la esperanza de vida promedio para cada "subconjunto" de datos.
Podemos hacer eso de la siguiente manera:

1. Recorre cada uno de los valores únicos de 'continente'
2. Para cada valor de continente, crea una variable temporal que almacene la vida útil para ese subconjunto,
3. Regresar la expectativa de vida calculada al usuario imprimiendo el resultado:


``` r
for( iContinent in unique(gapminder$continent) ){
   tmp <- mean(subset(gapminder, continent==iContinent)$lifeExp)
   cat("Average Life Expectancy in", iContinent, "is", tmp, "\n")
   rm(tmp)
}
```

**Paso 3**: El ejercicio solo requiere que se imprima el resultado si la expectativa de vida promedio es menor a 50 o superior a 50. Por lo tanto, debemos agregar una condición 'if' antes de imprimir, lo cual evalúa si la expectativa de vida promedio calculada es superior o inferior a un umbral, e imprime una salida condicional en el resultado.
Necesitamos corregir (3) desde arriba:

3a. Si la esperanza de vida calculada es menor que algún umbral (50 años), devuelve el continente e imprime la frase "la esperanza de vida es menor que el umbral", de lo contrario devuelve el continente e imprime la frase "la esperanza de vida es mayor que el umbral":


``` r
thresholdValue <- 50

for( iContinent in unique(gapminder$continent) ){
   tmp <- mean(subset(gapminder, continent==iContinent)$lifeExp)
   
   if(tmp < thresholdValue){
       cat("Average Life Expectancy in", iContinent, "is less than", thresholdValue, "\n")
   }
   else{
       cat("Average Life Expectancy in", iContinent, "is greater than", thresholdValue, "\n")
        } # end if else condition
   rm(tmp)
   } # end for loop
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 4

Modifica el **script** del Desafío 4 para obtener resultados para cada uno de los
países. En esta oportunidad que imprima si la esperanza de vida es menor que 50, se encuentra entre 50 y 70 o es mayor que 70.

:::::::::::::::  solution

## Solución al Desafío 4

Modificamos nuestra solución al Reto 3 agregando ahora dos umbrales, `lowerThreshold` y` upperThreshold` y extendiendo nuestras declaraciones if-else:


``` r
 lowerThreshold <- 50
 upperThreshold <- 70

for( iCountry in unique(gapminder$country) ){
    tmp <- mean(subset(gapminder, country==iCountry)$lifeExp)

    if(tmp < lowerThreshold){
        cat("Average Life Expectancy in", iCountry, "is less than", lowerThreshold, "\n")
    }
    else if(tmp > lowerThreshold && tmp < upperThreshold){
        cat("Average Life Expectancy in", iCountry, "is between", lowerThreshold, "and", upperThreshold, "\n")
    }
    else{
        cat("Average Life Expectancy in", iCountry, "is greater than", upperThreshold, "\n")
    }
    rm(tmp)
}
```

``` error
Error: object 'gapminder' not found
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 5 - Avanzado

Escribir un script que con un bucle recorra cada país en el **dataset**
**`gapminder`**, probar si el país comienza con una 'B' y graficar la
esperanza de vida contra el tiempo como un gráfico de líneas si la esperanza
de vida media es menor de 50 años.

:::::::::::::::  solution

## Solución para el Desafío 5

Lo primero que vamos a hacer es usar el comando `grep` que se introdujo en
la lección Shell de Unix para encontrar países que comiencen con" B "."

Si seguimos la lección de Shell de Unix podríamos vernos tentados de probar
lo siguiente


``` r
grep("^B", unique(gapminder$country))
```

Pero cuando evaluamos este comando obtenemos los índices de la variable del
factor `country` que comienza con "B".
Para obtener los valores, debemos agregar la opción `value = TRUE` al
comando` grep`:


``` r
grep("^B", unique(gapminder$country), value=TRUE)
```

A continuación almacenaremos estos países en una variable llamada
candidateCountries y luego con un bucle recorreremos cada entrada en la
variable.

Dentro del bucle se evaluará la expectativa de vida promedio para cada país
y de ser menor a 50 usamos un gráfico base para trazar la evolución de la
expectativa de vida promedio:


``` r
thresholdValue <- 50
candidateCountries <- grep("^B", unique(gapminder$country), value=TRUE)

for( iCountry in candidateCountries){
    tmp <- mean(subset(gapminder, country==iCountry)$lifeExp)

    if(tmp < thresholdValue){
        cat("Average Life Expectancy in", iCountry, "is less than", 
             thresholdValue, "plotting life expectancy graph... \n")

        with(subset(gapminder, country==iCountry),
                plot(year,lifeExp,
                     type="o",
                     main = paste("Life Expectancy in", iCountry, "over time"),
                     ylab = "Life Expectancy",
                     xlab = "Year"
                   ) # end plot
              ) # end with
    } # end for loop
    rm(tmp)
 }
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- Usar `if` y `else` para realizar elecciones.
- Usar `for` para operaciones repetidas.

::::::::::::::::::::::::::::::::::::::::::::::::::


