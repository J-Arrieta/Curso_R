Preprocesamiento_Datos
================
Jesús A. Arrieta
4 de septiembre 2024

# **Plantilla para el preprocesamiento de los datos**

Esta plantilla está diseñada para tener en cuenta los pasos que se deben
seguir al momento de comenzar a trabajar un conjunto de datos.

1.  Importar **librerías**
2.  Importar ***dataset***
3.  Eliminar datos faltantes: **NaN**
4.  Codificar las variables **Categóricas**
5.  **Escalar** variables (si es necesario)

## **Importanción de datos**

``` r
# Los dos primero pasos se realizan en esta celda.
#file.choose() Permite ubicar la ruta del archivo por una ventana.
ruta <- "/home/j-arrieta12/HD_MEC/DOCTORADO/Machinelearning-az/Sessions_Update/Part 1 - Data Preprocessing/Section 2 -------------------- Part 1 - Data Preprocessing --------------------/R/Data.csv"
dataset <- read.csv(ruta)
dataset$Age <- as.integer(dataset$Age)
```

## **Tratamiento de los valores NaN**

Existen muchas maneras de tratar con los
<span style="color:red">**NaN**</span> o datos faltantes. La primera
opción y más sencilla, es reemplazar el dato faltante por el valor
promedio. Sin embargo, esto no siempre es útil, ya que depende del
conjunto de datos y la naturaleza de los mismos. En A este proceso se le
conoce como <span style="color:red">**imputación de datos**</span> . A
continuación, se muestran dos formas de reemplazar los valores faltantes
por la media de los datos.

``` r
colSums(is.na(dataset))
```

    ##   Country       Age    Salary Purchased 
    ##         0         1         1         0

``` r
dataset$Age = ifelse(is.na(dataset$Age), 
                     ave(dataset$Age, FUN = function(x)mean(x, na.rm=TRUE)),
                     dataset$Age)

dataset$Salary[is.na(dataset$Salary)] <- mean(dataset$Salary[!is.nan(dataset$Salary)], na.rm = TRUE)
```

## **Codificar variables categóricas**

Son aquellos datos que <span style="color:red">**no**</span> son de tipo
<span style="color:red">**numérico**</span>, es decir,
<span style="color:red">**son**</span> datos o variables
<span style="color:red">**cualitativas**</span>. Este tipo de variables
se <span style="color:red">**categorizan**</span> y luego se crean
variables <span style="color:red">**dummy**</span> para poder operar con
ellas. Para esto se utilizará la función **factor**, que es un tipo de
estructura de datos que se emplea para manejar las variables
**categóricas**.

``` r
dataset$Country = factor(dataset$Country,
                         levels = c("France", "Spain","Germany"),
                         labels = c(1,2,3))

dataset$Purchased = factor(dataset$Purchased,
                         levels = c("No", "Yes"),
                         labels = c(0,1))
```
