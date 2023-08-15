# Tarea 2: Anscombe Quartet
## Descripción del algoritmo que gráfica los 4 datasets de la cuarteta de Anscombe

Se crea la función ff que representa un modelo lineal con la variable dependiente/respuesta "y" y la variable independiente/predictora "x"
#+begin_src r
ff <- y ~ x 
#+end_src

Se crea una lista llamada mods en el que cada elemento se llama lm1,..., lm4. y estos elementos son del 1 al 4. Se asignan los nombres con setNames de los elementos de la lista y con paste0 es que se crean como tal. 
#+begin_src r
mods <- setNames(as.list(1:4), paste0("lm", 1:4))
#+end_src

Luego se crea un ciclo for iterando del 1 al 4

Dentro del for, esta línea actualiza las variables predictoras y de respuesta en la fórmula ff utilizando la función lapply. Crea una lista de dos nombres de variables: "yi" y "xi", donde i es el índice del bucle. Luego convierte estos nombres de variables en símbolos utilizando as.name y los asigna al segundo y tercer elemento de la fórmula ff.
#+begin_src r
ff[2:3] <- lapply(paste0(c("y","x"), i), as.name)
#+end_src

Luego, esta línea ajusta un modelo de regresión lineal (lm) utilizando la fórmula ff y el conjunto de datos anscombe. Almacena el objeto del modelo tanto en la variable lmi como en la lista mods en el índice correspondiente a la iteración actual.
#+begin_src r
mods[[i]] <- lmi <- lm(ff, data = anscombe)
#+end_src

Saliendo del anterior ciclo, con esta línea decimos que se configuran los parámetros del trazado de la gráfica en op con el comando par. Delimitamos la cuadrícula a un 2x2 con mfrow y se ajustan los márgenes con mar. Luego Crea el márgen externo con oma. 

#+begin_src r
op <- par(mfrow = c(2, 2), mar = 0.1+c(4,4,1,1), oma =  c(0, 0, 2, 0))
#+end_src

Entramos a otro for que itera de nuevo del 1 al 4
Dentro de este ciclo:
Se actualiza las variables predictoras y de respuesta en la fórmula ff basándose en la iteración actual del bucle.
#+begin_src r
ff[2:3] <- lapply(paste0(c("y","x"), i), as.name)
#+end_src

Luego, para cada actualización, generamos las gráficas de puntos. Cada punto será azul y la línea naranja. 
#+begin_src r
plot(ff, data = anscombe, col = "blue", pch = 19, cex = 1.2, xlim = c(3, 19), ylim = c(3, 13))
abline(mods[[i]], col = "orange")
#+end_src

Por último, esta línea restaura los parámetros que habíamos puesto en op
#+begin_src r
par(op)
#+end_src


