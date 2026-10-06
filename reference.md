---
title: 'Referencia'
---

## Referencia

## [Introducción a R y RStudio](episodes/01-rstudio-intro.md)

- Usa la tecla **escape** para cancelar comandos incompletos o código en ejecución
  (Ctrl+C) si estas usando R desde el **shell**.
- Las operaciones aritméticas básicas siguen el orden estándar de precedencia:
  - Paréntesis: `(`, `)`
  - Exponentes: `^` or `**`
  - División: `/`
  - Multiplicación: `*`
  - Suma: `+`
  - Resta: `-`
- La notación científica está disponible, por ejemplo: `2e-3`
- Cualquier cosa a la derecha de `#` es un comentario, R lo ignorará!
- Las funciones se denotan por `function_name()`. Las expresiones dentro de los paréntesis se evaluan antes de pasarse a la función, y las funciones se pueden anidar.
- Funciones matemáticas: `exp`, `sin`, `log`, `log10`, `log2` etc.
- Operadores de comparación: `<`, `<=`, `>`, `>=`, `==`, `!=`
- Usa `all.equal` para comparar valores numéricos!
- `<-` es el operador de asignación. Cualquier expresión a la derecha del operador es evaluada, luego se almacena en la variable nombrada a la izquierda.
- `ls` lista todas las variables y funciones que has creado
- `rm` puede utilizarse para borrarlas
- Al asignar valores a los argumentos de la función, debes usar `=`.

## [Manejo de proyectos con RStudio](episodes/02-project-intro.md)

- Para crear un nuevo proyecto, ve a File -> New Project
- Instala el paquete `packrat` para crear proyectos independientes
- `install.packages` para instalar paquetes desde CRAN
- `library` para cargar un paquete en R
- `packrat::status` para verificar si se han instalado todos los paquetes a los que se hace referencia en tus **scripts**.

## [Buscando ayuda](episodes/03-seeking-help.md)

