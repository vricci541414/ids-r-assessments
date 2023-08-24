---
title: Robust Summaries with Outliers
description: 'dplyr, The Dot Placeholder, Group By, Sorting Data Tables'
---

## Ejercicio 1. Exploración del conjunto de datos de Galton: Promedio y Mediana

```yaml
type: NormalExercise
key: 00ffbfee10
lang: r
xp: 100
skills:
  - 1
```

Para este capítulo, utilizaremos los datos de altura recopilados por Francis Galton para sus estudios genéticos. Aquí solo usamos la altura de los niños en el conjunto de datos:

```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@instructions`
Calcule el promedio y la mediana de estos datos. Noté: no los asigne a una variable.

`@hint`
Puede utilizar las funciones  `mean` y `median`.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@solution`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
mean(x)
median(x)
```

`@sct`
```{r}
test_error()
test_object("x", incorrect_msg = "¿Definió `x` apropiadamente?")
test_function("mean", incorrect_msg = "¿Está calculando la media (`mean`) en el subconjunto correcto?")
test_function("median", incorrect_msg = "¿Está calculando la mediana (`median`) en el subconjunto correcto?")
success_msg("¡Buen trabajo! Fíjese que son similares.")
```

---

## Ejercicio 2. Explorando el conjunto de datos Galton - SD y MAD

```yaml
type: NormalExercise
key: a9b75b2e62
lang: r
xp: 100
skills:
  - 1
```

Ahora, para los mismos datos, calcule la desviación estándar y la desviación absoluta mediana (MAD).

`@instructions`
Calcule la desviación estándar y la desviación absoluta mediana de estos datos.

`@hint`
Usa las funciones `sd` y `mad`.

`@pre_exercise_code`
```{r}


```

`@sample_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@solution`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
sd(x)
mad(x)
```

`@sct`
```{r}
test_error()
test_object("x", incorrect_msg = "¿Definió `x` apropiadamente?")
test_function("sd", incorrect_msg = "¿Está calculando `sd` en el subconjunto correcto?")
test_function("mad", incorrect_msg = "¿Está calculando `mad` en el subconjunto correcto?")
success_msg("¡Buen trabajo! Observe de nuevo que son algo similares.")
```

---

## Ejercicio 3. Impacto del error en el promedio

```yaml
type: NormalExercise
key: c2e9eda61d
lang: r
xp: 100
skills:
  - 1
```

En los ejercicios anteriores vimos que el promedio y la mediana son muy similares y también lo son la desviación estándar y la MAD. Esto es de esperar ya que los datos se aproximan mediante una distribución normal que tiene esta propiedad.

Ahora suponga que Galton cometió un error al ingresar el primer valor, olvidándose de usar el punto decimal. Puede imitar este error escribiendo:

```{r}
library(HistData)
data(Galton)
x <- Galton$child
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
```

Los datos ahora tienen un valor atípico que la aproximación normal no tiene en cuenta. Veamos cómo afecta esto al promedio.

`@instructions`
Informaé cuántas pulgadas crece el promedio después de este error. Específicamente, reporte la diferencia entre el promedio de los datos con el error `x_with_error` y los datos sin el error `x`.

`@hint`
Resté los promedios entre sí.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
```

`@solution`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
mean(x_with_error)- mean(x)
```

`@sct`
```{r}
test_error()
test_object("x", incorrect_msg = "¿Definió `x` apropiadamente?")
test_object("x_with_error", incorrect_msg = "¿Definió `x_with_error` appropriately?")
test_function("mean", incorrect_msg = "¿Está calculando la `mean` en el subconjunto correcto?")
test_function("mean",index=2, incorrect_msg = "¿Está calculando la `mean` en el subconjunto correcto?")
test_output_contains("mean(x_with_error)-mean(x)", incorrect_msg = "¿Está calculando la diferencia entre las dos variables en el orden dado?")
success_msg("¡Buen trabajo! Observe el cambio en el promedio.")
```

---

## Ejercicio 4. Impacto del error en SD

```yaml
type: NormalExercise
key: bae5b2a5ed
lang: r
xp: 100
skills:
  - 1
```

En el ejercicio anterior vimos cómo un simple error en 1 de más de 900 observaciones puede resultar en que el promedio de nuestros datos aumente más de media pulgada, lo cual es una gran diferencia en términos prácticos. Ahora exploremos el efecto que tiene este valor atípico en la desviación estándar.

`@instructions`
Reporte cuantas pulgadas crece la SD (desviaciones estándar) despues de este error. Específicamente, reporte la diferencia entre la SD de los datos con el error `x_with_error` y los datos sin el error `x`.

`@hint`
Resté las desviaciones estándar entre sí.

`@pre_exercise_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@sample_code`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
```

`@solution`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
sd(x_with_error)- sd(x)
```

`@sct`
```{r}
ex() %>% check_predefined_objects("x", incorrect_msg = "¿Definió `x` apropiadamente?")
ex() %>% check_object("x_with_error") %>% check_equal(incorrect_msg = "¿Definió `x_with_error`apropiadamente?")
ex() %>% check_function("sd") %>% check_arg("x") %>% check_equal(incorrect_msg = "¿Está calculando `sd` en el subconjunto correcto?")
ex() %>% check_function("sd",index=2) %>% check_arg("x") %>% check_equal(incorrect_msg = "¿Está calculando `sd` en el subconjunto correcto?")
ex() %>% check_output_expr("sd(x_with_error)-sd(x)", missing_msg = "¿Está calculando la diferencia entre las dos variables en el orden dado?")
success_msg("¡Buen trabajo! Observe el aumento en la desviación estándar.")
```

---

## Ejercicio 5. Impacto del error en la mediana

```yaml
type: NormalExercise
key: 3e0ef1c1aa
lang: r
xp: 100
skills:
  - 1
