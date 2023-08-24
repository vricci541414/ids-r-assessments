---
title: Resumiendo con dplyr
description: >-
  Practicaremos nuestras abilidades de dplyr trabajando con data de una encuesta recopilada
  por el centro estadounidense nacional para estadísticas de la salud (CNES).
---

## Ejercicio de práctica. Centro Nacional par Estadísticas de la Salud

```yaml
type: MultipleChoiceExercise
key: 2f6ce1c49b
lang: r
xp: 50
skills:
  - 1
```

Para practicar nuestras abilidades de dplyr, trabajaremos con data de una encuesta recopilada
  por el centro estadounidense nacional para estadísticas de la salud (CNES). Este centro ha realizado una serie de encuestas sobre la salud y la alimentación desde los 1960s.

Empezando en el 1999, aproximadamente 5000 personas de todas las edades han sido entrevistadas cada año y entonces completan el componente de la encuesta que trata sobre la examinación de la salud. Parte de este conjunto de datos esta disponible a través del paquete NHANES, el cual se puede cargar de la siguiente manera:

```{r}
library(NHANES)
data(NHANES)
```

A la data NHANES le falta muchos valores. Recuerde que la función principal de resumir en R devolverá `NA` si cualquiera de los elementos del vector de entrada es un `NA`. Aquí tiene un ejemplo:

```{r}
library(dslabs)
data(na_example)
mean(na_example)
sd(na_example)
```

Para ignorar los `NA`s, podemos usar el argumento `na.rm`:

```{r}
mean(na_example, na.rm = TRUE)
sd(na_example, na.rm = TRUE)
```
Pruebe ejecutar este código, y entonces seleccione `Listo!` cuando esté listo para proceder con el análisis.

`@possible_answers`
- Listo!

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Está bien!"
test_mc(1,c(msg1))
```

---

## Ejercicio 1. Presión Arterial 1

```yaml
type: NormalExercise
key: be7d33bb10
lang: r
xp: 100
skills:
  - 1
```

Exploremos la data NHANES. Vamos a explorar la presión arterial en este conjunto de datos.

Primero seleccionemos un grupo para establecer el estándar. Usaremos las mujeres de 20-29 años. Tenga en cuenta que la categoría está codificada con ` 20-29`, con un espacio al frente del `20`! La variable `AgeDecade` es una variable categórica con estas edades.

Para saber si alguien es mujer, puede mirar la variable `Gender`.

`@instructions`
- Filtre el conjunto de datos `NHANES` para incluir solamente las mujeres entre los 20 y 29 años y asigne este nuevo data frame al objeto `tab`.
- Use el pipe para aplicar la función `filter`, con los lógicos apropiados, al conjunto de datos `NHANES`.
    - Recuerde que este grupo de edades está codificado con ` 20-29`, que incluye un espacio. Puede usar `head` para explorar la tabla `NHANES` para construir la llamada correcta a filter.

`@hint`
Use el lógico `AgeDecade == " 20-29" & Gender == "female"` dentro de `filter`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
## rellene lo necesario
tab <- NHANES %>%
```

`@solution`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
tab <- NHANES %>% filter(AgeDecade == " 20-29" & Gender == "female")
```

`@sct`
```{r}
test_error()
test_pipe(absent_msg = "Aquí queremos que use el pipe `%>%`.")
test_function("filter", incorrect_msg = "No olvide aplicar `filter` por `AgeDecade` y por `Gender`")
test_object("tab",incorrect_msg = "Asegurese de definir `tab` y que filtre correctamente.")
success_msg("Buen trabajo!")
```

---

## Ejercicio 2. Presión arterial 2

```yaml
type: NormalExercise
key: 2c14b6405a
lang: r
xp: 100
skills:
  - 1
```

Ahora calcularemos el promedio y la desviación estándar para el subgrupo que definimos en el ejercicio anterior (con respecto a las mujeres de 20-29 años), los cuales usaremos como referencia de lo que es típico.

Determinará el promedio y la desviación estándar de la presiónes arteriales sistólicas, las cuales están almacenadas en la variable `BPSysAve` en el conjunto de datos NHANES.

`@instructions`
- Complete la línea de código para guardar el promedio y la desviación estándar de la presión arterial sistólica como `average` y `standard_deviation` a una variable llamada `ref`.
- Use la función `summarize` después de filtrar para mujeres de 20-29 años de edad y conecte los resultados usando el pipe `%>%`. Cuando haga esto, recuerde que hay entradas `NA` en la data!

`@hint`
- Use `filter` y `summarize` y use el argumento `na.rm=TRUE` cuando calcule el promedio y la deviación estándar. También puede filtrar las entradas NA usando `filter`.
- Asegurese de titular el promedio y la deviación estándar correctamente dentro de `summarize`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
## complete esta línea de código
ref <- NHANES %>% filter(AgeDecade == " 20-29" & Gender == "female") %>%
```