- Para acceder a la ayuda de una función `?function_name` o `help(function_name)`
- Usa comillas para operadores especiales, por ejemplo: `?"+"`
- Utiliza la búsqueda ambigua si no puedes recordar un nombre `??search_term`
- [CRAN task views](https://cran.at.r-project.org/web/views) son un buen punto de partida.
- [Stack Overflow](https://stackoverflow.com/) es un buen lugar para obtener ayuda con tu código.
  - `?dput` Guardará datos que estás trabajando, para que otros puedan cargarlos fácilmente.
  - `sessionInfo()` te dará detalles de tu configuración.

## [Estructuras de datos](episodes/04-data-structures-part1.md)

Los valores atómicos en R deben ser de alguno de los 5 **tipos de datos**, múltiples valores se pueden agrupar en **estructuras de datos**.

**Tipos de datos**

- `typeof(object)` proporciona información sobre el tipo de dato de un objeto.

- Existen 5 tipos de datos principales:
  
  - `?numeric` números reales(decimal)
  - `?integer` sólo números enteros
  - `?character` texto
  - `?complex` números complejos
  - `?logical` valores **TRUE** o **FALSE**
  
  **Tipos especiales:**
  
  - `?NA` valores faltantes
  - `?NaN` "no es número" para valores indefinidos (por ejemplo, `0/0`).
  - `?Inf`, `-Inf` infinito.
  - `?NULL` una estructura de datos que no existe
  
  `NA` puede ocurrir en cualquier vector atómico. `NaN`, and `Inf` sólo pueden aparecer en vectores de tipo **complex**, **integer** o **numeric**. Los vectores atómicos son los bloques de construcción para todas las demás estructuras de datos. Un valor `NULL` ocurrirá en una estructura de datos entera (pero puede ocurrir como lista de elementos).

**Estructuras de datos básicas en R:**

- `?vector` atómico (sólo puede contener un tipo de dato)
- `?list` (contenedores para otros objetos)
- `?data.frame` objetos bidimensionales cuyas columnas pueden contener diferentes tipos de datos
- `?matrix` objeto bidimensional que puede contener sólo un tipo de dato.
- `?factor` vectores que contienen datos categóricos predefinidos.
- `?array` objeto multi-dimensional que puede contener sólo un tipo de dato.

Recuerda que las matrices son realmente vectores atómicos, y que los
**data.frames** son realmente listas(esto explica algunos de los comportamientos extraños de R).

**[Vectores](episodes/04-data-structures-part1.md)**

- `?vector()` Todos los elementos del vector deben ser del mismo tipo.
- Los elementos se pueden convertir de un tipo a otro utilizando *coerción*.
- La función concatenar 'c()' agrega elementos al vector.
- `seq(from=0, to=1, by=1)` crea una secuencia de números.
- Los elementos de un vector se pueden nombrar usando la función `names()`.

**[Factores](episodes/04-data-structures-part1.md)**

- `?factor()` Los factores son una estructura de datos diseñada para almacenar datos categóricos.
- `levels()` muestra los valores válidos que se pueden almacenar en un vector de tipo factor.

**[Listas](episodes/04-data-structures-part1.md)**

- `?list()` Las listas son una estructura de datos diseñada para almacenar datos de diferente tipos.

**[Matrices](episodes/04-data-structures-part1.md)**

- `?matrix()` Las matrices son una estructura de datos diseñada para almacenar datos bidimensionales.

**[Data Frames](episodes/05-data-structures-part2.md)**

- `?data.frame` es una estructura de datos clave. Es una `lista` de `vectores`.
- `cbind()` agregará una columna (vector) a un **data.frame**.
- `rbind()` agregará un renglón (list) a un **data.frame**.

**Funciones útiles para consultar estructuras de datos:**

- `?str` estructura, imprime un resumen de toda la estructura de datos
- `?typeof` te dice el tipo dentro de un vector atómico
- `?class` Indica cual es la estructura de datos
- `?head` Imprime los primeros `n` elementos (filas para objetos bidimensionales)
- `?tail` imprime los últimos `n` elementos (filas para objetos bidimensionales)
- `?rownames`, `?colnames`, `?dimnames` recupera o modifica los nombres de fila y columna de un objeto.
- `?names` recupera o modifica los nombres de un vector o lista atómica (o columnas de un **dataframe**).
- `?length` obtiene el número de elementos de un vector atómico
- `?nrow`, `?ncol`, `?dim` obtiene las dimensiones de un objeto n-dimensional
  (No funcionará en vectores o listas atómicas).

## [Explorando Dataframes](episodes/05-data-structures-part2.md)

- `read.csv` para leer datos en una estructura regular
  - `sep` argumento para especificar el separador
    - "," para valores separados por coma
    - "\\t" para valores separados por tabulador
  - Otros argumentos:
    - `header=TRUE` si hay una fila de encabezado

## [Subconjunto de datos](episodes/06-data-subsetting.md)

- Se puede acceder a los elementos por:
  
  - Indice
  - Nombre
  - Vectores lógicos

- `[` corchetes:
  
  - *extrae* elementos individuales o **subset** de vectores
  - por ejemplo,`x[1]` extrae el primer elemento del vector x.
  - *extrae* elementos individuales de una lista. El valor devuelto será otra `list()`.
  - *extrae* columnas de un **data.frame**.

- `[` con dos argumentos para:
  
  - *extrae* filas y/o columnas de
    - matrices
    - **data.frames**
    - por ejemplo: `x[1,2]` extraerá el valor de la fila 1, columna 2.
    - por ejemplo: `x[2,:]` extraerá toda la segunda fila.

- `[[` dobles corchetes para extraer elementos de las listas.

- `$` para acceder a columnas o listar elementos por nombre

- índices negativos omiten elementos

## [Control de flujo](episodes/07-control-flow.md)

- Usa la condición `if` para iniciar una instrucción condicional, `else if` para proporcionar pruebas adicionales, y `else` para proporcionar un valor predeterminado.
- Las instrucciones que se encuentran entre las llaves de las declaraciones condicionales deben estar indentadas.
- Usa `==` para probar la igualdad.
- `X && Y` sólo es cierto si tanto X como Y son `TRUE`.
- `X || Y` es cierto si ya sea X o Y, o ambos, son `TRUE`.
- Cero se considera `FALSE`; todos los demás números se consideran `TRUE`
- Anidar loops para operar en datos multidimensionales.

## [Creación de gráficos con calidad para publicación](episodes/08-plot-ggplot2.md)

- las figuras se pueden crear con la gramática de los gráficos:
  - `library(ggplot2)`
  - `ggplot` para crear la figura base
  - `aes`especifica la estética de los ejes de datos, la forma, color y tamaño
  - `geom`especifica el tipo de gráfico, por ejemplo, `point`, `line`, `density`, `box`
  - `geom`agrega también transformaciones estadísticas, por ejemplo. `geom_smooth`
  - `scale` funciones que controla la relación entre los valores de los datos y los valores visuales o estéticos
  - `facet` funciones para estratificar la figura en paneles
  - `aes` Las características estéticas se aplican a capas individuales, o se pueden establecer para todo el gráfico dentro de `ggplot`.
  - `theme` cambia el aspecto general del gráfico
  - ¡El orden de las capas importa!
  - `ggsave` salva una figura.

## [Vectorización](episodes/09-vectorization.md)

- La mayoría de las funciones y operaciones se aplican a cada elemento de un vector
- `*` la multiplicación de elemento a elemento
- `%*%` para una verdadera multiplicación de matrices
- `any()` regresará `TRUE` si cualquier elemento de un vector es `TRUE`
- `all()` regresará `TRUE` si *todos* los elementos de un vector son `TRUE`

## [Funciones](episodes/10-functions.md)

- `?"function"`
- Coloque el código cuyos parámetros cambian frecuentemente en una función, luego llámelo con diferentes valores de parámetros para personalizar su comportamiento.
- Se devuelve la última línea de una función, o puede usar `return` explícitamente
- Cualquier código escrito en el cuerpo de la función buscará preferiblemente variables definidas dentro de la función
- Documente ¿por qué?, luego ¿qué?, y finalmente ¿cómo? (si el código no se explica por sí mismo)

## [Escribiendo datos](episodes/11-writing-data.md)

- `write.table` para escribir objetos en formato regular
- asigna `quote = FALSE` para que el texto no sea envuelto entre comillas ` "`

## [Split-apply-combine](episodes/12-plyr.md)

- Use la familia de funciones `xxply` para aplicar funciones a grupos dentro de algunos datos.
- la primera letra, `a`rray,`d`ata.frame o `l`ist corresponde a los datos de entrada
- la segunda letra denota la estructura de datos de salida
- Las funciones anónimas (aquellas que no tienen un nombre asignado) se usan dentro de la familia de funciones `plyr`
  en grupos dentro de los datos.

## [Manejo de dataframe con dplyr](episodes/13-dplyr.md)

- `library(dplyr)`
- `?select` extrae variables por nombre.
- `?filter` regresa filas que coincidan con las condiciones.
- `?group_by` agrupa datos por una de muchas variables.
- `?summarize` resume valores múltiples a un solo valor.
- `?mutate` agrega nuevas variables a un **data.frame**.
- Combina operaciones usando el operador **pipe** `?"%>%"`.

## [Manejo de dataframe con tidyr](episodes/14-tidyr.md)

- `library(tidyr)`
- '?gather' convierte datos del formato *ancho* al *largo*.
- '?spread' convierte datos del formato *largo* al *ancho*.
- '?separate' separa un único valor en múltiples valores.
- '?unite' fusionar valores múltiples en un solo valor.

## [Generando reportes con knitr](episodes/15-knitr-markdown.md)

- Valor de informes reproducibles
- Conceptos básicos de Markdown
- fragmentos de código R
- Opciones de fragmentos
- Código R en línea
- Otros formatos de salida

## [Buenas prácticas para escribir un buen código](episodes/16-wrap-up.md)

- Programa defensivamente, es decir, asume que van a surgir errores y escribe el código para detectarlos cuando surjan.
- Escriba pruebas antes de escribir el código para ayudar a determinar exactamente qué se supone que debe hacer ese código.
- Conoce que se supone hace el código, antes de tratar de corregirlo.
- Haz que falle cada vez.
- Haz que falle rápido.
- Cambia una cosa a la vez, y por una razón.
- Ten un registro de lo que has hecho.
- Se humilde.

## Glosario

[argument]{#argument}
:   Un valor dado a una función o programa cuando se ejecuta.
El término a menudo se usa indistintamente (y de manera inconsistente) con [parámetro](#parameter).

[assign]{#assign}
:   Para darle a un valor un nombre asociandolo a una variable.

[body]{#body}
:   (de una función): las instrucciones que se ejecutan cuando se ejecuta una función.

[comment]{#comment}
:   Una observación en un programa que pretende ayudar a los lectores humanos a comprender lo que está sucediendo,
pero es ignorado por la computadora.
Los comentarios en Python, R y el shell de Unix comienzan con un caracter `#` y se ejecutan hasta el final de la linea;
los comentarios en SQL comienzan con `--`,
y otros idiomas tienen otras convenciones.

[comma-separated values]{#comma-separated-values}
:   (CSV) Una representación textual común para tablas
en el cual los valores en cada fila están separados por comas.

[delimiter]{#delimiter}
:   Un caracter or caracteres usados para separar valores individuales,
tales como las comas entre columnas en un archivo [CSV](#comma-separated-values).

[documentation]{#documentation}
:   Texto en lenguaje humano escrito para explicar lo que hace el software
cómo funciona, o cómo usarlo.

[floating-point number]{#floating-point-number}
:   Un número que contiene una parte fraccionaria y un exponente.
Ver también: [integer](#integer).

[for loop]{#for-loop}
:   Un ciclo que se ejecuta una vez para cada valor en algún tipo de conjunto, lista o rango.
Ver también: [while loop](#while-loop).

[index]{#index}
:   Un subíndice que especifica la ubicación de un único valor en una colección,
como un solo píxel en una imagen.

[integer]{#integer}
:   Un número entero, como -12343.
Ver también: [floating-point number](#floating-point-number).

[library]{#library}
:   En R, es el directorio(s) donde los [paquetes](#package) son almacenados.

[package]{#package}
:   Una colección de funciones R, datos y código compilado en un formato bien definido. Los paquetes se almacenan en una [biblioteca](#library) y se cargan usando la función de library().

[parameter]{#parameter}
:   Nombre de variable en la declaración de la función que se usa para guardar un valor cuando la función es llamada.
El término a menudo se usa indistintamente (y de manera inconsistente) con [argumento](#argumento).

[return statement]{#return-statement}
:   Una declaración que hace que una función deje de ejecutarse y devuelva un valor en donde fue llamada.

[sequence]{#sequence}
:   Una colección de información que se presenta en un orden específico.

[shape]{#shape}
:   Las dimensiones de una matriz, representadas como un vector.
Por ejemplo, una forma de matriz de 5 × 3 es `(5,3)`.

[string]{#string}
:   Abreviatura de "cadena de caracteres",
una [secuencia](#sequence) de cero o más caracteres.

[syntax error]{#syntax-error}
:  Un error de programación que ocurre cuando las instrucciones están en un orden o contienen caracteres no esperados por el lenguaje de programación.

[type]{#type}
:   La clasificación de algo en un programa (por ejemplo, el contenido de una variable)
como un tipo de número (por ejemplo [floating-point](#float), [integer](#integer)), [string](#string),
o algo más. En R el comando typeof() se usa para consultar el tipo de una variable.

[while loop]{#while-loop}
:   Un bucle que se ejecuta siempre que una condición dada sea verdadera.
Ver también: [for loop](#for-loop).


