---
Título: Introducción a ggplot2
Descripción: >-
  Aprenderá a usar el poderoso paquete de R, ggplot2, para visualización
---

## Ejercicio 1. básicos de ggplot2

```yaml
type: NormalExercise
key: 5f0d9213f4
lang: r
xp: 100
skills:
  - 1
```

Comience cargando las bibliotecas dplyr y ggplot2, así como los datos de `murders`.

```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

Note que puede cargar ambos dplyr y ggplot2, así como otros paquetes al instalar el paquete tidyverse. 

Con ggplot2, los gráficos pueden ser guardados como objetos. Por ejemplo, podemos asociar una base de datos con un objeto así 

```{r}
p <- ggplot(data = murders)
```

Dado que `data` es el primer argumento, no necesitamos deletrearlo. Así que en su lugar, podemos escribirlo de la siguiente manera: 

```{r}
p <- ggplot(murders)
```

o, si cargamos `dplyr`, podemos usar el operador punto: 

```{r}
p <- murders %>% ggplot()
```

Recuerde que el operador punto envía el objeto de la izquierda de `%>%` a ser el primer argumento para la función a la derecha de `%>%`.

Ahora hagamos una introducción a `ggplot`.

`@instructions`
¿Cuál es la clase, `class` del objeto `p`?

`@hint`
Utilice la función `class`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
p <- ggplot(murders)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
p <- ggplot(murders)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
p <- ggplot(murders)
class(p)
```

`@sct`
```{r}
test_error()
test_function_result("class", incorrect_msg = "Asegúrese que `p` es el argumento.")
test_function("class", incorrect_msg = "Use la función `class` y asegúrese que `p` es el argumento.")
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 2. Imprimir

```yaml
type: MultipleChoiceExercise
key: 04b871edcd
lang: r
xp: 50
skills:
  - 1
```

Recuerde que para imprimir un objeto puede usar el comando imprimir `print` o simplemente escribir el objeto. Por ejemplo, en lugar de 

```{r}
x <- 2
print(x)
```

simplemente puede escribir 


```{r}
x <- 2
x
```

Imprima el objeto `p` definido en el ejercicio uno 

```{r}
p <- ggplot(murders)
```

y describa lo que ve.

`@possible_answers`
- No sucede nada
- Un gráfico en blanco 
- Un gráfico de dispersión 
- Un histograma

`@hint`
Las bibliotecas y datos que necesitan ya se encuentran cargados previamente, pero de todas maneras necesitará definir `p`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
```

`@sct`
```{r}
msg2 = "¡Correcto!  ¡Buen trabajo!"
msg1 = msg3 = msg4 = "Incorrecto. Intente de nuevo."
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 3. Pipes (Operadores punto)

```yaml
type: NormalExercise
key: 1c5e6b0d1b
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a revisar el uso de operadores punto viendo cómo pueden ser utilizados con `ggplot`.

`@instructions`
El uso del operador `%>%`, crea un objeto `p` asociado con la base de datos de las alturas, `heights` en lugar de la base de datos de asesinatos, `murders` que había sido usada en ejercicios anteriores. 

`@hint`
Si usáramos el operador para crear un objeto asociado con la base de datos `murders`, usaríamos el código `p <- murders %>% ggplot()`. El código que queremos aquí es muy similar. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)

```

`@sample_code`
```{r}
data(heights)
# defina el objeto ggplot llamado p como en el ejercicio previo pero usando un operador punto 
```

`@solution`
```{r}
data(heights)
p <- heights %>% ggplot()
```

`@sct`
```{r}
test_error()
test_function("ggplot", incorrect_msg = "Asegúrese de estar llamando `ggplot` y estar usando la base de datos de alturas `heights`.")
test_pipe(absent_msg = "Queremos que use el operador `%>%` aquí.")

ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 4. Capas

```yaml
type: MultipleChoiceExercise
key: 772decbbf9
lang: r
xp: 50
skills:
  - 1
```