`@solution`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
ref <- NHANES %>%
  filter(AgeDecade == " 20-29" & Gender == "female") %>%
  summarize(average = mean(BPSysAve, na.rm = TRUE), 
            standard_deviation = sd(BPSysAve, na.rm = TRUE))
ref
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "No olvide aplicar `filter` por `AgeDecade` y por `Gender`.")
test_function("summarize",incorrect_msg = "Está creando variables llamadas `average` y `standard_deviation`?")
ex() %>% {
  check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
  check_function(., "sd") %>% check_arg(., "na.rm") %>% check_equal()
}
success_msg("Buen trabajo!")
```

---

## Ejercicio 3. Resumiendo promedios

```yaml
type: NormalExercise
key: 154efca36c
lang: r
xp: 100
skills:
  - 1
```

Ahora repetiremos el ejercicio y generaremos solamente el promedio de la presión arterial para las mujeres de 20-29 años. Para este ejercicio, debe revisar como utilizar el marcador de posición `.` en dplyr o la función `pull`.

`@instructions`
Modifique la línea del código de muestra para asignar el promedio a una variable numérica llamada `ref_avg` usando el `.` o `pull`.

`@hint`
Use el código parecido al código de muestra y entonces agregue el punto: `.$average`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
## modifique el código que escribimos para el ejercicio anterior.
ref_avg <- NHANES %>%
  filter(AgeDecade == " 20-29" & Gender == "female") %>%
  summarize(average = mean(BPSysAve, na.rm = TRUE), 
            standard_deviation = sd(BPSysAve, na.rm=TRUE))
```

`@solution`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
ref_avg <- NHANES %>%
      filter(AgeDecade == " 20-29" & Gender == "female") %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE)) %>%
      .$average
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "No olvide aplicar `filter` por `AgeDecade` y por `Gender`")
test_function("summarize",incorrect_msg = "Está creando una variable llamada `average` y `standard_deviation`?")
ex() %>% {
  check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
}
test_object("ref_avg",incorrect_msg = "Asegurese de definir `ref_avg`")
success_msg("Buen trabajo!")
```

---

## Ejercicio 4. Min y max

```yaml
type: NormalExercise
key: e0deb31386
lang: r
xp: 100
skills:
  - 1
```

Sigamos la práctica calculando dos otros resumenes de data: el mínimo y el máximo.

Una vez más, haremos esto para la variable `BPSysAve` y el grupo de mujeres de 20-29 años.

`@instructions`
- Reporte el valor mínimo y máximo para el mismo grupo que en los ejercicios anteriores.
- Otra vez, use `filter` y `summarize` conectados por el pipe `%>%`. Las funciones `min` y `max` se pueden utilizar para obtener los valores que desea.
- Dentro de `summarize`, guarde el valor mínimo y máximo de la presión arterial sistólica como `minbp` and `maxbp`.

`@hint`
- Eche un vistazo a la solución del ejercicio 3 - pero en vez de `mean` y `sd`, usemos `min` y `max`.
- Recuerde remover las entradas `NA` del conjunto de datos !

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
## complete la línea
NHANES %>%
      filter(AgeDecade == " 20-29"  & Gender == "female") %>%

```

`@solution`
```{r}
library(NHANES)
data(NHANES)
NHANES %>%
      filter(AgeDecade == " 20-29"  & Gender == "female") %>%
      summarize(minbp = min(BPSysAve, na.rm = TRUE), 
                maxbp = max(BPSysAve, na.rm = TRUE))
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "No olvide aplicar `filter` por `AgeDecade` y por `Gender`")
test_function("summarize",incorrect_msg = "Está creando unas variables llamadas `min` y `max`?")
#test_function("min",incorrect_msg = "No olvide incluir `na.rm`")
#test_function("max",incorrect_msg = "No olvide incluir `na.rm`")
ex() %>% {
   check_function(., "min") %>% check_arg(., "na.rm") %>% check_equal()
   check_function(., "max") %>% check_arg(., "na.rm") %>% check_equal()
}
test_output_contains("NHANES %>% filter(AgeDecade == ' 20-29'  & Gender == 'female') %>% summarize(minbp = min(BPSysAve, na.rm = TRUE),maxbp = max(BPSysAve, na.rm = TRUE))",incorrect_msg="Vuelva a intentarlo!")
success_msg("Buen trabajo!")
```

---

## Ejercicio 5. group_by

```yaml
type: NormalExercise
key: 39e2ca43e3
lang: r
xp: 100
skills:
  - 1
```

Ahora practiquemos usar la función `group_by`. 

Lo que vamos a hacer es una operación muy común en la ciencia de data: dividirás una tabla de data en grupos y entonces calcularás estadísticas para cada grupo.

