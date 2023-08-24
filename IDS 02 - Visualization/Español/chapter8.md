---
título: Explorando la base de datos de gapminder 
descripción: Visualización de resultados de gapminder con dplyr y ggplot
---

## Ejercicio 1. Esperanza de vida vs fertilidad - parte 1 

```yaml
type: NormalExercise
key: 2c12ac9e9b
lang: r
xp: 100
skills:
  - 1
```

La fundación Gapminder (www.gapminder.org) es una organización sin fines de lucro ubicada en Suecia que promueve desarrollo global por medio del uso de estadísticas que pueden ayudar a reducir creencias erradas sobre desarrollo global. 

`@instructions`
- Por medio del uso de ggplot y la capa puntos, genere un gráfico de dispersión con datos sobre esperanza de vida versus fertilidad para el continente africano en 2012. Esto significa que la fertilidad deberá ser graficada en el eje x y la esperanza de vida en el eje y.  
- Recuerde que puede utilizar la consola de R para explorar la base de datos de gapminder para identificar los nombres de las columnas en la base de datos. 
- En este ejercicio nosotros le proveemos partes de código para que ponga en marcha su codificación. Usted deberá llenar lo que está faltante. Pero note que más adelante, en los siguientes ejercicios, requeriremos que usted escriba la mayoría de su código. 

`@hint`
- Usted deberá `filter` para encontrar el continente y el año de nuestro interés. 
- Asegúrese de llamar `ggplot(aes(firstvar, secondvar)` para reemplazar `firstvar` y `secondvar` con los nombres apropiados para graficar la esperanza de vida en el eje y, mientras que la fertilidad en el eje x.  
- Puede añadir la capa puntos usando `geom_point`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
## llene las partes faltantes en filter y aes 
gapminder %>% filter( & ) %>%
  ggplot(aes( , )) +
  geom_point()
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder %>% filter(continent=="Africa" & year == 2012) %>%
  ggplot(aes(fertility, life_expectancy)) +
  geom_point()
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "No olvide filtrar con `filter` por el continente `Africa` y el año `year` 2012")
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

## Ejercicio 2. Esperanza de vida vs fertilidad - parte 2 - colorear su gráfico 

```yaml
type: NormalExercise
key: ba2e354cea
lang: r
xp: 100
skills:
  - 1
```

Note que hay algo de variabilidad en la esperanza de vida y fertilidad ya que algunos países africanos tienen muy altas esperanzas de vida. Parece también que hay tres agrupaciones en el gráfico. 

`@instructions`
Rehaga el gráfico que hicimos en ejercicios previos pero esta vez utilice color para distinguir las diferentes regiones de África para ver si esto explica las agrupaciones. ¡Recuerde que puede explorar los datos de gapminder para ver cómo están etiquetadas las regiones de África en la base de datos! 

Use `color` en lugar de `col` dentro de `ggplot` - mientras que ambas son equivalentes en R, el revisor de esta tarea estará calificando específicamente `color`.

`@hint`
Dentro de `aes` hay una variable `color`. Por lo demás, su código deberá ser el mismo que en el ejercicio pasado. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder %>% filter(continent=="Africa" & year == 2012) %>%
  ggplot(aes(fertility, life_expectancy, color = region)) +
  geom_point()
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "No olvide filtrar `filter` por el continente `Africa` y `year` 2012")
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_point", not_called_msg="¿Añadió la capa `geom_point()`?")
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 3. Esperanza de vida vs fertilidad - parte 3 - seleccionar país y región

```yaml
type: NormalExercise
key: 6f7eef9d12
lang: r
xp: 100
skills:
  - 1
```

Mientras que muchos de los países en la agrupación alta esperanza de vida/baja fertilidad pertenecen al norte de África, tres países no pertenecen. 

`@instructions`
- Genere una tabla mostrando el país y región para los países africanos (use `select`) que en 2012 tuvieron tasas de fertilidad de 3 o menos y esperanza de vida de al menos 70. 
- Asigne su resultado a un marco de datos llamado `df`.

`@hint`
Use `filter` y luego `select`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
df <- gapminder %>% 
  filter(continent=="Africa" & year == 2012 & fertility <=3 & life_expectancy>=70) %>%
  select(country, region)
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "No olvide filtrar `filter` por continente, año, fertilidad y esperanza de vida (continent, year, fertility, life_expectancy)")
test_function("select", incorrect_msg = "No olvide seleccionar `select` país y región (country, region)")
ex() %>% {
   check_object(.,"df") %>% check_equal()
}
test_student_typed(c("fertility <= 3", "3 >= fertility", "fertility < 4", "4 > fertility"),  
  not_typed_msg = "Recuerde restringir los datos a una fertilidad máxima de 3")
