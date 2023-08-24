---
titulo: Principios de visualización de datos - Parte 3
descripción: Parte 3 de ejercicios de principios de visualización de datos
---

## Ejercicio 1: Diagrama de mosaico: sarampión y viruela

```yaml
type: NormalExercise
key: 41c91866ca
lang: r
xp: 100
skills:
  - 1
```

El código de ejemplo proporcionado crea un diagrama de mosaico que muestra la tasa de casos de sarampión por población. Vamos a modificar el diagrama de mosaico para ver los casos de viruela.

`@instrucciones`
- Modifique el diagrama de mosaico para mostrar la tasa de casos de viruela en lugar de casos de sarampión.
- Excluir del gráfico los años en los que se notificaron casos en menos de 10 semanas.

`@pista`
- La columna que tiene el número de semanas en las que se reportaron casos se llama `weeks_reporting`.
- Para excluir años con menos de 10 semanas de casos notificados, modifique el "filtro" que utiliza.

`@código_pre_ejercicio`
```{r}
library(dplyr)
library(ggplot2)
library(RColorBrewer)
library(dslabs)
data(us_contagious_diseases)
```

`@código_de_ejemplo`
```{r}
library(dplyr)
library(ggplot2)
library(RColorBrewer)
library(dslabs)
data(us_contagious_diseases)

the_disease = "Measles"
dat <- us_contagious_diseases %>% 
   filter(!state%in%c("Hawaii","Alaska") & disease == the_disease) %>% 
   mutate(rate = count / population * 10000) %>% 
   mutate(state = reorder(state, rate))

dat %>% ggplot(aes(year, state, fill = rate)) + 
  geom_tile(color = "grey50") + 
  scale_x_continuous(expand=c(0,0)) + 
  scale_fill_gradientn(colors = brewer.pal(9, "Reds"), trans = "sqrt") + 
  theme_minimal() + 
  theme(panel.grid = element_blank()) + 
  ggtitle(the_disease) + 
  ylab("") + 
  xlab("")
```

`@solución`
```{r}
library(dplyr)
library(ggplot2)
library(RColorBrewer)
library(dslabs)
data(us_contagious_diseases)

the_disease = "Smallpox"
dat <- us_contagious_diseases %>% 
   filter(!state%in%c("Hawaii","Alaska") & disease == the_disease & weeks_reporting>=10) %>% 
   mutate(rate = count / population * 10000) %>% 
   mutate(state = reorder(state, rate))

dat %>% ggplot(aes(year, state, fill = rate)) + 
  geom_tile(color = "grey50") + 
  scale_x_continuous(expand=c(0,0)) + 
  scale_fill_gradientn(colors = brewer.pal(9, "Reds"), trans = "sqrt") + 
  theme_minimal() + 
  theme(panel.grid = element_blank()) + 
  ggtitle(the_disease) + 
  ylab("") + 
  xlab("")
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal(eval = TRUE)
  check_function(., "aes") %>% {
    check_arg(., "x") %>% check_equal(eval = FALSE)
    check_arg(., "y") %>% check_equal(eval = FALSE)
    check_arg(., "fill") %>% check_equal(eval = FALSE)
  }
  check_function(., "geom_tile", not_called_msg="¿Agregaste la capa `geom_tile()`?")
  check_function(., "scale_x_continuous") %>% check_arg(., "expand") %>% check_equal(eval = TRUE)
  check_function(., "scale_fill_gradientn") %>% check_arg(., "trans") %>% check_equal(eval = TRUE)
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 2. Gráfica de series de tiempo - sarampión y viruela

```yaml
type: NormalExercise
key: e01bd5d3b6
lang: r
xp: 100
skills:
  - 1
```

El código de muestra proporcionado crea un gráfico de series de tiempo que muestra la tasa de casos de sarampión por población por estado. Vamos a modificar nuevamente este diagrama para ver casos de viruela.

`@instrucciones`
- Modifique el código de muestra para la gráfica de serie temporal para trazar datos de viruela en lugar de sarampión.
- Una vez más, restrinja la trama a los años en los que se informaron casos en al menos 10 semanas.

`@pista`
- La columna que tiene el número de semanas en las que se reportaron casos se llama `weeks_reporting`.
- Para excluir años con menos de 10 semanas de casos notificados, modifique el "filtro" que utiliza.

`@código_pre_ejercicio`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)
```

`@código_de_ejemplo`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)

the_disease = "Measles"
dat <- us_contagious_diseases %>%
   filter(!state%in%c("Hawaii","Alaska") & disease == the_disease) %>%
   mutate(rate = count / population * 10000) %>%
   mutate(state = reorder(state, rate))

avg <- us_contagious_diseases %>%
  filter(disease==the_disease) %>% group_by(year) %>%
  summarize(us_rate = sum(count, na.rm=TRUE)/sum(population, na.rm=TRUE)*10000)

dat %>% ggplot() +
  geom_line(aes(year, rate, group = state),  color = "grey50", 
            show.legend = FALSE, alpha = 0.2, size = 1) +
  geom_line(mapping = aes(year, us_rate),  data = avg, size = 1, color = "black") +
  scale_y_continuous(trans = "sqrt", breaks = c(5,25,125,300)) + 
  ggtitle("Cases per 10,000 by state") + 
  xlab("") + 
  ylab("") +
  geom_text(data = data.frame(x=1955, y=50), mapping = aes(x, y, label="US average"), color="black") + 
  geom_vline(xintercept=1963, col = "blue")
