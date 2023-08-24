---
title: Distribuciones
description: Una descripción general sobre las distribuciones y sus características.
---

## Ejercicio 1. Distribuciones - 1

```yaml
type: MultipleChoiceExercise
key: 54f59fc608
lang: r
xp: 50
skills:
  - 1
```

Es posible que haya notado que los datos numéricos a menudo se resumen con el valor promedio. Por ejemplo, la calidad de una escuela secundaria a veces se resume con un número: el puntaje promedio en una prueba estandarizada. Ocasionalmente, se informa un segundo número: la desviación estándar. Entonces, por ejemplo, podría leer un informe que indica que las puntuaciones fueron 680 más o menos 50 (la desviación estándar). El informe ha resumido un vector completo de puntajes con solo dos números. ¿Es esto apropiado? ¿Hay alguna información importante que nos falta al mirar solo este resumen en lugar de la lista completa? Vamos a aprender cuándo estos 2 números son suficientes y cuándo necesitamos resúmenes y diagramas más elaborados para describir los datos.


Our first data visualization building block is learning to summarize lists of factors or numeric vectors. The most basic statistical summary of a list of objects or numbers is its distribution. Once a vector has been summarized as distribution, there are several data visualization techniques to effectively relay this information. In later assessments we will practice to write code for data visualization. Here we start with some multiple choice questions to test your understanding of distributions and related basic plots.

Nuestro primer bloque de construcción de visualización de datos es aprender a resumir listas de factores o vectores numéricos. El resumen estadístico más básico de una lista de objetos o números es su distribución. Una vez que un vector se ha resumido como distribución, existen varias técnicas de visualización de datos para transmitir esta información de manera efectiva. En evaluaciones más adelante, practicaremos para escribir código para la visualización de datos. Aquí comenzamos con algunas preguntas de opción múltiple para evaluar su comprensión de las distribuciones y las gráficas básicas relacionadas a las distribuciones.

En el conjunto de datos de 'murders', region (la región) es una variable categórica y a la derecha puede ver su distribución. Al 5% más cercano, ¿qué proporción de los estados se encuentran en la región Centro Norte?
---

## Ejercicio 1. Distribuciones - 1

```yaml
type: MultipleChoiceExercise
key: 54f59fc608
lang: r
xp: 50
skills:
  - 1
```

Es posible que haya notado que los datos numéricos a menudo se resumen con el valor promedio. Por ejemplo, la calidad de una escuela secundaria a veces se resume con un número: el puntaje promedio en una prueba estandarizada. Ocasionalmente, se informa un segundo número: la desviación estándar. Entonces, por ejemplo, podría leer un informe que indica que las puntuaciones fueron 680 más o menos 50 (la desviación estándar). El informe ha resumido un vector completo de puntajes con solo dos números. ¿Es esto apropiado? ¿Hay alguna información importante que nos falta al mirar solo este resumen en lugar de la lista completa? Vamos a aprender cuándo estos 2 números son suficientes y cuándo necesitamos resúmenes y diagramas más elaborados para describir los datos.

Nuestro primer bloque de construcción de visualización de datos es aprender a resumir listas de factores o vectores numéricos. El resumen estadístico más básico de una lista de objetos o números es su distribución. Una vez que un vector se ha resumido como distribución, existen varias técnicas de visualización de datos para transmitir esta información de manera efectiva. En evaluaciones más adelantes en este curso, practicaremos cómo escribir código para la visualización de datos. Aquí comenzamos con algunas preguntas de opción múltiple para evaluar su comprensión de las distribuciones y las gráficas básicas relacionadas a las distribuciones.

En el conjunto de datos de asesinatos llamado murders, region (la región) es una variable categórica y a la derecha puede ver su distribución. A el 5% más cercano, ¿qué proporción de los estados se encuentran en la región Centro Norte?

`@possible_answers`
- 75% 
- 50%
- 25%
- 5%

`@hint`


`@pre_exercise_code`
```{r, echo=FALSE}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(murders)
murders %>% group_by(region) %>%
  summarize(n = n()) %>%
  mutate(Proportion = n/sum(n), 
         region = reorder(region, Proportion)) %>%
  ggplot(aes(x=region, y=Proportion, fill=region)) + 
  geom_bar(stat = "identity", show.legend = FALSE) + 
  xlab("")
```

`@sct`
```{r}
msg3 = "¡Correcto!  ¡Buen trabajo!"
msg1 = msg2 = msg4 = msg5 = "Incorrecto. Intente otra vez"
test_mc(3, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Ejercicio 2. Distribuciones - 2

```yaml
type: MultipleChoiceExercise
key: 8fcdca7449
lang: r
xp: 50
skills:
  - 1
