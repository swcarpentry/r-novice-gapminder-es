---
title: Guardando datos
teaching: 10
exercises: 10
source: Rmd
---

::::::::::::::::::::::::::::::::::::::: objectives

- Ser capaz de guardar gráficos y datos desde R.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo guardar gráficos y datos creados en R?

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::  checklist

## Palabras clave

Comando : Traducción

`write.table` : escribir tabla


::::::::::::::::::::::::::::::::::::::::::::::::::

## Guardando gráficos

Ya hemos visto como guardar el gráfico más reciente que creaste con el paquete `ggplot2`
usando el comando `ggsave`. A manera de recordatorio, aquí está el código:


```r
ggsave("My_most_recent_plot.pdf")
```

Puedes guardar un gráfico desde Rstudio usando el botón de 'Export' en la
ventana de 'Plot'. Esto te dará la opción de guardarlo como .pdf, .png, .jpg
u otros formatos de imágenes.

Puede que quieras guardar los gráficos sin visualizarlos previamente
en la ventana de 'Plot'. Quizás quieras hacer un documento pdf con varias
páginas: por ejemplo, cada una con un gráfico distinto. O quizás estás
iterando sobre distintos subconjuntos de un archivo, graficando los datos
de cada subconjunto y quieres guardar cada una de los gráficos. En estos casos obviamente no
puedes detener la iteración en cada paso para dar clic en 'Export' para
cada uno.

En dicho caso conviene usar un método más flexible. La función `pdf` crea un
nuevo pdf del cual puedes controlar el tamaño y la resolución usando los
argumentos específicos de esta función.


```r
pdf("Life_Exp_vs_time.pdf", width=12, height=4)
ggplot(data=gapminder, aes(x=year, y=lifeExp, colour=country)) +
  geom_line() +
  theme(legend.position = "none") 

# ¡Tienes que asegurarte de cerrar el pdf! Para ello usas el comando:

dev.off()
```

Abre este documento y echa un vistazo.

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 1

Vuelve a escribir el comando 'pdf', pero esta vez emplea el término **facet** (sugerencia: usa `facet_grid`) con los
mismos datos. Esto te permitirá visualizar en un gráfico los datos por continente y guardarlos en un pdf.

:::::::::::::::  solution

## Solución al desafío 1


```r
pdf("Life_Exp_vs_time.pdf", width = 12, height = 4)
p <- ggplot(data = gapminder, aes(x = year, y = lifeExp, colour = country)) +
  geom_line() +
  theme(legend.position = "none")
p
p + facet_grid(. ~continent)
dev.off()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Los comandos como `jpeg`y `png` entre otros son usados de manera similar para producir
documentos en los correspondientes formatos.

## Guardando datos

En algún momento puede que también quieras guardar datos desde R.

Para ello podes usar la función `write.table`, que es muy similar a la
función `read.table` que se presentó anteriormente.

Vamos a crear un **script** para limpiar datos. En este análisis, vamos a
enfocarnos solamente en los datos de **gapminder** para Australia:


```r
aust_subset <- gapminder[gapminder$country == "Australia",]

write.table(aust_subset,
  file="cleaned-data/gapminder-aus.csv",
  sep=","
)
```

Ahora regresemos a la terminal para dar un vistazo a los datos y
asegurarnos que se vean bien:


```bash
head cleaned-data/gapminder-aus.csv
```

```{.output}
"country","year","pop","continent","lifeExp","gdpPercap"
"61","Australia",1952,8691212,"Oceania",69.12,10039.59564
"62","Australia",1957,9712569,"Oceania",70.33,10949.64959
"63","Australia",1962,10794968,"Oceania",70.93,12217.22686
"64","Australia",1967,11872264,"Oceania",71.1,14526.12465
"65","Australia",1972,13177000,"Oceania",71.93,16788.62948
"66","Australia",1977,14074100,"Oceania",73.49,18334.19751
"67","Australia",1982,15184200,"Oceania",74.74,19477.00928
"68","Australia",1987,16257249,"Oceania",76.32,21888.88903
"69","Australia",1992,17481977,"Oceania",77.56,23424.76683
```

Mmm, eso no era precisamente lo que queríamos. ¿De dónde vinieron todas
esas comillas?. Los números de línea tampoco tienen sentido.

Veamos el archivo de ayuda para investigar como podemos cambiar este
comportamiento.


```r
?write.table
```

Salvo que configuremos otra cosa, los vectores **character** aparecen de forma predeterminada entre comillas cuando se
guardan en un archivo. También se guardan los nombres de los renglones y las
columnas.

Cambiemos esto:


```r
write.table(
  gapminder[gapminder$country == "Australia",],
  file="cleaned-data/gapminder-aus.csv",
  sep=",", quote=FALSE, row.names=FALSE
)
```

Ahora echemos de nuevo un vistazo a los datos usando nuestras habilidades en
la terminal:


```bash
head cleaned-data/gapminder-aus.csv
```

```{.output}
country,year,pop,continent,lifeExp,gdpPercap
Australia,1952,8691212,Oceania,69.12,10039.59564
Australia,1957,9712569,Oceania,70.33,10949.64959
Australia,1962,10794968,Oceania,70.93,12217.22686
Australia,1967,11872264,Oceania,71.1,14526.12465
Australia,1972,13177000,Oceania,71.93,16788.62948
Australia,1977,14074100,Oceania,73.49,18334.19751
Australia,1982,15184200,Oceania,74.74,19477.00928
Australia,1987,16257249,Oceania,76.32,21888.88903
Australia,1992,17481977,Oceania,77.56,23424.76683
```

¡Ahora se ve mejor!

:::::::::::::::::::::::::::::::::::::::  challenge

## Desafío 2

Escribe un **script** para limpiar estos datos, filtrando los datos de
**gapminder** que fueron colectados desde 1990.

Usa este **script** para guardar este nuevo subconjunto de datos en el
directorio `cleaned-data`.

:::::::::::::::  solution

## Solución al desafío 2


```r
write.table(
  gapminder[gapminder$year > 1990, ],
  file = "cleaned-data/gapminder-after1990.csv",
  sep = ",", quote = FALSE, row.names = FALSE
)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::





:::::::::::::::::::::::::::::::::::::::: keypoints

- Guardar gráficos desde RStudio usando el botón de 'Export'.
- Usar `write.table` para guardar datos tabulares.

::::::::::::::::::::::::::::::::::::::::::::::::::