Ahora vamos a añadir capas y los correspondientes mapeos estéticos. Para los datos de murders, graficamos el número total de asesinatos versus los tamaños de la población en los videos. 

Explore la base de asesinatos `murders` para recordarse de los nombres de las dos variables (total de asesinatos y tamaño de la población) queremos que grafique y seleccione la respuesta correcta. 

`@possible_answers`
- `state` y `abb`
- `total_murders` y `population_size`
- `total` y `population`
- `murders` y `size`

`@hint`
Puede escribir `names(murders)` o lea el archivo de ayuda escribiendo `?murders`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sct`
```{r}
msg3 = "¡Correcto!  ¡Buen trabajo!"
msg1 = msg2 = msg4 = "Incorrecto. Inténtelo de nuevo."
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 5. geom_point 1

```yaml
type: NormalExercise
key: fdcac65e14
lang: r
xp: 100
skills:
  - 1
```

Para crear un gráfico de dispersión, añadimos una capa con la función `geom_point`. Los mapeos estéticos requieren que definamos las variables de los ejes x y y respectivamente. 

```{r, eval=FALSE}
murders %>% ggplot(aes(x = , y = )) +
  geom_point()
```
excepto que tenemos que llenar los espacios para definir las dos variables `x` y `y`.

`@instructions`
Llene el código muestra con los nombres correctos de las variables para graficar el total de asesinatos versus el tamaño de la población. 

`@hint`
En el ejercicio anterior determinamos que los nombres de las variables que queremos aquí son `population` (población) and `total`(total).

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
## Llene los espacios en blanco
murders %>% ggplot(aes(x = , y = )) +
  geom_point()
```

`@solution`
```{r}
murders %>% ggplot(aes(x = population, y = total)) +
  geom_point()
```

`@sct`
```{r}
test_error()
test_function("ggplot", incorrect_msg = "Asegúrese de estar llamando al paquete  `ggplot` y que este utilizando los datos `murders`")
test_pipe(absent_msg = "Queremos que utilice el operador punto `%>%` aquí.")

ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_point", not_called_msg="¿Añadió la capa `geom_point()`?")
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 6. geom_point 2

```yaml
type: NormalExercise
key: 7a9a873231
lang: r
xp: 100
skills:
  - 1
```

Note que si no usamos el argumento names (nombres), podemos obtener el mismo gráfico al asegurarnos que escribamos el nombre de las variables en el orden deseado: 

```{r}
murders %>% ggplot(aes(population, total)) +
  geom_point()
```

`@instructions`
Vuelva a hacer el gráfico pero cambie los ejes, de manera que `total` se encuentre en el eje x y `population` en el eje y.

`@hint`
Recuerde cambiar el orden de `total` y `population` en su código.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}

```

`@solution`
```{r}
murders %>% ggplot(aes(total, population)) +
  geom_point()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_point", not_called_msg="¿Añadió la capa `geom_point()`?")
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 7. texto geom_point 

```yaml
type: MultipleChoiceExercise
key: 5a6cbcf56e
lang: r
xp: 50
skills:
  - 1
```

Si en lugar de puntos queremos añadir texto, podemos usar las geometrías `geom_text()` o `geom_label()`. Sin embargo, note que el siguiente código 

```{r, eval=FALSE}
murders %>% ggplot(aes(population, total)) +
  geom_label()
```

nos dará el siguiente error de mensaje: 
`Error: geom_label requires the following missing aesthetics: label`

¿Por qué es esto? 

`@possible_answers`
- Necesitamos mapear un carácter a cada punto por medio del argumento etiqueta en aes
- Necesitamos especificarle a `geom_label` qué carácter debe usar en el gráfico 
- La geometría `geom_label` no requiere valores en los ejes x y y.
- `geom_label` no es un comando de ggplot2

