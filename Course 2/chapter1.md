---
title: Tipos de Datos
description: En ester curso, lo introducimos a los conceptos básicos de varios tipos de datos. 
free_preview: true
---

## Ejercicio 1. Nombres de variables

```yaml
type: NormalExercise
key: e70afa5dad
lang: r
xp: 100
skills:
  - 1
```

El tipo de datos con los que estamos trabajando influirá la técnica de visualización de datos que utilicemos.
Estaremos trabajando con dos tipos de variables: categóricas y numéricas. Cada una se puede dividir en otros dos grupos: las categóricas pueden ser ordinales o no ordinales, mientras que las variables numéricas pueden ser discretas o continuas.

Revisaremos los tipos de datos utilizando algunos de los ejemplos en el paquete `dslabs`. Por ejemplo, el conjunto de datos `heights`.

```{r}
library(dslabs)
data(heights)
```

`@instructions`
Comencemos practicando cómo extraer los nombres de las variables de un conjunto de datos usando la función `names`.
¿Cuáles son los dos nombres de las variables en el conjunto de datos `heights`?

`@hint`
Utilice la función `names`. Hicimos esto en el primer curso para el conjunto de datos `murders`:
```{r}
library(murders)
names(murders)
```

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
```

`@solution`
```{r}
library(dslabs)
data(heights)
names(heights)
```

`@sct`
```{r}
test_error()
test_output_contains("names(heights)", incorrect_msg = "¿Esta llamando la función en el conjunto de datos correcto?")
test_function("names", incorrect_msg = "Debería usar una función específica para obtener los nombres del conjunto de datos de 'heights'")
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 2. Tipo de variable.

```yaml
type: MultipleChoiceExercise
key: e6b1d336ad
lang: r
xp: 50
skills:
  - 1
```

Vimos que `sex` es la primera variable. Sabemos qué valores están representados por esta variable y podemos confirmarlo mirando los primeros enteros:
```{r}
library(dslabs)
data(heights)
head(heights)
```
¿Qué tipo de datos es la variable `sex`?

`@possible_answers`
- Continuo
- Categórica
- Ordinal
- Ninguna de las anteriores

`@hint`


`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
head(heights)
```

`@sct`
```{r}
msg1 = "Incorrecto. ¿Está mirando la variable correcta?
msg2 = "¡Correcto! Buen trabajo"
msg3 = "Incorrecto. ¡Intente otra vez!"
msg4 = "Incorrecto. ¿Es uno de los anteriores?"
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 3. Valores numéricos.

```yaml
type: NormalExercise
key: 7ea8b2ef03
lang: r
xp: 100
skills:
  - 1
```

Tenga en cuenta que los datos numéricos discretos pueden considerarse ordinales. Aunque esto es técnicamente cierto, por lo general reservamos el término de datos ordinales para las variables que pertenecen a un pequeño número de grupos diferentes, cuyo cada grupo tiene muchos miembros.

La variable `height` podría ser ordinal si, por ejemplo, reportamos una pequeña cantidad de valores como bajo, mediano y alto. Exploremos cuántos valores únicos utiliza la variable 'height. Para esto podemos usar la función unique:

```{r}
x <- c(3, 3, 3, 3, 4, 4, 2)
unique(x)
```

`@instructions`
Utilice las funciones `unique` y `length` para determinar cuántas alturas únicas se reportaron.

`@hint`
Aquí hay un ejemplo:
```{r}
x <- c(3, 3, 3, 3, 4, 4, 2)
length(unique(x))
```

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height
```

`@solution`
```{r}
library(dslabs)
data(heights)
x <- heights$height
length(unique(x))
```

`@sct`
```{r}
test_error()
test_output_contains("139", incorrect_msg = "¿Está llamando a la función en el conjunto de datos correcto?")
test_function("unique", incorrect_msg = "Debería usar unique para este ejercicio.")
test_function("length", incorrect_msg = "YDebería usar length para este ejercicio.")
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 4. Tablas

```yaml
type: NormalExercise
key: 2047247be5
lang: r
xp: 100
skills:
  - 1
