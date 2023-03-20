---
title: Principios de Visualización de Datos - Parte 2
description: Parte 2 de ejercicios de principios de visualización de datos
---

## Ejercicio 1: personalización de parcelas - mira y aprende
```yaml
type: NormalExercise
key: d7655f4b4a
lang: r
xp: 100
skills:
  - 1
```

Para hacer el gráfico de la derecha en el ejercicio del último conjunto de evaluaciones, tuvimos que reordenar los niveles de las variables de los estados.

`@instrucciones`
- Redefinir el objeto `estado` para que los niveles se reordenen por tasa.
- Imprima el nuevo objeto `estado` y sus niveles (usando `niveles`) para que pueda ver que el vector ahora está reordenado por los niveles.

`@pista`

- Puedes usar `reordenar` para reordenar los niveles del objeto de estado.
- Recuerda que estás reordenando por `tarifa`.
- Inspeccionar los niveles de un objeto con `niveles`.

`@código_pre_ejercicio`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
dat <- us_contagious_diseases %>%
filter(year == 1967 & disease=="Measles" & !is.na(population)) %>% mutate(rate = count / population * 10000 * 52 / weeks_reporting)
state <- dat$state 
rate <- dat$count/(dat$population/10000)*(52/dat$weeks_reporting)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
dat <- us_contagious_diseases %>%
filter(year == 1967 & disease=="Measles" & !is.na(population)) %>% mutate(rate = count / population * 10000 * 52 / weeks_reporting)
state <- dat$state 
rate <- dat$count/(dat$population/10000)*(52/dat$weeks_reporting)
```

`@solution`
```{r}
state <- reorder(state, rate)
print(state)
levels(state)
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(.,"reorder") %>% check_arg("x") %>% check_equal()
  check_function(.,"levels") %>% check_result() %>% check_equal()
}
test_object("state", incorrect_msg = "Did you reorder `state` properly and then print it?")

success_msg("Good job!")
```

---

## Ejercicio 2: Personalización de Parcelas - Redefinición

```yaml
type: NormalExercise
key: c63feefa1a
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a personalizar un poco más este gráfico creando una variable de tasa y reordenando por esa variable en su lugar.

`@instructions`
- Agregue una sola línea de código a la definición de la tabla `dat` que usa `mutate` para reordenar los estados por la variable de tasa.
- El código de muestra proporcionado creará un gráfico de barras utilizando el `dat` recién definido.

`@hint
- El código que necesita agregar es muy similar al utilizado en el ejercicio anterior - puede usar `reordenar` nuevamente.
- Asegúrese de agregar el código al código que define `dat`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(us_contagious_diseases)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(us_contagious_diseases)
dat <- us_contagious_diseases %>% filter(year == 1967 & disease=="Measles" & count>0 & !is.na(population)) %>%
  mutate(rate = count / population * 10000 * 52 / weeks_reporting)
dat %>% ggplot(aes(state, rate)) +
  geom_bar(stat="identity") +
  coord_flip()
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
dat <- us_contagious_diseases %>% filter(year == 1967 & disease=="Measles" & count>0 & !is.na(population)) %>%
 mutate(rate = count / population * 10000 * 52 / weeks_reporting) %>%
 mutate(state = reorder(state, rate))
dat %>% ggplot(aes(state, rate)) +
 geom_bar(stat="identity") +
 coord_flip()
```

`@sct`
```{r}
test_error()
ex() %>% {
check_function(.,"reorder", not_called_msg="Don't forget to reorder the data by rate") 
check_object(.,"dat") %>% check_equal()
}
success_msg("Good job!")
```

---

## Ejercicio 3: Mostrar los Datos y Personalizar Gráficos

```yaml
type: MultipleChoiceExercise
key: 688855b651
lang: r
xp: 50
skills:
  - 1
```

Digamos que estamos interesados ​​en comparar las tasas de homicidios con armas de fuego en todas las regiones de los EE. UU. Vemos esta trama:

```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data("murders")
murders %>% mutate(rate = total/population*100000) %>%
  group_by(region) %>%
  summarize(avg = mean(rate)) %>%
  mutate(region = factor(region)) %>%
  ggplot(aes(region, avg)) +
  geom_bar(stat="identity") +
  ylab("Murder Rate Average")
```

y decide mudarse a un estado en la región occidental. ¿Cuál es el principal problema de esta interpretación?

`@possible_answers`
- Las categorías están ordenadas alfabéticamente.
- El gráfico no muestra errores estándar.
- No muestra todos los datos. No vemos la variabilidad dentro de una región y es posible que los estados más seguros no estén en Occidente.
- El Nordeste tiene el promedio más bajo.

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data("murders")
murders %>% mutate(rate = total/population*100000) %>%
  group_by(region) %>%
  summarize(avg = mean(rate)) %>%
  mutate(region = factor(region)) %>%
  ggplot(aes(region, avg)) +
  geom_bar(stat="identity") +
  ylab("Murder Rate Average")
```

`@sct`
```{r}
msg3 = "Correcto! Buen trabajo!"
msg1 = msg2 = msg4 = "Incorrecto. Intenta de nuevo."
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 4: Hacer un diagrama de caja
```yaml
type: NormalExercise
key: fd7566b82b
lang: r
xp: 100
skills:
  - 1
```

Para investigar más a fondo si mudarse a la región occidental es una buena decisión, hagamos un diagrama de caja de las tasas de homicidios por región, que muestre todos los puntos.

`@instructions`
- Ordene las regiones por su tasa media de asesinatos usando `mutate` y `reorder`.
- Hacer un diagrama de caja de las tasas de homicidios por región.
- Mostrar todos los puntos en el diagrama de caja.

`@hint`
- Para ordenar las regiones por tasa, puede usar `mutar` y `reordenar` para ordenar la columna `región` por `tasa`.
- Usa `geom_boxplot()` para hacer un diagrama de caja.
- Usa `geom_point()` para mostrar los puntos.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data("murders")
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data("murders")
murders %>% mutate(rate = total/population*100000)
```

`@solution`
```{r}
murders %>% mutate(rate = total/population*100000) %>%
  mutate(region=reorder(region, rate, FUN=median)) %>%
  ggplot(aes(region, rate)) +
  geom_boxplot() +
  geom_point()
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(., "reorder", not_called_msg="Did you remember to reorder the regions by murder rate?") 
  check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
  check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
  }
  check_function(., "geom_boxplot", not_called_msg="Did you add the `geom_boxplot()` layer?")
  check_function(., "geom_point", not_called_msg="Did you add the `geom_point()` layer?")
}
success_msg("Good job!")
```

---

## Fin de la evaluación: Principios de visualización de datos, Parte 2

```yaml
type: PureMultipleChoiceExercise
key: 9e62a4982b
xp: 50
skills:
  - 1
```

Este es el final de la asignación de programación para esta sección. NO haga clic para acceder a evaluaciones adicionales desde esta página. ADVERTENCIA: si continúa con las evaluaciones haciendo clic en la flecha para pasar al siguiente ejercicio o presionando Ctrl-K, es posible que sus evaluaciones NO se puntúen.

Puede cerrar esta ventana y volver a <a href='https://www.edx.org/course/data-science-visualization-harvardx-ph125-2x'>Data Science: Visualization</a>.

`@hint`
- ¡No es necesario dar pistas!

`@possible_answers`
- [Impresionante]
- No

`@feedback`
- ¡Excelente! ¡Ahora vuelve al curso en edX!