`@hint`
Lea el archivo de ayuda para `geom_label` cuidadosamente y fíjese en los argumentos requeridos.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sct`
```{r}
msg1 = "¡Correcto!  ¡Buen trabajo!"
msg3 = msg2 = msg4 = msg5 = "Incorrecto. Inténtelo de nuevo."
test_mc(1, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 8. texto geom_point 

```yaml
type: NormalExercise
key: a46d573cd9
lang: r
xp: 100
skills:
  - 1
```

También puede añadir etiquetas a los puntos en un gráfico. 

`@instructions`
Reescriba el código del ejercicio anterior para: 
- añadir un estético `label` a `aes` que sea igual a la abreviación del estado. 
- use `geom_label` en lugar de `geom_point`

`@hint`
- La columna name (nombre) para la abreviación de los nombres en la base de datos `murders` es `abb`. Necesitará mapearla a los puntos usando `aes` de esta manera `aes(population, total, label = abb)`.
- También necesitará cambiar `geom_point` en el código a `geom_label`- vea el ejercicio 7 por un ejemplo. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
## edite la siguiente línea para añadir la etiqueta 
murders %>% ggplot(aes(population, total)) +
  geom_point()
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
murders %>% ggplot(aes(population, total, label = abb)) +
  geom_label()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(.,"label") %>% check_equal(eval=FALSE)
   }
   check_function(., "geom_label", not_called_msg="¿Añadió la capa `geom_label()`?")
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 9. colores geom_point 

```yaml
type: MultipleChoiceExercise
key: d7f3eb3027
lang: r
xp: 50
skills:
  - 1
```

Ahora cambiemos el color de las etiquetas a azul. ¿Cómo podemos hacer esto? 

`@possible_answers`
- Añadiendo una columna llamada `blue` (azul) a `murders` (asesinatos)
- Por medio de mapear los colores por medio de `aes` porque cada etiqueta necesita un color diferente 
- Usando el argumento `color` en `ggplot`
- Usando el argumento `color` en `geom_label` porque queremos que todos los colores sean azules y así no tendríamos que mapear colores 

