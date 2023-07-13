---
title: Distribuciones normales
description: En este capítulo repasamos la distribución normal     .
---

## Ejercicio 1. Proporciones

```yaml
type: NormalExercise
key: 2615b249e5
lang: r
xp: 100
skills:
  - 1
```

Los histogramas y los diagramas de densidad proporcionan excelentes resúmenes de una distribución. Pero, ¿podemos resumir aún más? Muchas veces vemos que el promedio y la desviación estándar se usan como estadísticas de resumen: ¡un resumen de dos números! Para entender qué son estos resúmenes y por qué se usan tanto, necesitamos entender la distribución normal.

La distribución normal, también conocida como curva de campana y distribución gaussiana, es uno de los conceptos matemáticos más famosos de la historia. Una razón de esto es que las distribuciones aproximadamente normales ocurren en muchas situaciones. Los ejemplos incluyen ganancias de juegos de azar, alturas, pesos, presión arterial, puntajes de pruebas estandarizadas y errores de medición experimental. Muchas veces, se necesita la visualización de datos para confirmar que nuestros datos siguen una distribución normal.

Aquí nos enfocamos en cómo la distribución normal nos ayuda a resumir datos y puede ser útil en la práctica.

Una forma en que la distribución normal es útil es que se puede usar para aproximar la distribución de una lista de números sin tener acceso a la lista completa. Demostraremos esto con el conjunto de datos de alturas.

Cargue el conjunto de datos de altura y cree un vector `x` con solo las alturas masculinas:

```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
```

`@instructions`
- ¿Qué proporción de los datos está entre 69 y 72 pulgadas (más alto que 69 pero más bajo o igual a 72)? Una proporción está entre 0 y 1.
- Usa la función `mean` en su código. Recuerde que puede usar `mean` (promedio) para calcular la proporción de entradas de un vector lógico que son `TRUE` (verdaderos).

`@hint`
- Recuerda que puedes crear un vector lógico con operadores lógicos. Por ejemplo, puede preguntar qué entradas de un vector están entre 2 y 5 de esta manera:

```{r}
x <- 1:10
x > 2 & x<=5
```
- Puede usar `mean` para calcular la proporción de entradas que son `TRUE`.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
```

`@solution`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
mean(x > 69 & x <= 72)
```

`@sct`
```{r}
test_error()
#test_object("x", incorrect_msg = "`x` no está definido correctamente.")
test_function("mean", incorrect_msg = "¿Está utilizando `mean` en el subconjunto correcto?")
test_output_contains("0.3337438", incorrect_msg = "¿Está usando `mean` usando la expresión lógica correcta? Debería ser algo así como `x>a & x<=b`.")
success_msg("¡Buen trabajo! Recuerde el valor aquí, lo mencionaremos en el futuro.")
```

---

## Ejercicio 2. Promedios y Desviaciones Estándar

```yaml
type: NormalExercise
key: 0390d2888e
lang: r
xp: 100
skills:
  - 1
```
Suponga que todo lo que sabe sobre los datos de altura del ejercicio anterior es el promedio y la desviación estándar y que su distribución se aproxima a la distribución normal. Podemos calcular el promedio y la desviación estándar de esta manera:

```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex=="Male"]
avg <- mean(x)
stdev <- sd(x)
```

Suponga que solo tiene `avg` y `stdev` a continuación, pero no tiene acceso a `x`, ¿puede aproximar la proporción de los datos entre 69 y 72 pulgadas?

Dada una distribución normal con una media 'mu' y una desviación estándar 'sigma', puede calcular la proporción de observaciones menores o iguales a un 'valor' determinado con 'pnorm(valor, mu, sigma)'. Observe que este es el CDF para la distribución normal. Aprenderemos mucho más sobre `pnorm` más adelante en la serie de cursos, pero también puede aprender más ahora con `?pnorm`.