test_student_typed(c("life_expectancy >= 70", "70 <= life_expectancy"),
  not_typed_msg = "Recuerde restringir los datos a una esperanza de vida de al menos 70")
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 4. Esperanza de vida y la guerra de Vietnam - parte 1 

```yaml
type: NormalExercise
key: 91e3023cfd
lang: r
xp: 100
skills:
  - 1
```

La guerra de Vietnam duró de 1955 a 1975. ¿Los datos apoyan a la idea que una guerra tiene efecto negativo en la esperanza de vida? Vamos a crear un gráfico de serie de tiempo que cubre el periodo de 1960 a 2010 con la esperanza de vida para Vietnam y los Estados Unidos, usando colores para distinguir entre ambos países. Comenzaremos el análisis por medio de generar una tabla de datos. 

`@instructions`
- Use `filter` para crear una tabla con los datos de los años desde 1960 a 2010 en Vietnam y los Estados Unidos.
- Guarde la tabla en un objeto llamado `tab`.

`@hint`
- Recuerde, ¡aún sigue utilizando la base de datos de gapminder! 
- Usted puede crear variables que contengan los años y países requeridos y usarlos cuando usa `filter`. Por ejemplo, si quiere datos de México y África del Sur con todos los años, puede usar `mycountries <- c("Mexico", "South Africa")` y posteriormente filtrar la base de datos de gapminder usando `filter(country %in% mycountries)`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
years <- 1960:2010
countries <- c("United States", "Vietnam")
tab <- gapminder %>% filter(year %in% years & country %in% countries)
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "No olvide filtrar `filter` por país y año")
ex() %>% {
   check_object(.,"tab") %>% check_equal()
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 5. Esperanza de vida y la guerra de Vietnam - parte 2 

```yaml
type: NormalExercise
key: 6fe8a21728
lang: r
xp: 100
skills:
  - 1
```

Ahora que ha creado una tabla de datos en el ejercicio 4, es tiempo de graficar los datos para los dos países. 

`@instructions`
- Use `geom_line` para graficar la esperanza de vida vs años para Vietnam y los Estados Unidos y guarde los gráficos como `p`. La tabla de datos estará guardada en `tab`.
- Use color para distinguir entre ambos países. 
- Imprima el objeto `p`.

`@hint`
- De nuevo recuerde que puede ver en la base de datos de gapminder cómo se llaman las diferentes columnas. 
- El año deberá ser graficado en el eje x y la esperanza de vida en el eje y. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
years <- 1960:2010
countries <- c("United States", "Vietnam")
tab <- gapminder %>% filter(year %in% years & country %in% countries)
```

`@sample_code`
```{r}
p <- # el código para sus gráficos va aquí - la tabla de datos estará gusrdada como `tab`
p
```

`@solution`
```{r}
p <- tab %>% ggplot(aes(x=year,y=life_expectancy,color=country)) + geom_line()
p
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_line", not_called_msg="¿Añadió la capa `geom_line()`?")
}
success_msg("Note la caída en esperanza de vida durante el tiempo de la guerra.")
```

---

## Ejercicio 6. Esperanza de vida en Camboya

```yaml
type: NormalExercise
key: 1df58235ad
lang: r
xp: 100
skills:
  - 1
```

Camboya también estuvo involucrado en este conflicto y, más tarde en esta guerra, Pol Pot y su comunista Khmer Rouge tomaron control y gobernaron Camboya de 1975 a 1979. Él es considerado como uno de los dictadores más brutales en la historia. ¿Los datos apoyan dicha afirmación? 

`@instructions`
Use una sola línea de código para crear un gráfico de serie de tiempo de 1960 a 2010 de esperanza de vida vs año para Camboya. 

`@hint`
- Puede modificar su código `filter` del ejercicio 4 para crear un gráfico de serie de tiempo para Camboya en lugar de Estados Unidos y Vietnam. 
- Después ingrese ese resultado en `ggplot`, de nuevo graficando año en el eje x y esperanza de vida en el eje y. 
- Recuerde utilizar `geom_line()` para crear el gráfico. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder %>% filter(year >= 1960 & year <= 2010 & country == "Cambodia") %>% 
  ggplot(aes(year, life_expectancy)) + geom_line()
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
   check_function(., "geom_line", not_called_msg="¿Añadió la capa `geom_line()`?")
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 7. Dólares por día - parte 1 

```yaml
type: NormalExercise
key: 6ed3eff502
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a calcular y graficar dólares por día para países africanos en 2010 usando datos del PIB. 