`@hint`
Note que porque todos los puntos sean azules no sería mapeo. Consecuentemente asignamos el color afuera de `aes`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
```

`@sct`
```{r}
msg4 = "¡Correcto!  ¡Buen trabajo!"
msg3 = msg2 = msg1 = "Incorrecto. Inténtelo de nuevo."
test_mc(4, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 10. colores 2 geom_point 

```yaml
type: NormalExercise
key: 76adde45cd
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a hacer las etiquetas azules. Previamente escribimos este código para añadir las etiquetas a nuestro gráfico: 

```{r, eval=FALSE}
murders %>% ggplot(aes(population, total, label= abb)) +
  geom_label()
```
Ahora vamos a editar este código. 

`@instructions`
- Reescriba el código de arriba para hacer las etiquetas azules añadiendo un argumento a `geom_label`.
- No necesita poner el argumento `color` dentro de `aes`.
- Note que el revisor espera que utilice el argumento `color` en lugar de `col`; estos son equivalentes.

`@hint`
Puede decirle a ggplot que haga un punto azul por medio del argumento `color` en `geom_label`. Puede usar los caracteres `"blue"`. No hay necesidad de usar `aes` dentro de `geom_label`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
murders %>% ggplot(aes(population, total,label= abb)) +
  geom_label()
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
murders %>% ggplot(aes(population, total, label = abb)) +
  geom_label(color = "blue")
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(.,"label") %>% check_equal(eval=FALSE)
   }
   check_function(., "geom_label", not_called_msg="¿Añadió la capa `geom_label()`?") %>% {
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 11. geom_labels por región

```yaml
type: MultipleChoiceExercise
key: ef630d59d6
lang: r
xp: 50
skills:
  - 1
```

Ahora suponga que queremos que el color represente diferentes regiones. De manera que los estados del oeste sean de un color, estados del noreste de otro y así sucesivamente. En este caso, ¿cuál de las siguientes respuestas sería la más apropiada? 

`@possible_answers`
- Añadiendo la columna `color` a `murders` con el color que queremos usar 
- Mapear los colores por medio del argumento de `aes` porque cada etiqueta necesita un color diferente 
- Utilizando el argumento `color` en `ggplot`
- Utilizando el argumento `color` en `geom_label` porque queremos que todos los colores sean azules y así no tengamos que mapear colores 

`@hint`
Ahora estamos asignando un color diferente a cada estado y este color está determinado por una de las variables en la base de datos. Así que necesitamos asignar el color por medio del mapeo `aes`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sct`
```{r}
msg2 = "¡Correcto!  ¡Buen trabajo!"
msg3 = msg4 = msg1 = "Incorrecto. Inténtelo de nuevo."
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 12. geom_label colores

```yaml
type: NormalExercise
key: e9ff3ae827
lang: r
xp: 100
skills:
  - 1
```

Hemos usado este código previamente para hacer un gráfico usando las abreviaciones de los estados como etiquetas: 

```{r}
murders %>% ggplot(aes(population, total, label = abb)) +
  geom_label()
```
Vamos a añadir un color para representar a la región. 

`@instructions`
Reescriba el código de arriba para hacer que la etiqueta de color corresponda a la región del estado. Debido a que este es un mapeo, necesitará hacer esto por medio de la función `aes`. Use la función existente `aes` dentro de la función `ggplot`.

`@hint`
La variable que contiene la información que determinará la región se llama `region`. Podemos asignar que el color sea igual a la región `color = region` por medio de `aes` y ggplot realizará automáticamente lo que queremos. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
## edite este código
murders %>% ggplot(aes(population, total, label = abb)) +
  geom_label()
```

`@solution`
```{r}
murders %>% ggplot(aes(population, total, label = abb, color = region)) +
  geom_label()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(.,"label") %>% check_equal(eval=FALSE)
       check_arg(.,"color") %>% check_equal(eval=FALSE)
   }
   check_function(., "geom_label", not_called_msg="¿Añadió la capa `geom_label()`?")
}
success_msg("¡Gran gráfico!")
```

---

## Ejercicio 13. Escala logarítmica

```yaml
type: NormalExercise
key: 00f2deb781
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a cambiar los ejes a escalas logarítmicas para considerar el hecho que la distribución de la población está sesgada. Vamos a intentar por medio de definir un objeto `p` que contenga el gráfico que hemos hecho hasta ahora: 

```{r}
p <- murders %>% ggplot(aes(population, total, label = abb, color = region)) +
  geom_label() 
```

Para cambiar los ejes x a una escala logarítmica hemos aprendido sobre la función `scale_x_log10()`. Podemos cambiar los ejes por medio de añadir esta capa al objeto `p` para cambiar la escala y representar el gráfico usando el siguiente código: 

```{r}
p + scale_x_log10()
```

`@instructions`
Cambie **ambos** ejes para que estén en escala logarítmica en el mismo gráfico. Asegúrese que no redefina `p` - sólo añada las capas apropiadas. 

`@hint`
Estará añadiendo dos capas ahora. Después de definir `p` el código resultante se verá algo como esto `p + layer_1 + layer_2`. Asegúrese que no redefina `p` - sólo añádale las capas. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
p <- murders %>% ggplot(aes(population, total, label = abb, color = region)) + geom_label()
## añada las capas a p aquí
```

`@solution`
```{r}
p<- murders %>% ggplot(aes(population, total, label = abb, color = region)) + geom_label()
p + scale_x_log10() + scale_y_log10()
```

`@sct`
```{r}
test_error()
test_object("p",incorrect_msg = "Asegúrese de definir `p`")
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(.,"label") %>% check_equal(eval=FALSE)
       check_arg(.,"color") %>% check_equal(eval=FALSE)
   }
   check_function(., "scale_x_log10", not_called_msg="¿Añadió la capa `scale_x_log10()`?")
   check_function(., "scale_y_log10", not_called_msg="Añadió la capa `scale_y_log10()`?")
   check_function(., "geom_label", not_called_msg="Añadió la capa `geom_label()`?")
}
success_msg("¡Gran gráfico!")
```

---

## Ejercicio 14. Títulos

```yaml
type: NormalExercise
key: f013c3250d
lang: r
xp: 100
skills:
  - 1
```

En los ejercicios anteriores hemos creado un gráfico usando el siguiente código: 

```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
p<- murders %>% ggplot(aes(population, total, label = abb, color = region)) +
  geom_label()
p + scale_x_log10() + scale_y_log10()
```

Ahora estamos añadiendo título a este gráfico. Haremos esto por medio de añadir otra capa, pero esta vez con la función `ggtitle`.

`@instructions`
Edite el código de arriba y añada el título "Gun murder data" (datos de asesinatos con pistola) al gráfico.

`@hint`
Use la función de la siguiente manera `p + ggtitle("Escriba el título aquí")`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
p <- murders %>% ggplot(aes(population, total, label = abb, color = region)) +
  geom_label()
# añada una capa para escribir el título en la siguiente línea 
p + scale_x_log10() + 
    scale_y_log10()
```

`@solution`
```{r}
p<- murders %>% ggplot(aes(population, total, label = abb, color = region)) +
  geom_label()
p + scale_x_log10() +
  scale_y_log10() + 
  ggtitle("Gun murder data")
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(.,"label") %>% check_equal(eval=FALSE)
       check_arg(.,"color") %>% check_equal(eval=FALSE)
   }
   check_function(., "scale_x_log10", not_called_msg="¿Añadió la capa `scale_x_log10()`?")
   check_function(., "scale_y_log10", not_called_msg="¿Añadió la capa `scale_y_log10()`?")
   check_function(., "geom_label", not_called_msg="¿Añadió la capa `geom_label()` ?")
   check_function(., "ggtitle", not_called_msg="¿Añadió la capa `ggtitle()`?") %>% check_arg(.,"label") %>% check_equal()
}
success_msg("¡Buen gráfico!")
```

---

## Ejercicio 15. Histogramas

```yaml
type: MultipleChoiceExercise
key: 524fb260ba
lang: r
xp: 50
skills:
  - 1
