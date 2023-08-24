---
título: Principios de Visualización de Datos - Parte 1
descripción : Muestre los datos, facilite las comparaciones: use ejes comunes, considere transformaciones,
  Comparaciones fáciles: las señales visuales comparadas deben ser adyacentes
---

## Ejercicio 1: Personalización de parcelas - Gráficos circulares

```yaml
type: MultipleChoiceExercise
key: 2fdba0e6ab
lang: r
xp: 50
skills:
  - 1
```

Los gráficos circulares son apropiados:

`@respuestas_posibles`
- Cuando queremos mostrar porcentajes.
- Cuando ggplot2 no está disponible.
- Cuando estoy en una panadería.
- Nunca. Las gráficas de barras y las tablas siempre son mejores.

`@pista`


`@pre_código_de_ejercicio`
```{r}

```

`@sct`
```{r}
msg1 = "Incorrecto. ¡Inténtalo de nuevo!"
msg2 = "Incorrecto. ¡Inténtalo de nuevo!"
msg3 = "Incorrecto. ¡Inténtalo de nuevo!"
msg4 = "¡Correcto! Buen trabajo. Los gráficos circulares no son una herramienta de visualización muy eficaz."
test_mc(4, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 2. Personalización de parcelas - ¿Qué está mal?
```yaml
type: MultipleChoiceExercise
key: ca5e3e9a17
lang: r
xp: 50
skills:
  - 1
```

¿Cuál es el problema con esta trama?

`@respuestas_posibles`
- Los valores están mal. La votación final fue de 306 a 232.
- El eje no comienza en 0. A juzgar por la longitud, parece que Trump recibió 3 veces más votos cuando en realidad fue un 30% más.
- Los colores deben ser los mismos.
- Los porcentajes deben mostrarse como un gráfico circular.

`@pista`


`@pre_código_de_ejercicio`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()

data.frame(candidate=c("Clinton","Trump"), electoral_votes = c(232, 306)) %>% 
  ggplot(aes(candidate, electoral_votes)) + 
  geom_bar(stat = "identity", width=0.5, color =1, fill = c("Blue","Red")) + 
  coord_cartesian(ylim=c(200,310)) + ylab("Electoral Votes") + xlab("") + 
  ggtitle("Result of Presidential Election 2016")
```

`@sct`
```{r}
msg2 = "Correcto! Buen trabajo!"
msg1 = msg3 = msg4 = msg5 = "Incorrecto. Intenta de nuevo."
test_mc(2, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Ejercicio 3: Personalización de parcelas - ¿Qué pasa 2?

```yaml
type: MultipleChoiceExercise
key: b3f6829f09
lang: r
xp: 50
skills:
  - 1
```

Echale un vistazo a las siguientes dos parcelas. Muestran la misma información: tasas de sarampión por estado en los Estados Unidos para 1928.

`@respuestas_posibles`
- Ambas parcelas proporcionan la misma información, por lo que son igualmente buenas.
- El gráfico de la izquierda es mejor porque ordena los estados alfabéticamente.
- La gráfica de la derecha es mejor porque ordena los estados por índice de enfermedad para que podamos ver rápidamente los estados con índices más altos y más bajos.
- Ambos diagramas deberían ser gráficos circulares en su lugar.

`@pista`


`@pre_código_de_ejercicio`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(gridExtra)
data(us_contagious_diseases)
p1 <- us_contagious_diseases %>% 
  filter(year == 1928 & disease=="Measles" & count>0 & !is.na(population)) %>% 
  mutate(rate = count / population * 10000 * 52 / weeks_reporting) %>%
  ggplot(aes(state, rate)) +
  geom_bar(stat="identity") +
  coord_flip() +
  xlab("")
p2 <- us_contagious_diseases %>% 
  filter(year == 1928 & disease=="Measles" & count>0 & !is.na(population)) %>% 
  mutate(rate = count / population * 10000*52 / weeks_reporting) %>%
  mutate(state = reorder(state, rate)) %>%
  ggplot(aes(state, rate)) +
  geom_bar(stat="identity") +
  coord_flip() +
  xlab("")
grid.arrange(p1, p2, ncol = 2)
```

`@sct`
```{r}
msg3 = "Correcto! Buen trabajo!"
msg1 = msg2 = msg4 = msg5 = "Incorrecto. ¡Inténtalo de nuevo!"
test_mc(3, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Fin de la Evaluación: Principios de Visualización de Datos, Parte 1

```yaml
type: PureMultipleChoiceExercise
key: 38d67dff84
xp: 50
skills:
  - 1
```
Este es el final de la asignación de programación para esta sección. NO haga clic para acceder a evaluaciones adicionales desde esta página. ADVERTENCIA: si continúa con las evaluaciones haciendo clic en la flecha para pasar al siguiente ejercicio o presionando Ctrl-K, es posible que sus evaluaciones NO se puntúen.

Puede cerrar esta ventana y volver a <a href='https://www.edx.org/course/data-science-visualization-harvardx-ph125-2x'>Data Science: Visualization</a>.

`@pista`
- ¡No es necesario dar pistas!

`@respuestas_posibles`
- [Impresionante]
- No

`@comentario`
- ¡Excelente! ¡Ahora vuelve al curso en edX!