Calcularemos el promedio y la desviación estándar de la presión arterial sistólica para las mujeres de cada grupo de edades separadamente. Recuerde que los grupos de edades están guardados en `AgeDecade`.

`@instructions`
- Use las funciones `filter`, `group_by`, `summarize`, y el pipe `%>%` para calcular el promedio y la desviación estándar de la presión arterial sistólica para las mujeres de cada grupo de edades separadamente.
- Dentro de `summarize`, guarde el promedio y la desviación estándar de la presión arterial sistólica (`BPSysAve`) como `average` y `standard_deviation`.
- Ojo: obvie las advertencias sobre las entradas NA implícitas. Esta advertencia no prevendrá que su código se ejecute o sea calificado correctamente.

`@hint`
- En la llamada `filter` solo filtramos con respecto a `Gender` y no `AgeDecade`.
- `AgeDecade` debe ser usada en la función `group_by`.
- Lo restante es muy parecido al código de los ejercicios anteriores en los que calculamos el promedio y la desviación estándar.
- No olvide remover las entradas `NA`!

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
##complete la lii3ínea con group_by y summarize
NHANES %>%
      filter(Gender == "female") %>%
```

`@solution`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
NHANES %>%
      filter(Gender == "female") %>%
      group_by(AgeDecade) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE))
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "No olvide aplicar `filter` por `Gender`")
test_function("group_by", incorrect_msg = "No olvide aplicar `group_by` por `AgeDecade`")
test_function("summarize",incorrect_msg = "Está creando unas variables llamadas `average` y `standard_deviation`?")
ex() %>% {
   check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
   check_function(., "sd") %>% check_arg(., "na.rm") %>% check_equal()
}
test_output_contains("NHANES %>% filter(Gender == 'female') %>% group_by(AgeDecade) %>% summarize(average = mean(BPSysAve, na.rm = TRUE), standard_deviation = sd(BPSysAve, na.rm=TRUE))",incorrect_msg="Vuélvalo a intentar!")
success_msg("Buen trabajo!")
```

---

## Ejercicio 6. group_by ejemplo 2

```yaml
type: NormalExercise
key: 2b7079d1d7
lang: r
xp: 100
skills:
  - 1
```

Ahora practiquemos usar `group_by` un poco más. Vamos a repetir el ejercicio anterior de calcular el promedio y la desviación estándar de la presión arterial sistólica, pero para los hombres en vez de para las mujeres.

Esta vez no proveeremos tanto código de muestra. Esta vez es por tu cuenta !

`@instructions`
- Calcule el promedio y la desviación estándar de la presión arterial sistólica para los hombres de cada grupo de edades separadamente usando los mismos meétodos que en el ejercicio anterior.
- Guarde el promedio y la desviación estándar de la presión arterial sistólica (`BPSysAve`) como `average` y `standard_deviation`.

Ojo: obvie las advertencias sobre las entradas NA implícitas. Esta advertencia no prevendrá que su código se ejecute o sea calificado correctamente.

`@hint`
Cambie su filtro para `Gender` de manera tal que refleje la nueva categoría - todo lo demás permanece igual que en el ejercicio anterior!

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@solution`
```{r}
library(NHANES)
data(NHANES)
NHANES %>%
      filter(Gender == "male") %>%
      group_by(AgeDecade) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE))
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "No olvide aplicar `filter` por `Gender`")
test_function("group_by", incorrect_msg = "No olvide aplicar `group_by` por `AgeDecade`")
test_function("summarize",incorrect_msg = "Está creando unas variables llamadas `average` y `standard_deviation`?")
ex() %>% {
   check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
   check_function(., "sd") %>% check_arg(., "na.rm") %>% check_equal()
}
test_output_contains("NHANES%>%filter(Gender=='male')%>%group_by(AgeDecade)%>%summarize(average=mean(BPSysAve,na.rm=TRUE),standard_deviation=sd(BPSysAve,na.rm=TRUE))",incorrect_msg="Vuélvalo a intentar!")

success_msg("Buen trabajo!")
```

---

## Ejercicio 7. group_by ejemplo 3

```yaml
type: NormalExercise
key: f653ffcd3a
lang: r
xp: 100
skills:
  - 1
```

Podemos combinar ambos resumenes e incluirlos en una sola línea. Esto es porque `group_by` nos permite agrupar por más de una variable.

Podemos usar `group_by(AgeDecade, Gender)` para agrupar por décadas de edades y por género.

`@instructions`
- Cree una sola tabla de resumen para el promedio y la desviación estándar de la presión arterial sistólica usando `group_by(AgeDecade, Gender)`.
    - Lleve en cuenta que ya no tenemos que aplicar `filter`!
    - Su código dentro de `summarize` debe permanecer igual que en los ejercicios anteriores, y debe usar los nombres `average` y `standard_deviation` de las variables.
- Ojo: obvie las advertencias sobre las entradas NA implícitas. Esta advertencia no prevendrá que su código se ejecute o sea calificado correctamente.

`@hint`
Esto es igual al ejercicio anterior con la excepción de que no filtramos y cambiamos `group_by` para que incluya década de edad y género.

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(NHANES)
data(NHANES)
```

