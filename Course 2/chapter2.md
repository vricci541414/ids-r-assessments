---
title: 'Cuantiles, Percentiles y Diagramas de caja'
description: 'Gráficas de cuantil-cuantil, Percentiles, Diagramas de caja, Distribución de alturas femeninas'
---

## Ejercicio 1. Longitud vectorial 

```yaml
type: NormalExercise
key: 56141be397
lang: r
xp: 100
skills:
  - 1
```

Al analizar datos es importante saber la cantidad de medidas que tiene cada categoría.

`@instructions`
- Definir una variable `male` que tiene las alturas masculinas.
- Definir una variable `female` que tiene las alturas femeninas.
- Reportar la longitud de cada variable.

`@hint`
Utilic la función `length` después de definir dos vectores llamados `male`  (masculino) y `female` (femenino) de alturas subdivididas. Utilice la función `length` dos veces, una vez para cada variable.

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
male <- heights$height[heights$sex=="Male"]
female <- heights$height[heights$sex=="Female"]
```

`@solution`
```{r}
library(dslabs)
data(heights)
male <- heights$height[heights$sex=="Male"]
female <- heights$height[heights$sex=="Female"]

length(male)
length(female)
```

`@sct`
```{r}
test_error()
#test_output("female", incorrect_msg = "¿Está subdividiendo correctamente?")
#test_output("male", incorrect_msg = "¿Está subdividiendo correctamente?")
test_function("length",index=1, incorrect_msg = "Debería usar 'length' dos veces para este ejercicio.")
test_function("length",index=2, incorrect_msg = "Debería usar 'length' dos veces para este ejercicio.")
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 2. Percentiles

```yaml
type: NormalExercise
key: b66abf907d
lang: r
xp: 100
skills:
  - 1
```

Supongamos que no podemos hacer un gráfico y queremos comparar las distribuciones una al lado de la otra. Si el número de puntos de datos es grande, enumerar todos los números no es práctico. Un enfoque más práctico es observar los percentiles. Podemos obtener percentiles usando la función 'quantile' así


```{r}
library(dslabs)
data(heights)
quantile(heights$height, seq(.01, 0.99, 0.01))
```

`@instructions`
- Cree dos vectores de cinco filas que muestren los percentiles 10, 30, 50, 70 y 90 para las alturas de cada sexo y llame estos vectores `female_percentiles` y `male_percentiles`.
- Luego cree un marco de datos llamado `df` con estos dos vectores como columnas. Los nombres de las columnas deben ser "female" y "male" y deben aparecer en ese orden. Como ejemplo, considere que si desea que un marco de datos tenga nombres de columna `names` y `grades`, en ese orden, se hace así:


```{r}
df <- data.frame(names = c("Jose", "Mary"), grades = c("B", "A"))
```
- Eche un vistazo al marco de datos `df`. Esto proporcionará información sobre cómo difieren las alturas masculinas y femeninas.

`@hint`
Necesitará aplicar 'quantile' a las alturas de 'male' y 'female' y especificar los percentiles.
Luego, debe llamar a `data.frame`. ¡Asegúrese de tener las columnas en el orden especificado! Aquí hay un ejemplo con secuencias de números:


```{r}
male <- 50:80
female <- 45:85
female_percentiles <- quantile(female, seq(0.1, 0.9, 0.2))
male_percentiles <- quantile(male, seq(0.1, 0.9, 0.2))
df <- data.frame(female = female_percentiles, male = male_percentiles)
df
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
male <- heights$height[heights$sex=="Male"]
female <- heights$height[heights$sex=="Female"]
```

`@solution`
```{r}
library(dslabs)
data(heights)
male <- heights$height[heights$sex=="Male"]
female <- heights$height[heights$sex=="Female"]

female_percentiles <- quantile(female, seq(0.1, 0.9, 0.2))
male_percentiles <- quantile(male, seq(0.1, 0.9, 0.2))

df <- data.frame(female = female_percentiles, male = male_percentiles)
df
```

`@sct`
```{r}
test_error()
test_object("female_percentiles", incorrect_msg = "Asegúrese de usar la función `quantile`.")
test_object("male_percentiles", incorrect_msg = "Asegúrese de usar la función `quantile`.")
test_object("df",incorrect_msg = "Debería de usar `data.frame` para definir `df` en este ejercicio. Asegúrese de que las columnas estén el orden `female`, `male`.")
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 3. Interpretándo Diagramas de Caja - 1

```yaml
type: MultipleChoiceExercise
key: ca5e3e9a17
lang: r
xp: 50
skills:
  - 1
```

Estudie los diagramas de caja que resumen las distribuciones de tamaños de población por país.

¿Qué continente tiene el país con el mayor tamaño de población?

`@possible_answers`
- África
- Américas
- Asia
- Europa
- Oceanía

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(gapminder)
gapminder %>% 
    filter(year == 2010) %>% 
    group_by(continent) %>% 
    ggplot(aes(x=continent, y=population/10^6)) + 
    geom_boxplot() + 
    scale_y_continuous(trans = "log10", breaks = c(1,10,100,1000)) + 
    ylab("Population in millions")

```

