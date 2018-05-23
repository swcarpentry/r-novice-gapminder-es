---
layout: page
title: "Guía del instructor"
permalink: /guide/
---

## Tiempo

Dedicar unos 30 minutos antes del comienzo de cada taller y otros 15 minutos
al comienzo de cada sesión para resolver dificultades técnicas como WiFi e
instalación cosas (incluso si le pediste a los estudiantes que instalen programas con anticipación, y reservar más tiempo
si no lo hiciste).

## Planificación de la lección

La lección contiene mucho más material del que puede ser enseñado en un día.
Los instructores deberán elegir un subgrupo apropiado de episodios a usar 
para un curso estándar de un día de duración. 

Algunos lineamientos sugeridos del material a utilizar son:

(sugerido por [@liz-is](https://github.com/swcarpentry/r-novice-gapminder/issues/104#issuecomment-276529213))

* 01 Introducción a R y RStudio
* 04 Estructuras de datos
* 05 Explorando data frames (desde la sección "Ejemplo realista")
* 08 Creando gráficas con calidad para publicación con ggplot2
* 10 Funciones
* 13 Manipulación de data frames con dplyr
* 15 Produciendo informes con knitr

(sugerido por [@naupaka](https://github.com/swcarpentry/r-novice-gapminder/issues/104#issuecomment-312547509))
* 01 Introducción a R y RStudio
* 02 Gestión de proyectos con RStudio
* 03 Buscando ayuda
* 04 Estructuras de datos
* 05 Explorando data frames 
* 06 Haciendo subconjuntos de datos
* 09 Vectorization
* 08 Creando gráficas con calidad para publicación con ggplot2 *OR* 
13 Manipulación de data frames con dplyr
* 15 Produciendo informes con knitr

Medio día de curso podría consistir en (sugerido por [@karawoo](https://github.com/swcarpentry/r-novice-gapminder/issues/104#issuecomment-277599864)):

* 01 Introducción a R y RStudio
* 04 Estructuras de datos (únicamente creando vectores con `c()`)
* 05 Explorando data frames (desde la sección "Ejemplo realista")
* 06 Haciendo subconjuntos de datos (excluyendo subconjuntos de factores, matrices y listas)
* 08 Creando gráficas con calidad para publicación con ggplot2

## Configurando git en RStudio

Pueden haber dificultades relacionando git a RStudio dependiendo del 
sistema operativo y de su versión. Para asegurarse que Git está correctamente
instalado y configurado, los alumnos deberán ir a la ventana Opciones de
la aplicación RStudio.

* **Mac OS X:**
  * Ir a RStudio -> Preferencias... -> Git/SVN
  * Chequear si existe un **path** a un archivo en la ventana "Git ejecutable". Si no lo hay, el siguiente desafío será averiguar dónde está ubicado Git. 
  * En la terminal, ingresa `which git` y obtendrás el **path** al archivo ejecutable de git. En la ventana "Git ejecutable" quizás tengas dificultades encontrando el directorio, ya que OS X oculta muchos de sus archivos del sistema operativo. Con la ventana de selección de archivo abierta, presionar las teclas "Comando-Shift-G" hará que se abra un cuadro de texto donde podrás tipear o pegar el **path** completo a tu archivo ejecutable de Git: e.g. /usr/bin/git o lo que corresponda.
* **Windows:**
  * Ir a Herramientas -> Opciones Globales... -> Git/SVN
  * Si usas el Instalador de Software Carpentry, entonces 'git.exe' debe ser instalado en `C:/Archivos de Programa/Git/bin/git.exe`.

Para evitar que los alumnos tengan que re-ingresar su **password** cada vez que hacen un **push** a GitHub, éste comando (que puede ser corrido desde un **prompt** de **bash**) hará que solo tengan que ingresar su **password** una única vez:

~~~
$ git config --global credential.helper 'cache --timeout=10000000'
~~~
{: .language-bash}

## Obteniendo datos

La forma más simple de obtener los datos usados en esta lección durante un taller es 
hacer que los asistentes ejecuten lo siguiente:

~~~
git remote add data https://github.com/resbaz/r-novice-gapminder-files
git pull data master
~~~
{: .language-bash}

Si Git no está siendo enseñado como parte del taller, entonces los datos crudos pueden ser descargados desde
[gapminder-FiveYearData][gapminder-data] y
[gapminder-FiveYearData-Wide][gapminder-data-wide].

Los asistentes pueden usar el diálogo `Archivo - Guardar como...` de su navegador para guardar el archivo.

## En general

Asegurarse de enfatizar las buenas prácticas: escribir el código en **scripts** y hacer 
que esté bajo control de versiones. Alentar a los estudiantes a crear archivos de **scripts**
para resolver los desafíos. 

Si estás trabajando en un ambiente remoto (en "la nube"), puedes pedirles que suban los datos de **gapminder**
luego de la segunda lección. 

Asegurate de enfatizar que, a fin de cuentas, las matrices son vectores y que las **data frames**
son listas: esto explicará mucho del comportamiento esotérico encontrado 
en las operaciones básicas.

El reciclado de vectores y funciones probablemente se explican mejor usando 
diagramas en una pizarra.

Es recomendado mirar y hacer los ejemplos de una página de ayuda de R: los 
archivos de ayuda pueden ser intimidantes al principio, pero saber cómo leerlos es 
tremendamente útil.

Mostrar las **CRAN task views**, verlas con uno de los temas.

Hay mucho contenido: muévete rápidamente por las primeras lecciones. Éstas son extensas
mayormente con el propósito de aprender por ósmosis: de forma que su recuerdo 
se dispare cuando se encuentren luego con un problema o comportamiento esotérico.

Lecciones clave en las cuales dedicar tiempo:

* Haciendo subconjuntos de datos - conceptualmente difíciles para novatos
* Funciones - los estudiantes tienen problemas especialmente con ellas
* Estructuras de datos - vale la pena ser completo, pero puedes avanzar por la lección rápidamente.

No se preocupes por no equivocarte o conocer el material de pies a cabeza. Usa
los errores como momentos de aprendizaje: la habilidad más importante que puedes 
enseñar es cómo eliminar errores (**debug**) y recuperarse de errores inesperados.

[gapminder-data]: https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder-FiveYearData.csv
[gapminder-data-wide]: https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder_wide.csv