`@instructions`
- Usa la aproximación normal para estimar la proporción la proporción de los datos que está entre 69 y 72 pulgadas.
- Tenga en cuenta que no puede usar `x` en su código, solo `avg` y `stdev`. También tenga en cuenta que R tiene una función que puede resultar muy útil aquí: consulte la función `pnorm` (y recuerde que puede obtener ayuda usando `?pnorm`).

`@hint`
Use la función `pnorm` con los argumentos correctos para `mean` y `sd` para predecir las proporciones para calcular la proporción que está por debajo de 72 y restar la proporción que está por debajo de 69.

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex=="Male"]
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex=="Male"]
avg <- mean(x)
stdev <- sd(x)
```

`@solution`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex=="Male"]
avg <- mean(x)
stdev <- sd(x)
pnorm(72, avg, stdev) - pnorm(69, avg, stdev)
```

`@sct`
```{r}
test_error()
test_output_contains("0.3061779", incorrect_msg = "¿Está utilizando `pnorm` en el promedio correcto y sd correcto? Recuerde que puede estimar la proporción por debajo de 72 y restar la proporción por debajo de 69. Use `pnorm` para ambas estimaciones.")
success_msg("¡Buen trabajo! Fíjese en lo similares que son.")
```

---

## Ejercicio 3. Aproximaciones

```yaml
type: NormalExercise
key: 82595c60bc
lang: r
xp: 100
skills:
  - 1
```

Note que la aproximación calculada en la segunda pregunta es muy cercana al cálculo exacto en la primera pregunta. La distribución normal fue una aproximación útil para este caso.

Sin embargo, la aproximación no siempre es útil. Un ejemplo son los valores más extremos, a menudo llamados "colas" de la distribución. Veamos un ejemplo. Podemos calcular la proporción de alturas entre 79 y 81.

```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
mean(x > 79 & x <= 81)
```

`@instructions`
- Usa la aproximación normal para estimar la proporción de alturas entre 79 y 81 pulgadas y guárdela en un objeto llamado `aprox`.
- Reporte cuántas veces mayor es la proporción real en comparación con la aproximación.

`@hint`
- ¡Recuerde calcular el promedio y la desviación estándar!
- Luego calcule la aproximación normal usando `pnorm`.
- Finalmente, calcule la relación entre el valor exacto y la aproximación dividiendo los dos valores.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
exact <- mean(x > 79 & x <= 81)
```

`@solution`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
avg <- mean(x)
stdev <- sd(x)
exact <- mean(x>79 & x<=81)
approx <- pnorm(81, avg, stdev) - pnorm(79, avg, stdev)
exact/approx
```

`@sct`
```{r}
test_error()
test_output_contains("exact/approx", incorrect_msg = "Calcule la proporción de sus dos respuestas de evaluación anteriores")
success_msg("¡Buen trabajo! Observe que en las colas de la distribución, la aproximación no es tan precisa.")
```

---

## Ejercicio 4. Atletas de siete pies de altura y la NBA

```yaml
type: NormalExercise
key: 4004286f5d
lang: r
xp: 100
skills:
  - 1
```

Alguien le pregunta qué porcentaje de jugadores de siete pies hay en la Asociación Nacional de Baloncesto (NBA). ¿Puede proporcionar una estimación? Intentemos usar la aproximación normal para responder esta pregunta.

Dada una distribución normal con una media 'mu' y una desviación estándar 'sigma', puede calcular la proporción de observaciones menores o iguales a un determinado 'valor' con 'pnorm(valor, mu, sigma)'. Observe que este es el CDF para la distribución normal. Aprenderemos mucho más sobre `pnorm` más adelante en la serie de cursos, pero también puede aprender más ahora con `?pnorm`.

Primero, estimaremos la proporción de hombres adultos que miden más de 7 pies.

Suponga que la distribución de hombres adultos en el mundo se distribuye normalmente con un promedio de 69 pulgadas y una desviación estándar de 3 pulgadas.