```

En los ejercicios anteriores vimos cómo un error puede tener un efecto sustancial en el promedio y la desviación estándar.

Ahora vamos a ver como la mediana y la MAD son mucho más resistentes a los valores atípicos. Por eso decimos que son resúmenes _robust_ (_robustos_).

`@instructions`
Reporte cuántas pulgadas crece la mediana después del error. Específicamente, reporte la diferencia entre la mediana de los datos con el error `x_with_error` y los datos sin el error `x`.

`@hint`
Resté las medianas entre sí.

`@pre_exercise_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@sample_code`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
```

`@solution`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
median(x_with_error)- median(x)
```

`@sct`
```{r}
test_error()
test_object("x", incorrect_msg = "¿Definió `x` apropiadamente?")
test_object("x_with_error", incorrect_msg = "Definió `x_with_error` apropiadamente?")
test_function("median", incorrect_msg = "¿Está calculando `median` en el subconjunto correcto?")
test_function("median",index=2, incorrect_msg = "¿Está calculando `median` en el subconjunto correcto?")
test_output_contains("median(x_with_error)-median(x)", incorrect_msg = "¿Está calculando la diferencia en las dos variables en el orden dado?")
success_msg("¡Buen trabajo! Note la robustez de la mediana.")
```

---

## Ejercicio 6. Impacto del error en MAD

```yaml
type: NormalExercise
key: 7d449b012e
lang: r
xp: 100
skills:
  - 1
```

Vimos que la mediana apenas cambia. Ahora veamos cómo se ve afectado el MAD.

`@instructions`
Reporte cuántas pulgadas crece el MAD después del error. Específicamente, reporte la diferencia entre la MAD de los datos con el error `x_with_error` y los datos sin el error `x`.

`@hint`
Resté los MAD entre sí.

`@pre_exercise_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@sample_code`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
```

`@solution`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
mad(x_with_error)- mad(x)
```

`@sct`
```{r}
test_error()
test_object("x", incorrect_msg = "¿Definió `x` apropiadamente?")
test_object("x_with_error", incorrect_msg = "¿Definió `x_with_error` apropiadamente?")
test_function("mad", incorrect_msg = "¿Está calculando `mad` en el subconjunto correcto?")
test_function("mad",index=2, incorrect_msg = "¿Está calculando `mad` en el subconjunto correcto?")
test_output_contains("mad(x_with_error)-mad(x)", incorrect_msg = "¿Está calculando la diferencia en las dos variables en el orden dado?")
success_msg("¡Buen trabajo! Observe que el MAD no cambia.")
```

---

## Ejercicio 7. Utilidad de EDA

```yaml
type: MultipleChoiceExercise
key: 754e716c31
lang: r
xp: 50
skills:
  - 1
```

¿Cómo podría usar el análisis exploratorio de datos para detectar que se cometió un error?

`@possible_answers`
- Dado que es solo un valor entre muchos, no podremos detectarlo.
- Veríamos un cambio evidente en la distribución.
- Una gráfica de caja, un histograma o una gráfica qq (cuantil-cuantil) revelaría un valor atípico claro.
- Un diagrama de dispersión mostraría altos niveles de error de medición.

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg3 = "¡Correcto! ¡Buen trabajo!"
msg1 = msg2 = msg4 = msg5 = "Incorrecto. Intenté otra vez."
test_mc(3, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Ejercicio 8. Uso de EDA para explorar cambios

```yaml
type: NormalExercise
key: 468a1a1b56
lang: r
xp: 100
skills:
  - 1
```

Hemos visto cómo el promedio puede verse afectado por valores atípicos. Pero, ¿qué tan grande puede llegar a ser este efecto? Por supuesto, esto depende del tamaño del valor atípico y del tamaño del conjunto de datos.

Para ver cómo los valores atípicos pueden afectar el promedio de un conjunto de datos, escribamos una función simple que tome el tamaño del valor atípico como entrada y devuelva el promedio.

`@instructions`
Escriba una función llamada `error_avg` que tome un valor `k` y devuelva el promedio del vector `x` después de que la primera entrada cambió a `k`. Muestre los resultados para `k=10000` y `k=-10000`.

`@hint`
Su función debe reemplazar el primer valor en el vector `x` con el único argumento, `k`, y luego calcular `mean`. ¡Y recuerde llamar a la función en `k=10000` y `k=-10000`!

`@pre_exercise_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@sample_code`
```{r}
x <- Galton$child
error_avg <- function(k){


}

```

`@solution`
```{r}
x <- Galton$child

error_avg <- function(k){
  x[1] <- k
  mean(x)
}

error_avg(10000)
error_avg(-10000)
```

`@sct`
```{r}
test_error()
msg = "Vuelva a comprobar cómo estás definiendo la función `error_avg()`."
fun_def <- ex() %>% check_fun_def("error_avg")
fun_def %>% check_arguments()
fun_def %>% check_call(10000) %>% check_result(msg)
fun_def %>% check_body() %>% check_operator('mean')
test_function_result("error_avg",index=1, incorrect_msg = "¿Está calculando `error_avg` con `k=10000`?")
test_function_result("error_avg",index=2, incorrect_msg = "¿Está calculando `error_avg` con `k=10000`?")
test_error()
success_msg("¡Buen trabajo! Observe cómo cambiar un solo valor a un valor atípico grande puede tener un gran efecto en el promedio.")
```

---

## Fin de la Evaluación: Resúmenes Robustos con Valores Atípicos

```yaml
type: PureMultipleChoiceExercise
key: 3dcf2d5987
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