`@solution`
```{r}
library(NHANES)
data(NHANES)
NHANES %>%
      group_by(AgeDecade, Gender) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE))
```

`@sct`
```{r}
test_error()
test_function("group_by", incorrect_msg = "No olvide aplicar `group_by` por `AgeDecade` y por `Gender`")
test_function("summarize",incorrect_msg = "Está creando unas variables llamadas `average` y `standard_deviation`?")
ex() %>% {
   check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
   check_function(., "sd") %>% check_arg(., "na.rm") %>% check_equal()
}
test_output_contains("NHANES %>%
      group_by(AgeDecade, Gender) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE))",incorrect_msg="Vuélvalo a intentar!")
success_msg("Buen trabajo!")
```

---

## Ejercicio 8. Arrange

```yaml
type: NormalExercise
key: 89bb8e55f9
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a explorar las diferencias entre las presiones arteriales sistólicas de distintas razas, como está reportado en la variable `Race1`.

Aprenderemos a usar la función `arrange` para ordenar el resultado de acorde a una variable.

Lleve en cuenta que esta función puede usarse para ordenar cualquier tabla con respecto a un resultado particular. Aquí tiene un ejemplo que ordena por presión arterial sistólica.

```{r}
NHANES %>% arrange(BPSysAve)
```

Si la queremos en orden descendiente podemos usar la función `desc` de la siguiente manera:

```{r}
NHANES %>% arrange(desc(BPSysAve))
```

En este ejemplo, vamos a comparar las presiones arteriales sistoo4ólicas a través de las entradas de la variable `Race1` para los hombres de 40-49 años.

`@instructions`
- Calcule el promedio y la desviación estándar para cada una de las entradas de `Race1` para los hombres en la década de edades entre los 40 y los 49. Recuerde que este grupo de edades está codificado con ` 40-49`, que incluye un espacio.
- Ordene la tabla resultante desde el promedio menor hasta el promedio mayor de presión arterial sistólica.
- Use las funciones `filter`, `group_by`, `summarize`, `arrange`, y el pipe `%>%` para hacer esto en una sola línea de código. 
- Dentro de `summarize`, guarde el promedio y la desviación estándar de la presión arterial sistólica como `average` y `standard_deviation`.

`@hint`
- Esto es muy parecido a ejercicios anteriores, pero con distintos filtros y agrupamientos.
- Tendrá que darle un nombre a su promedio en `summarize` o no podrá usar la función `arrange` para ordenar su data.

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@solution`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
NHANES %>%
      filter(Gender == "male" & AgeDecade==" 40-49") %>%
      group_by(Race1) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE)) %>%
      arrange(average)
```

`@sct`
```{r}
test_function("filter", incorrect_msg = "No olvide aplicar `filter` por `Gender` y `AgeDecade`")
test_function("group_by", incorrect_msg = "No olvide aplicar `group_by` por `Race``")
test_function("summarize",incorrect_msg = "Está creando unas variables llamadas `average` y `standard_deviation`?")
ex() %>% {
   check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
   check_function(., "sd") %>% check_arg(., "na.rm") %>% check_equal()
}
test_function("arrange",incorrect_msg = "`arrange` the variables by the `average`")
test_output_contains("NHANES %>%
      filter(Gender == 'male' & AgeDecade==' 40-49') %>%
      group_by(Race1) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE)) %>%
      arrange(average)",incorrect_msg="Asegurese de que arrange sea llamada con respecto a average y no standard deviation y que tenga la combinación especificada correcta de edad y género!")
success_msg("Buen trabajo!")
```

---

## Fin de la evaluación: Resumiendo con dplyr

```yaml
type: PureMultipleChoiceExercise
key: 35d4331f57
xp: 50
skills:
  - 1
```

TEste es el fin del trabajo asignado de programación de esta sección. Por favor NO avanze a evaluaciones adicionales desde esta página. ADVERTENCIA: si continua las evaluaciones presionando en la flecha para obtener el próximo ejercicio o presionando Ctrl-K, puede que sus evaluaciones NO sean calificadas.

Ya puede cerrar esta ventana para volver a <a href='https://www.edx.org/course/data-science-visualization-harvardx-ph125-2x'>Data Science: Visualization</a>.

`@hint`
- No hint necessary!

`@possible_answers`
- [Fantástico]
- Nope

`@feedback`
- Fabuloso! Ahora regrese al curso en edX!
- Ahora regrese al curso en edX!