`@instructions`
- Usando la aproximación normal, estime la proporción de hombres adultos que miden más de 7 pies, denominados _siete pies_. Recuerda que 1 pie equivale a 12 pulgadas.
- Suponga que la distribución de hombres adultos en el mundo se distribuye normalmente con un promedio de 69 pulgadas y una desviación estándar de 3 pulgadas.
- Usa la función `pnorm`. Tenga en cuenta que `pnorm` encuentra la proporción menor o igual a un valor dado, pero se le pide que encuentre la proporción mayor que ese valor.
- Imprima su presupuesto; no lo almacene en un objeto.

`@hint`
Utilice la función `pnorm`. Recuerde que 7 pies son `7*12` pulgadas.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# Utilice pnorm para calcular la proporción sobre 7 pies (7*12 pulgadas)

```

`@solution`
```{r}
# Utilice pnorm para calcular la proporción sobre 7 pies (7*12 pulgadas)
1 - pnorm(7*12, 69, 3)
```

`@sct`
```{r}
test_error()
test_output_contains("2.866516e-07", incorrect_msg = "Asegúrese de que está calculando la cola derecha de la distribución. `1 - su estimación`")
success_msg("¡Gran trabajo!")
```

---

## Ejercicio 5. Estimando el número de atletas de siete pies de altura

```yaml
type: NormalExercise
key: 0b85453043
lang: r
xp: 100
skills:
  - 1
```

Ahora tenemos una aproximación para la proporción, llámela `p`, de hombres que miden 7 pies o más.

Sabemos que hay alrededor de mil millones de hombres entre 18 y 40 años en el mundo, el rango de edad de atletas en la NBA.

¿Podemos usar la distribución normal para estimar cuántos de estos mil millones de hombres miden al menos siete pies de altura?

`@instructions`
- Use su respuesta al ejercicio anterior para estimar la proporción de hombres que miden siete pies o más en el mundo y almacene ese valor como `p`.
- Luego, multiplique este valor por mil millones (10^9) y redondee el número de hombres de 18 a 40 años que miden siete pies de alto o más al entero más cercano con la función `round`. (No almacene este valor en un objeto).

`@hint`
Usa la función `pnorm` como en el ejercicio anterior, pero esta vez almacene el resultado en `p`. Cuando redondee, recuerde que mil millones es 10^9 y luego use la función  `round`.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}

```

`@solution`
```{r}
p <- 1 - pnorm(7*12, 69, 3)
round(p * 10^9)
```

`@sct`
```{r}
test_error()
test_output_contains("287", incorrect_msg = "Asegúrese de redondear al entero más cercano. Pruebe la función `round`.")
success_msg("¡Gran trabajo! Recuerde esta respuesta: la usaremos en el siguiente ejercicio.")
```

---

## Ejercicio 6. ¿Cuántos atletas de siete pies de altura hay en la NBA?

```yaml
type: NormalExercise
key: 9ab25189ea
lang: r
xp: 100
skills:
  - 1
```

Hay alrededor de 10 jugadores de la Asociación Nacional de Baloncesto (NBA) que miden 7 pies de altura o más.

`@instructions`
- Usa su respuesta al ejercicio 4 para estimar la proporción de hombres que miden siete pies o más en el mundo y almacene ese valor como `p`.
- Use su respuesta al ejercicio anterior (ejercicio 5) para redondear el número de hombres de 18 a 40 años que miden siete pies o más al entero más cercano y almacene ese valor como `N`. Tenga en cuenta que R distingue entre mayúsculas y minúsculas, así que no use `n`.
- Luego calcule la proporción de jugadores de siete pies de edad de 18 a 40 años del mundo que están en la NBA. (No almacene este valor en un objeto).

`@hint`
Usa la función `pnorm` como en el ejercicio 4, pero esta vez almacena la salida en `p`. Cuando redondee, recuerde que mil millones es 10^9, y almacene ese objeto en `N`. ¡Use la información dada sobre el número de jugadores de la NBA para calcular la proporción!

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}