```

En el conjunto de datos de asesinatos, la región es una variable categórica y a la derecha está su distribución.

Cual de los siguientes es verdadero:

`@possible_answers`
- El gráfico es un histograma.
- El gráfico muestra solo cuatro números con un gráfico de barras.
- Las categorías no son números, por lo que no tiene sentido graficar la distribución.
- Los colores, no la altura de las barras, describen la distribución.

`@hint`


`@pre_exercise_code`
```{r, echo=FALSE}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(murders)
murders %>% group_by(region) %>%
  summarize(n = n()) %>%
  mutate(Proportion = n/sum(n), 
         region = reorder(region, Proportion)) %>%
  ggplot(aes(x=region, y=Proportion, fill=region)) + 
  geom_bar(stat = "identity", show.legend = FALSE) + 
  xlab("")
```

`@sct`
```{r}
msg2 = "¡Correcto!  ¡Buen trabajo!"
msg1 = msg3 = msg4 = "Incorrecto. Intente de nuevo"
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 3. Función de Distribución Acumulativa Empírica (eCDF)

```yaml
type: MultipleChoiceExercise
key: f2bb41e8b9
lang: r
xp: 50
skills:
  - 1
```

El gráfico muestra el eCDF para las alturas masculinas:

Según la gráfica, ¿qué porcentaje de hombres miden menos de 75 pulgadas?

`@possible_answers`
- 100%
- 95%
- 80%
- 72 pulgadas

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
heights %>% filter(sex=="Male") %>% ggplot(aes(height)) + 
  stat_ecdf() +
  ylab("F(a)") + xlab("a")
```

`@sct`
```{r}
msg2 = "¡Correcto! ¡Buen trabajo!"
msg1 = msg3 = msg4 = "Incorrecto. Intente otra vez."
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 4. eCDF Alturas masculinas

```yaml
type: MultipleChoiceExercise
key: beac9cc921
lang: r
xp: 50
skills:
  - 1
```

El gráfico muestra el eCDF para las alturas masculinas:

Redondeado a la pulgada más cercana, ¿qué altura `m` tiene la propiedad de que la mitad de los estudiantes varones son más altos que `m` y la mitad son más bajos que 'm'?


`@possible_answers`
- 61 pulgadas
- 64 pulgadas
- 69 pulgadas
- 74 pulgadas

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
heights %>% filter(sex=="Male") %>% ggplot(aes(height)) + 
  stat_ecdf() +
  ylab("F(a)") + xlab("a")
```

`@sct`
```{r}
msg3 = "¡Correcto!  ¡Buen trabajo!"
msg1 = msg2 = msg4 = "Incorrecto. Intente otra vez"
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 5. eCDF de tasa de homicidios

```yaml
type: MultipleChoiceExercise
key: 33398b09b8
lang: r
xp: 50
skills:
  - 1
```

Aquí hay un eCDF de las tasas de homicidios en todos los estados.

Sabiendo que hay 51 estados (contando DC) y basado en este gráfico, ¿cuántos estados tienen tasas de homicidios superiores a 10 por cada 100 000 personas?

`@possible_answers`
- 1
- 5
- 10
- 50

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(murders)
murders %>% mutate(murder_rate = total/population * 10^5) %>%
  ggplot(aes(murder_rate)) + 
  stat_ecdf() +
  ylab("F(a)") + xlab("a")
```

`@sct`
```{r}
msg1 = "¡Correcto!  ¡Buen trabajo!"
msg3 = msg2 = msg4 = "Incorrecto. Intente otra vez"
test_mc(1, c(msg1, msg2, msg3, msg4))
```

---

## ## Ejercicio 6. eCDF de tasa de homicidios - 2

```yaml
type: MultipleChoiceExercise
key: 0a8a8bd476
lang: r
xp: 50
skills:
  - 1
```

Aquí hay un eCDF de las tasas de homicidios en todos los estados:

Según el eCDF mostrado, ¿cuáles de las siguientes afirmaciones son verdaderas?

`@possible_answers`
- Alrededor de la mitad de los estados tienen tasas de homicidio por encima de 7 por 100,000 y la otra mitad por debajo.
- La mayoría de los estados tienen tasas de homicidio por debajo de 2 por 100,000.
- Todos los estados tienen tasas de homicidio superiores a 2 por 100,000.
- Con la excepción de 4 estados, las tasas de homicidios están por debajo del 5 por 100,000.

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(murders)
murders %>% mutate(murder_rate = total/population * 10^5) %>%
  ggplot(aes(murder_rate)) + 
  stat_ecdf() +
  ylab("F(a)") + xlab("a")
```