En la primera parte de este análisis, vamos a crear la variable de dólares por día. 

`@instructions`
- Use `mutate` para crear la variable `dollars_per_day` (dólares por día), la cual es definida por PIB/población/365. 
- Genere la variable `dollars_per_day` para países africanos para el año 2010.
- Remueva cualquier valor `NA`.
- Guarde la base de datos cambiada como `daydollars`.

`@hint`
- Primero mute, `mutate` y luego filtre, `filter`.
- Puede remover los valores `NA` usando `!is.na(dollars_per_day)`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
daydollars <- # escriba su código aquí
```

`@solution`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
daydollars <- gapminder %>% mutate(dollars_per_day = gdp/population/365) %>% filter(continent == "Africa" & year == 2010 & !is.na(dollars_per_day)) 
```

`@sct`
```{r}
test_error()
ex() %>% check_object("daydollars") %>% check_equal()
test_function("filter", incorrect_msg = "Recuerde filtrar `filter` por continente y año")
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 8. Dólares por día - parte 2

```yaml
type: NormalExercise
key: 6d64ddb280
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a calcular y graficar dólares por día para países africanos en 2010 usando datos del PIB. 

En la segunda parte de este análisis, vamos a graficar la densidad suave usando un logaritmo (base 2) en el eje x.

`@instructions`
- La base de datos que incluye la variable `dollars_per_day` está cargada previamente como `daydollars`.
- Genere un gráfico de densidad suave para dólares por día con `daydollars`.
- Use `scale_x_continuous` para cambiar el eje x a una escala de logaritmo (base 2).

`@hint`
- Use `ggplot` para graficar `dollars_per_day`
- Use `geom_density` para crear el gráfico de densidad suave. 
- Use `scale_x_continuous(trans = "log2")` para transformar el eje x. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
daydollars <- gapminder %>% mutate(dollars_per_day = gdp/population/365) %>% filter(continent == "Africa" & year == 2010 & !is.na(dollars_per_day))
```

`@sample_code`
```{r}
# su código aquí
```

`@solution`
```{r}
daydollars %>% ggplot(aes(dollars_per_day)) + geom_density() + scale_x_continuous(trans = "log2")
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density", not_called_msg="¿Añadió la capa de `geom_density()`?")
   check_function(., "scale_x_continuous") %>% check_arg(., "trans") %>% check_equal(eval = TRUE)
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 9. Dólares por día - parte 3 - múltiples gráficos de densidad 

```yaml
type: NormalExercise
key: 686da17725
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a combinar las herramientas de graficar que hemos usado en los dos ejercicios anteriores para crear gráficos de densidad para múltiples años. 

`@instructions`
- Genere la variable `dollars_per_day` como en el ejercicio 7, pero para países africanos en los años 1970 y 2010 en esta ocasión.
- Asegúrese de remover cualquier valor `NA`.
- Genere un gráfico de densidad suave con los dólares por día para 1970 y 2010 usando una escala de logaritmo (base 2) para el eje x. 
- Use `facet_grid` para mostrar un gráfico de densidad suave diferente para 1970 y 2010.

`@hint`
- Cambie la manera en la que llama `filter` para incluir ambos años. 
- Añada `facet_grid(year~.)` al final para mostrar ambos gráficos. 
- ¡Todo lo demás se mantiene de la misma manera que en ejercicios pasados!

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year %in% c(1970,2010) & !is.na(dollars_per_day)) %>%
  ggplot(aes(dollars_per_day)) + 
  geom_density() + 
  scale_x_continuous(trans = "log2") + 
  facet_grid(year ~ .)
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
   check_function(., "facet_grid")
}
test_student_typed("scale_x_continuous(trans = \"log2\")",  
  not_typed_msg = "Recuerde utilizar una escala log2 en el eje x")
success_msg("Note el cambio en los gráficos de densidad para los dos diferentes años.")
```

---

## Ejercicio 10. Dólares por día - parte 4 - gráfico de densidad apilado