`@sct`
```{r}
msg3 = "¡Correcto! ¡Buen trabajo!"
msg1 = msg2 = msg4 = msg5 = "Incorrecto. Intente otra vez"
test_mc(3, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Ejercicio 4. Interpretándo Diagramas de Caja - 2


```yaml
type: MultipleChoiceExercise
key: abdc87afbd
lang: r
xp: 50
skills:
  - 1
```

Estudie los diagramas de caja que resumen las distribuciones de tamaños de población por país.

¿Qué continente tiene la población mediana más grande?

`@possible_answers`
- África
- Américas
- Asia
- Europa
- Oceanía

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(gapminder)
gapminder %>% 
    filter(year == 2010) %>% 
    group_by(continent) %>% 
    ggplot(aes(x=continent, y=population/10^6)) + 
    geom_boxplot() + 
    scale_y_continuous(trans = "log10", breaks = c(1,10,100,1000)) + 
    ylab("Population in millions")
```

`@sct`
```{r}
msg1 = "¡Correcto!  ¡Buen trabajo!"
msg2 = msg3 = msg4 = msg5 = "Incorrecto. Mire muy de cerca dónde están las medianas."
test_mc(1, c(msg1, msg2, msg3, msg4, msg5))
```

---

## Ejercicio 5. Interpretándo Diagramas de Caja - 3

```yaml
type: MultipleChoiceExercise
key: 2481169bf1
lang: r
xp: 50
skills:
  - 1
```

Una vez más, mire los diagramas de caja que resumen las distribuciones de los tamaños de las poblaciones por país. Al millón más cercano, ¿cuál es el tamaño de la población 'median' (mediana) de África?

`@possible_answers`
- 100 millones
- 25 millones
- 10 millones
- 5 millones
- 1 millón

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(gapminder)
gapminder %>% 
    filter(year == 2010) %>% 
    group_by(continent) %>% 
    ggplot(aes(x=continent, y=population/10^6)) + 
    geom_boxplot() + 
    scale_y_continuous(trans = "log10", breaks = c(1,10,100,1000)) + 
    ylab("Population in millions")
```

`@sct`
```{r}
msg3 = "¡Correcto!  ¡Buen trabajo!"
msg1 = msg2 = msg4 = msg5 = "Incorrecto. Mire muy de cerca dónde están las medianas."
test_mc(3, c(msg1, msg2, msg3, msg4, msg5))
```

---

## Ejercicio 6. Cuantiles bajos

```yaml
type: MultipleChoiceExercise
key: 66e045675a
lang: r
xp: 50
skills:
  - 1
```

Examine los siguientes diagramas de caja e informe aproximadamente qué proporción de países en Europa tienen una población abajo de 14 millones:

`@possible_answers`
- 0.75
- 0.50
- 0.25
- 0.01

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(gapminder)
gapminder %>% 
    filter(year == 2010) %>% 
    group_by(continent) %>% 
    ggplot(aes(x=continent, y=population/10^6)) + 
    geom_boxplot() + 
    scale_y_continuous(trans = "log10", breaks = c(1,10,100,1000)) + 
    ylab("Population in millions")
```

`@sct`
```{r}
msg2 = "¡Correcto!  ¡Buen trabajo!"
msg1 = msg3 = msg4 = msg5 = "Incorrecto. Intente otra."
test_mc(1, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Ejercicio 7. Rango Intercuantílico (IQR en inglés)

```yaml
type: MultipleChoiceExercise
key: c1b21fa2ad
lang: r
xp: 50
skills:
  - 1
```

Usando el diagrama de caja como guía, ¿qué continente que se muestra a continuación tiene el rango intercuartílico más grande para log(population)?

`@possible_answers`
- África
- Américas
- Asia
- Europa
- Oceanía

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(gapminder)
gapminder %>% 
    filter(year == 2010) %>% 
    group_by(continent) %>% 
    ggplot(aes(x=continent, y=population/10^6)) + 
    geom_boxplot() + 
    scale_y_continuous(trans = "log10", breaks = c(1,10,100,1000)) + 
    ylab("Population in millions")
```

`@sct`
```{r}
msg2 = "¡Correcto!  ¡Buen trabajo!"
msg1 = msg3 = msg4 = msg5 = "Incorrecto. Intente otra vez"
test_mc(2, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Fin de la evaluación: Cuantiles, Percentiles y Diagramas de caja

```yaml
type: PureMultipleChoiceExercise
key: b90a40700b
xp: 50
skills:
  - 1
```

Este es el final de la asignación de programación para esta sección. Por favor NO haga clic para acceder a evaluaciones adicionales desde esta página. ADVERTENCIA: si continúa con las evaluaciones haciendo clic en la flecha para pasar al siguiente ejercicio o presionando Ctrl-K, es posible que sus evaluaciones NO se califiquen.

Puede cerrar esta ventana y volver a <a href='https://www.edx.org/course/data-science-visualization-harvardx-ph125-2x'>Ciencia de datos: Visualización</a>.

`@hint`
- ¡No es necesario dar pistas!

`@possible_answers`
- [Asombroso]
- No

`@feedback`
- "¡Excelente! Ahora navegue de regreso al curso en edX."
- "Ahora navegue de regreso al curso en edX."