```

Vamos a redirigir nuestra atención de la base de datos `murders` a explorar la base sobre alturas `heights`.

Utilizamos la función `geom_histogram` para hacer un histograma de las alturas en la base de datos `heights` (alturas). Cuando leemos documentación para esta función vemos que requiere solamente un mapeo, los valores que serán utilizados para el histograma. 

¿Cuál es la variable que contiene las alturas en pulgadas en la base de datos `heights`?

`@possible_answers`
- `sex`
- `heights`
- `height`
- `heights$height`

`@hint`
Explore `names(heights)` para ver los nombres de las variables. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sct`
```{r}
msg3 = "¡Correcto!  ¡Buen trabajo!"
msg1 = msg2 = msg4 = "Incorrecto. Inténtelo de nuevo."
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Ejercicio 16. Un segundo ejemplo

```yaml
type: NormalExercise
key: 94d29619a2
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a hacer un histograma de las alturas, así que cargaremos la base de datos `heights`. El siguiente código ha sido pre-corrido para que carguen la base de datos de las alturas: 

```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@instructions`
- Cree un objeto de ggplot llamado `p` usando el operador (pipe) para asignar los datos de las alturas a un objeto ggplot.
- Asigne `height` a los valores x por medio de la función `aes`.

`@hint`
Justo como antes, utilizaremos el operador `heights %>% ggplot( AES MAPEO AQUÍ)`. Pero el mapeo `aes` tiene solamente una variable ahora. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
# defina p aquí
p <- 
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
p <- heights %>% 
  ggplot(aes(height))
```

`@sct`
```{r}
test_error()
test_pipe(absent_msg = "Queremos que utilice el operador `%>%` aquí.")
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 17. Histogramas 2