```yaml
type: NormalExercise
key: a73ffee200
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a editar el código del ejercicio 9 para mostrar el gráfico de densidad apilado para cada región en África. 

`@instructions`
- La mayor parte del código será el mismo que en el ejercicio 9:
- Genere la variable `dollars_per_day` como en el ejercicio 7, pero para países africanos para los años 1970 y 2010 esta vez.
- Asegúrese de remover cualquier valor `NA`.
- Genere un gráfico de densidad suave para dólares por día para 1970 y 2010 usando una escala logarítmica (base 2) para el eje x. 
- Use `facet_grid` para mostrar diferentes gráficos de densidad para 1970 y 2010. 
- Asegúrese de que las densidades son suaves por medio del uso de `bw = 0.5`.
- Use los argumentos `fill` y `position` donde sea apropiado para crear gráficos de densidad apilados para cada región. 

`@hint`
- Use `fill = region` en `aes`.
- Use `position = "stack"` en `geom_density`, junto con `bw = 0.5`.
- ¡Todo lo demás deberá ser lo mismo! 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)

gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year %in% c(1970,2010) & !is.na(dollars_per_day)) %>%  
  ggplot(aes(dollars_per_day, fill = region)) + 
  geom_density(bw=0.5, position = "stack") + 
  scale_x_continuous(trans = "log2") + 
  facet_grid(year ~ .)
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "fill") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density") %>% {
       check_arg(., "bw") %>% check_equal(eval = FALSE)
       check_arg(., "position") %>% check_equal(eval = FALSE)
   }
   check_function(., "facet_grid")
}
test_student_typed("scale_x_continuous(trans = \"log2\")",  
  not_typed_msg = "Recuerde usar la escala log2 en el eje x")
success_msg("Mire los gráficos - ¿diferentes regiones en África muestran distintos patrones?")
```

---

## Ejercicio 11. Gráfico de dispersión sobre mortalidad infantil - parte 1 

```yaml
type: NormalExercise
key: bb1f9910e7
lang: r
xp: 100
skills:
  - 1
```

Vamos a continuar analizando patrones en la base de datos de gapminder por medio de graficar tasas de mortalidad infantil versus dólares por día en países africanos. 

`@instructions`
- Genere la variable de dólares por día `dollars_per_day` usando `mutate` y filtre `filter` para el año 2010 para países africanos. 
- Recuerde remover los valores `NA` para `infant_mortality` y `dollars_per_day`.
- Guarde la base de datos mutada en `gapminder_Africa_2010`.
- Realice un gráfico de dispersión `infant_mortality` versus `dollars_per_day` para los países en el continente africano. 
- Use color para denotar las diferentes regiones de África. 

`@hint`
- Como en ejercicios previos, use `mutate` para generar `dollars_per_day`, que es igual a PIB/población/365.
- Usted debe filtrar `filter` para ambos `continent` y `year`.
- Retire los valores `NA` para `dollars_per_day` y `infant_mortality`.
- `geom_point()` puede ser usado para crear un gráfico de dispersión. 
- `color = region` corresponde dentro de `aes`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder_Africa_2010 <- # crea la base de datos mutada 

# ahora hacemos el gráfico de dispersión 
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder_Africa_2010 <- gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year == 2010 & !is.na(dollars_per_day) & !is.na(infant_mortality))

gapminder_Africa_2010 %>%  ggplot(aes(dollars_per_day, infant_mortality, color = region)) +
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
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_point") 
}
success_msg("¡Buen trabajo! ¿Parece que existe una relación entre dólares por día y mortalidad infantil?")
```

---

## Ejercicio 12. Gráfico de dispersión sobre mortalidad infantil - parte 2 - eje logarítmico

```yaml
type: NormalExercise
key: b50dffa3d0
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a transformar el eje x del gráfico del ejercicio anterior. 

`@instructions`
- La base de datos mutada está precargada como `gapminder_Africa_2010`.
- Como en el ejercicio previo, haga un grafico de dispersión de `infant_mortality` versus `dollars_per_day` para países del continente africano. 
- Como en el ejercicio previo, use color para denotar las diferentes regiones de África. 
- Transforme el eje x a una escala logarítmica (base 2).

`@hint`
El código para graficar es el mismo que en el ejercicio previo - solamente añada la transformación del eje usando `scale_x_continuous` con el argumento apropiado. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder_Africa_2010 <- gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year == 2010 & !is.na(dollars_per_day) & !is.na(infant_mortality))
```

`@sample_code`
```{r}
gapminder_Africa_2010 %>% # el código para graficar va aquí 
```

`@solution`
```{r}
gapminder_Africa_2010 %>% 
  ggplot(aes(dollars_per_day, infant_mortality, color = region)) +
  geom_point() + 
  scale_x_continuous(trans = "log2")
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_point")
   check_function(., "scale_x_continuous") %>% check_arg(., "trans") %>% check_equal() 
}
success_msg("¡Buen trabajo! ¿La transformación ayuda a establecer una relación más clara entre dólares por día y mortalidad infantil?")
```

---

## Ejercicio 13. Gráfico de dispersión sobre mortalidad infantil - parte 3 - añadiendo etiquetas

```yaml
type: NormalExercise
key: 2190d733ca
lang: r
xp: 100
skills:
  - 1