```

`@solution`
```{r}
p <- 1 - pnorm(7*12, 69, 3)
N <- round(p * 10^9)
10/N
```

`@sct`
```{r}
test_error()
test_output_contains("10/N", incorrect_msg = "Divida el número de jugadores de la NBA de 7 pies de altura por su respuesta anterior para obtener una proporción")
success_msg("¡Gran trabajo! ¡Es un porcentaje más alto de lo que hubiera imaginado!")
```

---

## Ejercicio 7. La altura de Lebron James

```yaml
type: NormalExercise
key: 817a8de36d
lang: r
xp: 100
skills:
  - 1
```

En el ejercicio anterior estimamos la proporción de siete pies en la NBA usando este código simple:

```{r}
p <- 1 - pnorm(7*12, 69, 3)
N <- round(p * 10^9)
10/N
```

Repita los cálculos realizados en la pregunta anterior para la altura de Lebron James: 6 pies y 8 pulgadas.
Hay alrededor de 150 jugadores, en lugar de 10, que son al menos tan altos en la NBA.

`@instructions`
Indiqué la proporción estimada de personas que están en la NBA de al menos la la misma altura de Lebron.

`@hint`
Asegúrese de modificar el código para `p` para reflejar la altura de Lebron James y para que la proporción final refleje la cantidad de jugadores de la NBA que tienen al menos esa altura en la NBA.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
## Cambié la solución a la respuesta anterior
p <- 1 - pnorm(7*12, 69, 3)
N <- round(p * 10^9)
10/N
```

`@solution`
```{r}
p <- 1 - pnorm(6*12 + 8, 69, 3)
N <- round(p * 10^9)
150/N
```

`@sct`
```{r}
test_error()
test_object("p", incorrect_msg = "Asegúrese de que las alturas estén en pulgadas y represente la altura de Lebron. El promedio y la desviación estándar son iguales ya que es la misma población.")

test_output_contains("150/N", incorrect_msg = "¿Recordó cambiar el número de personas en la NBA que tienen esa altura?")
success_msg("¡Gran trabajo! ¿Es más difícil ingresar a la NBA si uno no mide 7 pies de altura?")
```

---

## Ejercicio 8. Interpretación

```yaml
type: MultipleChoiceExercise
key: d846ce8d42
lang: r
xp: 50
skills:
  - 1
```

Al responder a las preguntas anteriores, descubrimos que no es raro que un jugador de siete pies se convierta en un jugador de la NBA.

¿Cuál sería una crítica justa de nuestros cálculos?

`@possible_answers`
- La práctica y el talento son lo que hace a un gran jugador de baloncesto, no la altura.
- La aproximación normal no es adecuada para alturas.
- Como se vio en el ejercicio 3, la aproximación normal tiende a subestimar los valores extremos. Es posible que haya más jugadores de siete pies de altura de los que predijimos.
- Como se vio en el ejercicio 3, la aproximación normal tiende a sobrestimar los valores extremos. Es posible que haya menos jugadores de siete pies de altura de los que predijimos.

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg3 = "¡Correcto! ¡Buen trabajo!"
msg1 = msg2 = msg4 = "Incorrecto. Intenté otra vez."
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Fin de la Evaluación: Distribución Normal

```yaml
type: PureMultipleChoiceExercise
key: 4307faf5ce
xp: 50
skills:
  - 1
```

Este es el final de la asignación de programación para esta sección. Por favor NO haga clic para acceder a evaluaciones adicionales desde esta página. ADVERTENCIA: si continúa con las evaluaciones haciendo clic en la flecha para pasar al siguiente ejercicio o presionando Ctrl-K, es posible que sus evaluaciones NO se califiquen.

Puede cerrar esta ventana y volver a <a href='https://www.edx.org/course/data-science-visualization-harvardx-ph125-2x'>Ciencia de datos: Visualización</a>.

`@hint`
- ¡No es necesaria ninguna pista!

`@possible_answers`
- [Awesome]
- No

`@feedback`
- ¡Excelente! ¡Ahora vuelva al curso en edX!
- ¡Ahora vuelva al curso en edX!