```yaml
type: NormalExercise
key: 744cb87b5b
lang: r
xp: 100
skills:
  - 1
```

Ahora estamos listos para añadir una capa que de hecho haga el histograma. 

`@instructions`
Añada una capa al objeto `p` (creado en el ejercicio anterior) utilizando la función `geom_histogram` para hacer el histograma. 

`@hint`
Estamos simplemente añadiendo una capa `+ geom_histogram`. Asegúrese que no está redefiniendo `p`!

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
p <- heights %>% 
  ggplot(aes(height))
## añada una capa a p
```

`@solution`
```{r}
p <- heights %>% 
  ggplot(aes(height))
p + geom_histogram()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_histogram", not_called_msg="¿Añadió la capa `geom_histogram()`?")
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 18. Ancho de las barras en histograma

```yaml
type: NormalExercise
key: 9723af5161
lang: r
xp: 100
skills:
  - 1
```

Note que cuando corremos el código del ejercicio previo, nos aparecerá la siguiente advertencia: 

>> `stat_bin() using bins = 30. Pick better value with binwidth.`

`@instructions`
Use el argumento `binwidth` para cambiar el histograma hecho en el ejercicio previo para usar barras de una pulgada de tamaño. 

`@hint`
El argumento `binwidth` va dentro de la función `geom_histogram`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
p <- heights %>% 
  ggplot(aes(height))
## añada la capa geom_histogram pero con el argumento requerido 
```

`@solution`
```{r}
p <- heights %>% 
  ggplot(aes(height))
p + geom_histogram(binwidth = 1)
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_histogram", not_called_msg="¿Añadió la capa `geom_point()`?") %>%
        check_arg(.,"binwidth") %>% check_equal(eval=FALSE)
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 19. Gráfico de densidad suave

```yaml
type: NormalExercise
key: bd3cb2d728
lang: r
xp: 100
skills:
  - 1
```

Ahora en lugar de un histograma, vamos a hacer un gráfico de densidad suave. En este caso, no haremos un objeto `p`. En su lugar haremos un gráfico utilizando una sola línea de código. En el ejercicio anterior, pudimos haber creado un histograma usando una línea de código como ésta: 

```{r, eval=FALSE}
heights %>% 
  ggplot(aes(height)) +
  geom_histogram()
```

Ahora en lugar de `geom_histogram` utilizaremos `geom_density` para crear un gráfico de densidad suave. 

`@instructions`
Añada la capa apropiada para crear un gráfico de densidad suave de las alturas. 

`@hint`
En lugar de utilizar `geom_histogram`, utilice `geom_density`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
## añada la capa correcta utilizando +
heights %>% 
  ggplot(aes(height))
```

`@solution`
```{r}
heights %>% 
  ggplot(aes(height)) + 
  geom_density()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density", not_called_msg="¿Añadió la capa `geom_density()`?")
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 20. Dos gráficos de densidad suave 

```yaml
type: NormalExercise
key: b2bb7f2d81
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a hacer gráficos de densidad para hombres y mujeres por separado. Para lograrlo, podemos utilizar el argumento `group` que se encuentra dentro del mapeo  `aes`. Debido a que cada punto será asignado a una densidad diferente dependiendo de la variable de la base de datos, necesitamos el mapeo dentro de `aes`.

`@instructions`
Genere dos gráficos de densidad suave para hombres y mujeres por medio de definir `group` por sexos separados. Utilice la función existente `aes` dentro de la función `ggplot`.

`@hint`
Sólo necesitamos cambiar el `aes` por medio de añadir el argumento `group = sex`. Luego añade la capa `geom_density` como antes.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
## añada el argumento del grupo y luego una capa con + 
heights %>% 
  ggplot(aes(height))
```

`@solution`
```{r}
heights %>% 
  ggplot(aes(height, group = sex)) + 
  geom_density()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "group") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density", not_called_msg="¿Añadió la capa `geom_density()`?")
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 21. Dos gráficos de densidad suave 2 

```yaml
type: NormalExercise
key: 5d73d44fd1
lang: r
xp: 100
skills:
  - 1