```

Uno de los resultados útiles de la visualización de datos es que podemos aprender sobre la distribución de variables. Para datos categóricos, podemos construir esta distribución simplemente calculando la frecuencia de cada valor único. Esto se puede hacer con la función `table`. Aquí hay un ejemplo:

```{r}
x <- c(3, 3, 3, 3, 4, 4, 2)
table(x)
```

`@instructions`
Utilice la función `tablE` para calcular las frecuencias de cada valor de altura único. Debido a que estamos usando la tabla de frecuencia resultante en un ejercicio posterior, queremos que guarde los resultados en un objeto y lo llame 'tab'.

`@hint`
Aquí hay un ejemplo
```{r}
x <- c(3, 3, 3, 3, 4, 4, 2)
tab <- table(x)
```

En este ejercicio trataremos los valores de altura como categóricos, más específicamente como ordinales, y calcularemos estas frecuencias.

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height

```

`@solution`
```{r}
library(dslabs)
data(heights)
x <- heights$height
tab <- table(x)
```

`@sct`
```{r}
test_error()
test_object("tab", incorrect_msg = "¿Está llamando a la función `table` en el conjunto de datos correcto?")
test_function("table", incorrect_msg = "Debería usar la función `table` para este ejercicio.")
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 5. Variables indicadores

```yaml
type: NormalExercise
key: 89f473fdd1
lang: r
xp: 100
skills:
  - 1
```

Para ver por qué tratar las alturas reportadas como un valor ordinal no es útil en la práctica, observemos cuántos valores se reportaron una sola vez.

`@instructions`
En el ejercicio anterior calculamos la variable `tab` que contiene el número de veces que aparece cada valor único. Para los valores reportados solo una vez, `tab` será 1. Use lógicos y la función `sum` para contar la cantidad de veces que esto sucede.

`@hint`
Aquí hay un ejemplo
```{r}
x <- c(3, 3, 3, 3, 4, 4, 2)
tab <- table(x)
sum(tab==1)
```


Utilice la función `sum` para contar el número de veces que las entradas en `tab` son iguales a 1.

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
tab <- table(heights$height)
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
tab <- table(heights$height)
```

`@solution`
```{r}
library(dslabs)
data(heights)
tab <- table(heights$height)
sum(tab==1)
```

`@sct`
```{r}
test_error()
test_output_contains("sum(tab==1)", incorrect_msg = "¿Está llamando a la función `sum` en la tabla que hizo?")
test_function("sum", incorrect_msg = "Debería usar la función `sum` para este ejercicio.")
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 6. Tipos de datos - alturas

```yaml
type: MultipleChoiceExercise
key: ce3b6a5f17
lang: r
xp: 50
skills:
  - 1
```

Dado que hay un número finito de alturas reportadas y técnicamente la altura puede considerarse ordinal, ¿cuál de las siguientes es verdadera?

`@possible_answers`
- Es más efectivo considerar que las alturas son numéricas dada la cantidad de valores únicos que observamos y el hecho de que si seguimos recopilando datos, se observarán aún más.
- De hecho, es preferible considerar las alturas como ordinales ya que en una computadora solo hay un número finito de posibilidades.
- Esta es en realidad una variable categórica: alto, mediano o bajo.
- Esta es una variable numérica porque se usan números para representarla.

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "¡Correcto! ¡Buen trabajo!"
msg2 = "Incorrecto. Intente otra vez"
msg3 = "Incorrecto. Intente otra vez"
msg4 = "Incorrecto. Intente otra vez"
test_mc(1, c(msg1, msg2, msg3, msg4))
```

---

## Fin de la evaluación: Tipos de datos

```yaml
type: PureMultipleChoiceExercise
key: e3235fbaae
xp: 50
skills:
  - 1
```

Este es el final de la asignación de programación para esta sección. Por favor NO haga clic para acceder a evaluaciones adicionales desde esta página. ADVERTENCIA: si continúa con las evaluaciones haciendo clic en la flecha para pasar al siguiente ejercicio o presionando Ctrl-K, es posible que sus evaluaciones NO serán calificadas.

Puede cerrar esta ventana y volver a <a href='https://www.edx.org/course/data-science-visualization-harvardx-ph125-2x'>
Ciencia de datos: Visualización</a>.

`@hint`
- No pista necesaria

`@possible_answers`
- [Awesome]
- No

`@feedback`
- "¡Genial! ¡Ahora vuelva al curso en edX!"
- ¡Ahora vuelva al curso en edX!"