```

Note que hay una gran variación en mortalidad infantil y dólares por día a través de los países africanos. 

Como ejemplo, un país tiene tasas de mortalidad infantil menores a 20 por 1000 y dólares por día de 16, mientras que otro país tiene mortalidad infantil de poco más de 10% y dólares por día de aproximadamente 1. 

En este ejercicio, reharemos el gráfico del ejercicio 12 con los nombres de los países en lugar de puntos, de manera que podremos identificar qué país es cuál. 

`@instructions`
- La base de datos mutada y precargada es `gapminder_Africa_2010`.
- Como en  ejercicios previos, haga un gráfico de dispersión de `infant_mortality` versus `dollars_per_day` para países del continente africano. 
- Como en el ejercicio anterior, use color para denotar las diferentes regiones de África.  
- Como en el ejercicio anterior, transforme el eje x para estar en escala logarítmica (base 2).
- Añada una capa `geom_text` para mostrar los nombres de los países en lugar de puntos. 
- Asegúrese de llamar `aes()` dentro de llamar `ggplot()`.

`@hint`
- Use la capa `geom_text` en lugar de `geom_point` para mostrar los nombres de los países. 
- También necesitará `label = country` para tener las etiquetas adecuadas. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder_Africa_2010 <- gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year == 2010 & !is.na(dollars_per_day) & !is.na(infant_mortality))
```

`@sample_code`
```{r}
gapminder_Africa_2010 %>% # su código de graficar va aquí
```

`@solution`
```{r}
gapminder_Africa_2010 %>% 
  ggplot(aes(dollars_per_day, infant_mortality, color = region, label = country)) +
  geom_text() + 
  scale_x_continuous(trans = "log2")
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
       check_arg(., "label") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_text")
   check_function(., "scale_x_continuous") %>% check_arg(., "trans") %>% check_equal() 
}
success_msg("¡Buen trabajo!")
```

---

## Ejercicio 14. Gráfico de dispersión sobre mortalidad infantil - parte 4 - comparación entre gráficos de dispersión

```yaml
type: NormalExercise
key: 94bb0c97d6
lang: r
xp: 100
skills:
  - 1
```

Ahora vamos a ver los cambios en los patrones de mortalidad infantil y dólares por día en países africanos entre 1970 y 2010. 

`@instructions`
- Genere `dollars_per_day` usando `mutate` y filtre `filter` para los años 1970 y 2010 para los países africanos. 
- Recuerde remover los valores `NA`.
- Así como en los ejercicios previos, haga un gráfico de dispersión de mortalidad infantil `infant_mortality` versus dólares por día `dollars_per_day` para países del continente africano. 
- Así como en el ejercicio previo, use color para denotar las diferentes regiones de África.
- Así como en el ejercicio previo, transforme el eje x para que sea una escala logarítmica (base 2).
- Así como en el ejercicio previo, añada una capa para mostrar los nombres de los países además de los puntos. 
- Use `facet_grid` para mostrar diferentes gráficos para 1970 y 2010. Asegúrese de alinear los gráficos verticalmente. 

`@hint`
Mire atrás al ejercicio 9 para un recordatorio de cómo usar `facet_grid` si necesita ayuda. Todo el resto del código es muy similar al hecho en ejercicios anteriores. 

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year %in% c(1970, 2010) & !is.na(dollars_per_day) & !is.na(infant_mortality)) %>%
  ggplot(aes(dollars_per_day, infant_mortality, color = region, label = country)) +
  geom_text() + 
  scale_x_continuous(trans = "log2") +
  facet_grid(year~.)
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
       check_arg(., "label") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_text")
   check_function(., "facet_grid") %>% check_arg(., "rows") %>% check_equal(eval = FALSE)
   check_function(., "scale_x_continuous") %>% check_arg(., "trans") %>% check_equal(eval = FALSE) 
}
success_msg("¡Buen trabajo!")
```

---

## Fin de la Evaluación: Explorando la base de datos de gapminder 

```yaml
type: PureMultipleChoiceExercise
key: 35d4331f57
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