```

En el ejercicio previo, hicimos dos gráficos de densidad suave, uno para cada sexo usando: 

```{r}
heights %>% 
  ggplot(aes(height, group = sex)) + 
  geom_density()
```
También podemos asignar grupos por medio de los argumentos `color` o `fill`. Por ejemplo, si usted escribe `color = sex` ggplot sabe que usted quiere un color diferente para cada sexo. Así que dos densidades deberán ser dibujadas. Consecuentemente, puede saltarse el mapeo de `group = sex`.
El uso de `color` tiene el beneficio añadido que usa color para distinguir los grupos. 

`@instructions`
Cambie los gráficos de densidad del ejercicio anterios para añadir color. 

`@hint`
En lugar de usar `group = sex`, podemos usar `color = sex` dentro de `aes` para hacer el mapeo. ¡También recuerde añadir la capa de densidad suave! 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
## edite la siguiente línea para usar color en lugar de grupo y luego añadir la capa de densidad  
heights %>% 
  ggplot(aes(height, group = sex))
```

`@solution`
```{r}
heights %>% 
  ggplot(aes(height, color = sex)) + 
  geom_density() 
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density", not_called_msg="¿Añadió la capa de `geom_density()`?")
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 22. Dos gráficos de densidad suave 3 

```yaml
type: NormalExercise
key: af8c96629b
lang: r
xp: 100
skills:
  - 1
```

También podemos asignar grupos usando el argumento `fill`. Cuando usamos la geometría `geom_density`, `color` crea una línea de color para el gráfico de densidad suave mientras que `fill` colorea en el área bajo la curva. 

Podemos ver cómo se ve esto al correr el siguiente código: 

```{r}
heights %>% 
  ggplot(aes(height, fill = sex)) + 
  geom_density() 
```
Sin embargo, aquí la segunda densidad es trazada sobre la otra. Podemos cambiar esto por medio de usar algo llamado _alpha blending_.

`@instructions`
Fije el parámetro del alpha a 0.2 en la función `geom_density` para realizar este cambio. 

`@hint`
Asegúrese de fijar el `alpha = 0.2` en la parte correcta de su código. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}

```

`@solution`
```{r}
heights %>% 
  ggplot(aes(height, fill = sex)) + 
  geom_density(alpha = 0.2)
```

`@sct`
```{r}
test_error()
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "fill") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density", not_called_msg="¿Añadió la capa de `geom_density()`?") %>% check_arg(.,"alpha") %>% check_equal(eval=TRUE)
}
success_msg("¡Buen trabajo")
```

---

## Fin de la Evaluación: Introducción a ggplot2

```yaml
type: PureMultipleChoiceExercise
key: eb426fb216
xp: 50
skills:
  - 1
```

Este es el final de la tarea de programación para esta sección. Por favor NO seleccione o explore tareas adicionales a las que se encuentran en esta página para esta sección. Advertencia: si usted continua con otras evaluaciones por medio de seleccionar la flecha que lleva al siguiente ejercicio o por medio de presionar Ctrl-K es posible que sus evaluaciones NO sean calificadas. 

##### ESTE SIGUIENTE LINK TIENE QUE SER ACTUALIZADO CUANDO SE TENGA LA PÁGINA DEL NUEVO CURSO#######

Puede cerrar esta ventana y regresar a <a href='https://www.edx.org/course/data-science-visualization-harvardx-ph125-2x'>Data Science: Visualization</a>.

##### FIN DEL LINK QUE TIENE QUE SER ACTUALIZADO####### 

`@hint`
- ¡No se necesitan pistas!

`@possible_answers`
- [Maravilloso]
- No

`@feedback`
- ¡Genial! ¡Ahora regrese al curso en edX!
- ¡Ahora regrese al curso en edX!