```

`@solución`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)
the_disease = "Smallpox"

dat <- us_contagious_diseases %>%
   filter(!state%in%c("Hawaii","Alaska") & disease == the_disease & weeks_reporting >= 10) %>%
   mutate(rate = count / population * 10000) %>%
   mutate(state = reorder(state, rate))

avg <- us_contagious_diseases %>%
  filter(disease==the_disease) %>% group_by(year) %>%
  summarize(us_rate = sum(count, na.rm=TRUE)/sum(population, na.rm=TRUE)*10000)

dat %>% ggplot() +
  geom_line(aes(year, rate, group = state),  color = "grey50", 
            show.legend = FALSE, alpha = 0.2, size = 1) +
  geom_line(mapping = aes(year, us_rate),  data = avg, size = 1, color = "black") +
  scale_y_continuous(trans = "sqrt", breaks = c(5,25,125,300)) + 
  ggtitle("Cases per 10,000 by state") + 
  xlab("") + 
  ylab("") +
  geom_text(data = data.frame(x=1955, y=50), mapping = aes(x, y, label="US average"), color="black") + 
  geom_vline(xintercept=1963, col = "blue")
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal(eval = TRUE)
  check_function(., "aes") %>% {
    check_arg(., "x") %>% check_equal(eval = FALSE)
    check_arg(., "y") %>% check_equal(eval = FALSE)
    check_arg(., "group") %>% check_equal(eval = FALSE)
  }
  check_function(., "geom_line", not_called_msg=""¿Agregaste la capa `geom_tile()`?")
  check_function(., "scale_y_continuous") %>% check_arg(., "trans") %>% check_equal(eval = TRUE)
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 3: Gráfica de series de tiempo - todas las enfermedades en California

```yaml
type: NormalExercise
key: 77c862e397
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a ver las tasas de todas las enfermedades en un estado. Nuevamente, modificará el código de muestra para producir el gráfico deseado.

`@instrucciones`
- Para el estado de California, haga una gráfica de serie de tiempo que muestre las tasas de todas las enfermedades.
- Incluya solo años con 10 o más semanas de informes.
- Utilizar un color diferente para cada enfermedad.
- Incluya su función `aes` dentro de `ggplot` en lugar de dentro de su capa `geom`.

`@pista`
- Puede usar `color` dentro de `aes` para trazar cada enfermedad en un color diferente.
- La columna que tiene el número de semanas en las que se reportaron casos se llama `weeks_reporting`.
- Para excluir años con menos de 10 semanas de casos notificados, modifique el "filtro" que utiliza.

`@código_pre_ejercicio`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)
```

`@código_de_ejemplo`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)

us_contagious_diseases %>% filter(state=="California") %>% 
  group_by(year, disease) %>%
  summarize(rate = sum(count)/sum(population)*10000) %>%
  ggplot(aes(year, rate)) + 
  geom_line()
```

`@solución`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)

us_contagious_diseases %>% filter(state=="California" & weeks_reporting>=10) %>% 
  group_by(year, disease) %>%
  summarize(rate = sum(count)/sum(population)*10000) %>%
  ggplot(aes(year, rate, color = disease)) + 
  geom_line()
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal(eval = TRUE)
  check_function(., "aes") %>% {
    check_arg(., "x") %>% check_equal(eval = FALSE)
    check_arg(., "y") %>% check_equal(eval = FALSE)
    check_arg(., "color") %>% check_equal(eval = FALSE)
  }
  check_function(., "geom_line", not_called_msg="¿Agregaste la capa `geom_line()`?")
}
test_student_typed("color = disease",  
  not_typed_msg = "Recuerda usar la enfermedad para fijar el color.")
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 4: Gráfica de series de tiempo - todas las enfermedades en los Estados Unidos

```yaml
type: NormalExercise
key: 5daf3a49ef
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a hacer una gráfica de serie de tiempo para las tasas de todas las enfermedades en los Estados Unidos. Para este ejercicio, proporcionamos menos código de muestra; puede echar un vistazo al ejercicio anterior para comenzar.

`@instrucciones`
- Calcule la tasa de EE. UU. usando `summarize` para sumar los estados. Llame a la variable `tasa`.
- La tasa de EE. UU. para cada enfermedad será el número total de casos dividido por la población total.
- Recuerde convertir a casos por 10.000.
- Deberá filtrar por `!is.na(population)` para obtener todos los datos.
- Graficar cada enfermedad en un color diferente.

`@pista`
- Puede usar `color` dentro de `aes` para trazar cada enfermedad en un color diferente.
- No necesita filtrar por `weeks_reporting` en este ejercicio.

`@código_pre_ejercicio`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)
```

`@código_de_ejemplo`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)
```

`@solución`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)

us_contagious_diseases %>% filter(!is.na(population)) %>% 
  group_by(year, disease) %>%
  summarize(rate = sum(count)/sum(population)*10000) %>%
  ggplot(aes(year, rate, color = disease)) + 
  geom_line()
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal(eval = TRUE)
  check_function(., "aes") %>% {
    check_arg(., "x") %>% check_equal(eval = FALSE)
    check_arg(., "y") %>% check_equal(eval = FALSE)
    check_arg(., "color") %>% check_equal(eval = FALSE)
  }
  check_function(., "geom_line", not_called_msg="¿Agregaste la capa `geom_line()`?")
}
success_msg("¡Buen trabajo!")
```

---

## Fin de la evaluación: Principios de visualización de datos, Parte 3

```yaml
type: PureMultipleChoiceExercise
key: 2ebfaeb28b
xp: 50
skills:
  - 1
```

Este es el final de las asignaciones de programación.

Puede cerrar esta ventana y volver a <a href='https://www.edx.org/course/data-science-visualization-harvardx-ph125-2x'>Data Science: Visualization</a>.

`@pista`
- ¡No es necesario dar pistas!

`@respuestas_posibles`
- [Impresionante]
- No

`@comentario`
- ¡Excelente! ¡Ahora vuelve al curso en edX!