`@sct`
```{r}
msg4 = "¡Correcto!  ¡Buen trabajo!"
msg3 = msg2 = msg1 = "Incorrecto. Intente otra vez"
test_mc(4, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 7. Histogramas

```yaml
type: MultipleChoiceExercise
key: 576854fa94
lang: r
xp: 50
skills:
  - 1
```

Aquí hay un histograma de estaturas masculinas en nuestro conjunto de datos de "heights":

Basado en esta gráfica, ¿cuántos hombres hay entre 62.5 y 65.5?

`@possible_answers`
- 11
- 29
- 58
- 99

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
heights %>% 
  filter(sex=="Male") %>% 
  ggplot(aes(height)) + 
  geom_histogram(binwidth = 1, color = "black")
```

`@sct`
```{r}
msg3 = "¡Correcto!  ¡Buen trabajo!"
msg4 = msg2 = msg1 = "Incorrecto. Intente otra vez"
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 8. Histogramas - 2

```yaml
type: MultipleChoiceExercise
key: 0e27748ac7
lang: r
xp: 50
skills:
  - 1
```

Aquí hay un histograma de estaturas masculinas en nuestro conjunto de datos de 'heights:

¿Aproximadamente qué **porcentaje** mide menos de 60 pulgadas?

`@possible_answers`
- 1%
- 10%
- 25%
- 50%

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
heights %>% 
  filter(sex=="Male") %>% 
  ggplot(aes(height)) + 
  geom_histogram(binwidth = 1, color = "black")
```

`@sct`
```{r}
msg1 = "¡Correcto!  ¡Buen trabajo!"
msg4 = msg2 = msg3 = "Incorrecto. Intente otra vez"
test_mc(1, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 9. Gráficas de densidad

```yaml
type: MultipleChoiceExercise
key: 0ffb36f695
lang: r
xp: 50
skills:
  - 1
```

Basado en esta gráfica de densidad, ¿qué proporción de estados de EE. UU. tienen poblaciones de más de 10 millones?

`@possible_answers`
- 0.02
- 0.15
- 0.50
- 0.55

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
murders %>% ggplot(aes(x=population/10^6)) + geom_density(fill = "grey") + scale_x_log10() + xlab("Population in millions")
```

`@sct`
```{r}
msg2 = "¡Correcto!  ¡Buen trabajo!"
msg4 = msg1 = msg3 = "Incorrecto. Intente otra vez"
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 10. Gráficas de densidad - 2

```yaml
type: MultipleChoiceExercise
key: adff149195
lang: r
xp: 50
skills:
  - 1
```

Aquí hay tres diagramas de densidad. ¿Es posible que sean del mismo conjunto de datos?
Cuál de las siguientes afirmaciones es verdadera:


`@possible_answers`
- Es imposible que sean del mismo conjunto de datos.
- Son del mismo conjunto de datos, pero diferentes debido a errores de código.
- Son el mismo conjunto de datos, pero el primero y el segundo no suaviza suficiente y el tercero suaviza demasiado.
- Son el mismo conjunto de datos, pero el primero no tiene el eje-x en la escala logarítmica, el segundo no suaviza suficiente y el tercero suaviza demasiado.

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(gridExtra)
library(dslabs)
data(murders)
p1 <- murders %>% ggplot(aes(x=population/10^6)) + geom_density(fill = "grey", bw = 5) + xlab("Population in millions") + ggtitle("1")
p2 <- murders %>% ggplot(aes(x=population/10^6)) + geom_density(fill = "grey", bw = .05) + scale_x_log10() + xlab("Population in millions") + ggtitle("2")
p3 <- murders %>% ggplot(aes(x=population/10^6)) + geom_density(fill = "grey", bw = 1) + scale_x_log10() + xlab("Population in millions") + ggtitle("3")
grid.arrange(p1,p2,p3,ncol=2)
```

`@sct`
```{r}
msg4 = "¡Correcto!  ¡Buen trabajo!"
msg2 = msg1 = msg3 = "Incorrecto. Intente otra vez"
test_mc(4, c(msg1, msg2, msg3, msg4))
```

---

## Fin de la evaluación: Distribuciones

```yaml
type: PureMultipleChoiceExercise
key: 79ce49ce08
lang: r
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