---
title: Introducción a R y RStudio
teaching: 45
exercises: 10
source: Rmd
---

::::::::::::::::::::::::::::::::::::::: objectives

- Describir el propósito y el uso de cada panel del RStudio IDE
- Ubicar botones y opciones en RStudio IDE
- Definir una variable
- Asignar un dato a una variable
- Administrar un espacio de trabajo en una sesión R interactiva
- Usar operadores matemáticos y de comparación
- Llamar funciones
- Gestionar paquetes

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo orientarse en RStudio?
- ¿Cómo interactuar con R?
- ¿Cómo administrar tu entorno?
- ¿Cómo instalar paquetes?

::::::::::::::::::::::::::::::::::::::::::::::::::



## Motivación

La ciencia es un proceso de varios pasos: una vez que hayas diseñado un experimento y recopilado datos, ¡comienza la verdadera diversión!
Esta lección te enseñará cómo comenzar este proceso usando R y RStudio. Comenzaremos con datos brutos, realizaremos análisis exploratorios
y aprenderemos a trazar gráficamente los resultados. Este ejemplo comienza con un conjunto de datos de [gapminder.org](https://www.gapminder.org)
que contiene información sobre la población de muchos países a lo largo del tiempo. ¿Puedes leer estos datos en R? ¿Puedes hacer un gráfico de
la población de Senegal? ¿Puedes calcular el ingreso promedio de los países del continente asiático? Al final de estas lecciones,
¡podrás hacer cosas como graficar datos de poblaciones de estos países en menos de un minuto!

## Antes de empezar el taller

Asegúrate de tener instalada la última versión de R y RStudio en tu máquina. Esto es importante, ya que algunos paquetes utilizados en el
taller pueden no instalarse correctamente (o no funcionar) si R no está actualizado.

[Descarga e instala la última versión de R aquí](https://www.r-project.org/),
[descarga e instala RStudio aquí](https://www.rstudio.com/)

## Introducción a RStudio

Bienvenido a la parte R del taller de Software Carpentry.

A lo largo de esta lección, vamos a enseñarte algunos de los fundamentos del lenguaje R, así como algunas buenas prácticas para organizar el
código de proyectos científicos que harán tu vida más fácil.

Usaremos RStudio: un entorno de desarrollo integrado y gratuito de código abierto. RStudio proporciona un editor incorporado, funciona en todas
las plataformas (incluso en servidores) y ofrece muchas ventajas, como la integración de control de versiones y gestión de proyectos.

**Diseño básico**

Cuando abres por primera vez el RStudio, serás recibido por tres paneles:

- La consola interactiva de R (a la izquierda)
- Ambiente/Historial (en la esquina superior derecha)
- Archivos/Gráficos/Paquetes/Ayuda/Visor (abajo a la derecha)

![](fig/01-rstudio.png){alt='RStudio layout'}

Si abres archivos, como los scripts R, también se abrirá un panel de editor en la esquina superior izquierda.

![](fig/01-rstudio-script.png){alt='RStudio layout with .R file open'}

## Flujo de trabajo dentro de RStudio

Hay dos formas principales en que uno puede trabajar dentro de RStudio.

1. Probar y jugar dentro de la consola interactiva de R y luego copiar el código en un archivo .R para ejecutarlo más tarde.
  - Esto funciona bien cuando se hacen pequeñas pruebas y/o se está comenzando.
  - Rápidamente se vuelve laborioso.
2. Comienza a escribir un archivo en .R y usa las teclas de acceso directo de RStudio para ejecutar la línea actual, las líneas seleccionadas o modificadas en la consola interactiva.
  - Esta es una buena forma de comenzar; todo tu código estará guardado para después.
  - Podrás ejecutar el archivo que quieres desde RStudio o mediante la función `source ()` de R.

:::::::::::::::::::::::::::::::::::::::::  callout

## Sugerencia: Ejecutando segmentos/secciones de tu código

RStudio ofrece gran flexibilidad para ejecutar código desde dentro de la ventana del editor
Hay botones, opciones de menú y atajos de teclado. Para ejecutar la línea actual, puedes

1. hacer clic en el botón `Run` arriba en el panel del Editor, o  2. Seleccionar "Run Lines" desde el menú
  "Code", o  3. Presionar Ctrl-Enter en Windows o Linux o Command-Enter en OS X. (Este atajo también se
  puede hacer colocando el mouse sobre el botón). Para ejecutar un bloque de código, selecciónalo y luego
  pulsa `Run`. Si has modificado una línea de código dentro de un bloque que acabas de ejecutar,
  no es necesario re-seleccionar el bloque y `Run`, puedes usar el botón
  `Re-run the previous region`. Esto ejecutará el bloque de código anterior, incluidas las modificaciones que
  hayas realizado.
  

::::::::::::::::::::::::::::::::::::::::::::::::::

## Introducción a R

Gran parte de tu tiempo en R lo gastarás en la consola interactiva de R. Aquí es donde ejecutarás todo tu código,
y puede ser un entorno útil para probar ideas antes de guardarlas en un script R. La consola en RStudio es la misma que
obtendrías si escribieras `R` en la terminal de shell/linea de comandos.

Lo primero que verás en la sesión interactiva de R es un montón de información, seguido por un ">" y un cursor parpadeante.
Esto es similar al entorno de la terminal de shell que aprendiste durante las lecciones de shell: R opera con la misma idea
de "leer, evaluar, mostrar" (tú escribes comandos, R intenta ejecutarlos y luego devuelve un resultado).

## Usando R como una calculadora

Lo más simple que podrías hacer con R es aritmética:


``` r
1 + 100
```

``` output
[1] 101
```

R te mostrará la respuesta, precedido de un "[1]". No te preocupes por esto por ahora, lo explicaremos más adelante. Por ahora piensa en eso como parte de la salida.

Al igual que bash, si escribes un comando incompleto R esperará a que lo completes:

```r
> 1 +
```

```output
+
```

Cada vez que presionas Enter y R te muestra un "+" en lugar de ">", significa que está esperando que completes el comando. Si deseas cancelar un comando, simplemente presiona "Esc" y RStudio te devolverá el ">" **prompt**.

:::::::::::::::::::::::::::::::::::::::::  callout

## Sugerencia: Cancelando comandos

Si usas R desde la línea de comandos en lugar de estar dentro de RStudio,
debes usar `Ctrl + C` en lugar de` Esc` para cancelar el comando.
¡Esto se aplica también a los usuarios de Mac!

La cancelación de un comando no sólo es útil para matar comandos incompletos:
también puedes usarlo para decirle a R que deje de ejecutar el código (por ejemplo, si tarda
mucho más de lo que esperabas), o para deshacerte del código que estás escribiendo actualmente.


::::::::::::::::::::::::::::::::::::::::::::::::::

Cuando usas R como calculadora, el orden de las operaciones es el mismo que has aprendido en la escuela.

De mayor a menor precedencia:

- Paréntesis: `(`, `)`
- Exponente: `^` o `**`
- División: `/`
- Multiplicación: `*`
- Suma: `+`
- Resta: `-`


``` r
3 + 5 * 2
```

``` output
[1] 13
```

Usa paréntesis para agrupar las operaciones a fin de forzar el orden de la evaluación o para aclarar lo que deseas hacer.


``` r
(3 + 5) * 2
```

``` output
[1] 16
```

Esto puede ser difícil de manejar cuando no es necesario, pero aclara tus intenciones.
Recuerda que otros pueden leer tu código.


``` r
(3 + (5 * (2 ^ 2))) # difícil de leer
3 + 5 * 2 ^ 2       # claro, si recuerdas las reglas
3 + 5 * (2 ^ 2)     # si olvidas algunas reglas, esto podría ayudar
```

El texto después de cada línea de código se llama "comentario". Todo lo que sigue después del símbolo hash (o numeral) `#` es ignorado por R cuando se ejecuta el código.

Los números pequeños o grandes tienen una notación científica:


``` r
2/10000
```

``` output
[1] 2e-04
```

Es la abreviatura de "multiplicado por `10 ^ XX` ". Entonces `2e-4` es la abreviatura de `2 * 10^(-4)`.

Tú también puedes escribir números en notación científica:


``` r
5e3  # nota la falta del signo menos aquí
```

``` output
[1] 5000
```

## Funciones matemáticas

R tiene muchas funciones matemáticas integradas. Para llamar a una función, simplemente escribimos su nombre seguido de paréntesis ( ).
Todo lo que escribas dentro de los paréntesis se llaman argumentos de la función:


``` r
sin(1)  # función trigonométrica
```

``` output
[1] 0.841471
```


``` r
log(1)  # logaritmo natural
```

``` output
[1] 0
```


``` r
log10(10) # logaritmo en base-10
```

``` output
[1] 1
```


``` r
exp(0.5) # e^(1/2)
```

``` output
[1] 1.648721
```

No te preocupes si no recuerdas todas las funciones en R. Simplemente puedes buscarlas en Google,
o si puedes recordar el comienzo del nombre de la función, puedes usar el tabulador para completar su nombre en RStudio.

Esta es una de las ventajas que RStudio tiene sobre R, tiene capacidades de autocompletado que te permiten buscar funciones, sus argumentos y los valores que toman más fácilmente.

Escribir un `?` antes del nombre de un comando abrirá la página de ayuda para ese comando. Además de proporcionar una
descripción detallada del comando y cómo funciona, al desplazarse hacia la parte inferior de la página de ayuda generalmente
se mostrarán ejemplos que ilustran el uso del comando. Veremos un ejemplo más adelante.
Puedes consultar también [las guías rápidas](https://raw.githubusercontent.com/rstudio/cheatsheets/master/translations/spanish/introduccion-a-r.pdf)
disponibles en el sitio de RStudio.

## Comparando

Podemos realizar comparaciones en R:


``` r
1 == 1  # igualdad (observa dos signos iguales, se lee como "es igual a")
```

``` output
[1] TRUE
```


``` r
1 != 2  # desigualdad (leída como "no es igual a")
```

``` output
[1] TRUE
```


``` r
1 < 2  # menor que
```

``` output
[1] TRUE
```


``` r
1 <= 1  # menor o igual que
```

``` output
[1] TRUE
```


``` r
1 > 0  # mayor que
```

``` output
[1] TRUE
```


``` r
1 >= -9 # mayor o igual que
```

``` output
[1] TRUE
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Sugerencia: Comparando números

Una advertencia sobre la comparación de números:
nunca debes usar `==` para comparar dos números a menos que
sean enteros (**integer** es un tipo de datos que
específica números enteros).

Las computadoras sólo pueden representar números decimales con
un cierto grado de precisión, así que dos números que parecen iguales
cuando se muestran por R, pueden tener diferentes representaciones
subyacentes y por lo tanto ser diferentes por un pequeño margen de error
(llamado tolerancia numérica de la máquina).

En su lugar, debes usar la función `all.equal`.

Lectura adicional: [http://floating-point-gui.de/](https://floating-point-gui.de/)

::::::::::::::::::::::::::::::::::::::::::::::::::

## Variables y asignaciones

Podemos almacenar valores en variables usando el operador de asignación `<-`. Veamos un ejemplo:


``` r
x <- 1/40
```

Observa que la asignación no muestra el valor. En cambio, lo almacena para más adelante en algo llamado **variable**. `x` ahora contiene el **valor** `0.025`:


``` r
x
```

``` output
[1] 0.025
```

Más precisamente, el valor almacenado es una *aproximación decimal* de esta fracción, llamado [número de coma flotante o **floating point**](https://en.wikipedia.org/wiki/Floating_point).

Busca la pestaña `Environment` en uno de los paneles de RStudio, y verás que `x` y su valor han aparecido. Nuestra variable `x` se puede usar en lugar de un número en cualquier cálculo que espere un número:


``` r
log(x)
```

``` output
[1] -3.688879
```

Ten en cuenta que las variables pueden reasignarse, es decir, puedes cambiar el valor almacenado en la variable:


``` r
x <- 100
```

`x` tenía el valor `0.025` y ahora tiene el valor `100`.

También, los valores de asignación pueden contener la variable asignada:


``` r
x <- x + 1 # observa cómo RStudio actualiza la descripción de x en la pestaña superior derecha
y <- x * 2
```

El lado derecho de la asignación puede ser cualquier expresión de R válida.
La expresión del lado derecho *se evalúa por completo* antes de que se realice la asignación.

Los nombres de las variables pueden contener letras, números, guiones bajos y puntos. No pueden comenzar con un número ni contener espacios en absoluto. Diferentes personas usan diferentes convenciones para nombres largos de variables, estos incluyen

- puntos.entre.palabras
- guiones\_bajos\_entre\_palabras
- MayúsculasMinúsculasParaSepararPalabras

Lo que uses depende de ti, pero **sé consistente**.

También es posible utilizar el operador `=` para la asignación:


``` r
x = 1/40
```

Esta forma es menos común entre los usuarios R. Lo más importante es
**ser consistente** con el operador que usas. Ocasionalmente hay lugares
donde es menos confuso usar `<-` que `=`, y es el símbolo más común usado en la comunidad.
Entonces la recomendación es usar `<-`.

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 1

De los siguientes ejemplos, ¿Cuáles son nombres de variables válidas en R?


``` r
min_height
max.height
_age
.mass
MaxLength
min-length
2widths
celsius2kelvin
```

:::::::::::::::  solution

## Solución al desafío 1

Los siguientes nombres de variables son válidos en R:


``` r
min_height
max.height
MaxLength
celsius2kelvin
```

El punto al inicio crea una variable oculta:


``` r
.mass
```

Los siguientes no son nombres de variables válidos en R:


``` r
_age
min-length
2widths
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Vectorización

Es muy importante tener en cuenta que R es *vectorizado*, lo que significa que las variables y funciones pueden tener vectores como valores y R puede operar en vectores completos a la vez.
En contraste con los conceptos de vectores de física y matemáticas, un vector en R describe un conjunto de valores del
mismo tipo de datos en un cierto orden. Por ejemplo:


``` r
1:5
```

``` output
[1] 1 2 3 4 5
```

``` r
2^(1:5)
```

``` output
[1]  2  4  8 16 32
```

``` r
x <- 1:5
2^x
```

``` output
[1]  2  4  8 16 32
```

Esto es increíblemente poderoso; discutiremos esto en una próxima lección.

## Administrando tu entorno

Hay algunos comandos útiles que puedes usar para interactuar con la sesión de R.

`ls` listará todas las variables y funciones almacenadas en el entorno global
(tu sesión de trabajo en R):


``` r
ls()
```

``` output
[1] "object" "x"      "y"     
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Sugerencia: ocultando objetos

Al igual que en el shell, `ls` oculta por defecto cualquier variable o función que comience
con un ".". Para listar todos los objetos, escribe `ls(all.names = TRUE)`

::::::::::::::::::::::::::::::::::::::::::::::::::

Ten en cuenta que no se dió ningún argumento a `ls`, pero sí se necesita poner los paréntesis
para decirle a R que llame a la función.

Si escribimos `ls` nada más, ¡R mostrará el código fuente de esa función!


``` r
ls
```

``` output
function (name, pos = -1L, envir = as.environment(pos), all.names = FALSE, 
    pattern, sorted = TRUE) 
{
    if (!missing(name)) {
        pos <- tryCatch(name, error = function(e) e)
        if (inherits(pos, "error")) {
            name <- substitute(name)
            if (!is.character(name)) 
                name <- deparse(name)
            warning(gettextf("%s converted to character string", 
                sQuote(name)), domain = NA)
            pos <- name
        }
    }
    all.names <- .Internal(ls(envir, all.names, sorted))
    if (!missing(pattern)) {
        if ((ll <- length(grep("[", pattern, fixed = TRUE))) && 
            ll != length(grep("]", pattern, fixed = TRUE))) {
            if (pattern == "[") {
                pattern <- "\\["
                warning("replaced regular expression pattern '[' by  '\\\\['")
            }
            else if (length(grep("[^\\\\]\\[<-", pattern))) {
                pattern <- sub("\\[<-", "\\\\\\[<-", pattern)
                warning("replaced '[<-' by '\\\\[<-' in regular expression pattern")
            }
        }
        grep(pattern, all.names, value = TRUE)
    }
    else all.names
}
<bytecode: 0x55b26aa87d80>
<environment: namespace:base>
```

Puedes usar `rm` para eliminar objetos que ya no necesitas:


``` r
rm(x)
```

Si tienes muchas cosas en tu entorno y deseas borrarlas todas,
puedes pasar los resultados de `ls` y mandarlos a la función `rm`:


``` r
rm(list = ls())
```

En este caso, hemos combinado los dos. Al igual que el orden de las operaciones, todo lo que se encuentre dentro de los paréntesis más internos se evalúa primero, y así sucesivamente.

En este caso, hemos especificado que los resultados de `ls` se deben usar para el argumento `list` y luego remover la lista con `rm`. Cuando asignes valores a argumentos por su nombre, *debes* usar el operador `=`.

Si, en cambio, usamos `<-`, habrá efectos secundarios no deseados, o puedes recibir un mensaje de error:


``` r
rm(list <- ls())
```

``` error
Error in rm(list <- ls()): ... must contain names or character strings
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Sugerencia: Advertencias vs. Errores

¡Presta atención cuando R hace algo inesperado! Los errores, como el anterior,
se lanzan cuando R no puede proceder a un cálculo. Por otro lado, las advertencias
generalmente significan que la función se ha ejecutado, pero probablemente
no funcionó como se esperaba.

En ambos casos, el mensaje que muestra R usualmente te da pistas sobre cómo
solucionar el problema.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Paquetes en R

Es posible agregar funciones a R escribiendo un paquete u obteniendo un paquete escrito
por otra persona. Hay más de 10.000 paquetes disponibles en CRAN (la red completa de archivos R).
R y RStudio tienen funcionalidad para administrar paquetes:

- Puedes ver qué paquetes están instalados escribiendo `installed.packages()`
- Puedes instalar paquetes escribiendo `install.packages("nombre_de_paquete")`
- Puedes actualizar los paquetes instalados escribiendo `update.packages()`
- Puedes eliminar un paquete con `remove.packages("nombre_de_paquete")`
- Puedes hacer que un paquete esté disponible para su uso con `library(nombre_de_paquete)`

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 2

¿Cuál será el valor de cada variable después de cada comando en el siguiente programa?


``` r
mass <- 47.5
age <- 122
mass <- mass * 2.3
age <- age - 20
```

:::::::::::::::  solution

## Solución al desafío 2


``` r
mass <- 47.5
```

Esto dará un valor de 47.5 para la variable mass


``` r
age <- 122
```

Esto dará un valor de 122 para la variable age


``` r
mass <- mass * 2.3
```

Multiplica el valor existente en mass 47.5 por 2.3 para dar un nuevo valor
109\.25 a la variable mass.


``` r
age <- age - 20
```

Resta 20 del valor existente de 122 para obtener un nuevo valor
de 102 para la variable age.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 3

Ejecuta el código del desafío anterior y escribe un comando para comparar la variable `mass` con `age`.
¿Es la variable `mass` más grande que `age`?

:::::::::::::::  solution

## Solución del desafío 3

Una forma de responder esta pregunta en R es usar `>` para hacer lo siguiente:


``` r
mass > age
```

``` output
[1] TRUE
```

Esto debería dar un valor booleano `TRUE` ya que 109.25 es mayor que 102.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 4

Limpia tu entorno de trabajo borrando las variables de `mass` y `age`.

:::::::::::::::  solution

## Solución al desafío 4

Podemos usar el comando `rm` para realizar esta tarea:


``` r
rm(age, mass)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 5

Instala los siguientes paquetes: `ggplot2`, `plyr`, `gapminder`.

:::::::::::::::  solution

## Solución al desafío 5

Puedes utilizar el comando `install.packages()` para instalar los paquetes requeridos.


``` r
install.packages("ggplot2")
install.packages("plyr")
install.packages("gapminder")
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- Usa RStudio para escribir y correr programas en R.
- R tiene operadores aritméticos y funciones matemáticas usuales.
- Utilizar `<-` para asignar valores a variables.
- Utilizar `ls()` para listar las variables en el programa.
- Utilizar `rm()` para eliminar objetos en el programa.
- Utilizar `install.packages()` para instalar paquetes (libraries).

::::::::::::::::::::::::::::::::::::::::::::::::::


