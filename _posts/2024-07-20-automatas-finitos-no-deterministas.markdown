---
title:  "Autómatas finitos no deterministas"
date:   2024-07-20 14:43:00 -0500
categories: [Autómatas finitos no deterministas, Autómatas finitos, Lenguajes regulares]
tags: [afnd, afd, af, lr] 
author: ok
---

El contenido de este artículo le pertenece al Profesor **Andrés Sicard Ramírez**[^1], quien me ha permitido compartirlo por este medio.

---
## Preliminares

### Referencias

Las referencias principales para este artículo son (*Kozen 2012, Lecturas 5 y 6*).

### Convenciones

1. Los números naturales incluyen el cero, es decir, $\mathbb{N} = \\{0, 1, 2, \ldots\\}$.
2. El conjunto potencia de un conjunto $A$ es denotado $2^A$.
3. Los términos *definición inductiva* y *definición recursiva* se usan como sinónimos.

---

## Introducción sobre el no determinismo

- Una computación se considera **no determinista** cuando el siguiente estado de la misma no está completamente determinado por su estado actual. 

- El **no determinismo** es una abstracción fundamental en las Ciencias de la Computación. 

- No determinismo y diseño eficiente de programas:

  > "El famoso problema $P = NP$ —si todos los problemas que se pueden resolver en **tiempo polinomial no determinista** se pueden resolver en **tiempo polinomial determinista**— es un problema abierto importante en la ciencia de la computación y posiblemente uno de los problemas abiertos más importantes en toda la matemática." (Kozen 2012, pág. 25).

---

## Definición de autómata finito no determinista (AFND)

> **Definición:** Un **autómata finito no determinista** (**AFND**) es una estructura
>
> $$N = (Q, \Sigma, \Delta, S, F),$$
>
> donde:
>
> - $Q$ es un conjunto finito, los **estados**.
> - $\Sigma$ es un conjunto finito, el **alfabeto de entrada**.
> - $\Delta : Q \times \Sigma \to 2^Q$, la **función de transición**.
> - $S \subseteq Q$, el conjunto de **estados iniciales**.
> - $F \subseteq Q$, el conjunto de **estados finales**.

---

## Representaciones del AFND

De forma similar a los **AFD**s, los **AFND**s tienen dos maneras de ser representados:

- **Diagrama de transición:** Un diagrama que muestra los estados como nodos y las transiciones como aristas dirigidas etiquetadas con los símbolos del alfabeto de entrada, *permitiendo transiciones simultáneas, ausencia de algunas transiciones y transiciones $\varepsilon$* (**VER AQUÍ**). Esta es la forma más sencilla de representar un AFND.
- **Listando cada una de sus partes:** Consiste en describir $Q$, $\Sigma$, los pares ordenados de la función de transición $\Delta$, $S$ y $F$.

### Ejemplo 1

Encontrar un **AFND** que "acepte" el lenguaje

$$L = \{ x \in \{0, 1\}^* \mid \text{el segundo símbolo desde la derecha es} \ 1\}.$$

y expresarlo con las dos representaciones.

### Actividad 1

1. Encontrar un **AFND**, con la representación de su preferencia, que "acepte" el lenguaje

   $$L = \{ x \in \{ 0, 1 \}^* \mid \text{el quinto símbolo desde la derecha es} \ 1 \ \text{y el tercero es} \ 0\}.$$

1. Encontrar un **AFND**, con la representación de su preferencia, que "acepte" la palabra `help`, es decir, que "acepte" el lenguaje

   $$L = \{ \text{help} \}.$$

**Observaciones:** 

- Estamos hablando desde ahora de lo que puede aceptar un AFND mas no lo hemos definido formalmente aún. En la próxima sección vamos a ver qué es lo que significa.
- También para representar un AFND, contamos con una representación adicional, la de tabla, esta se obtiene por medio del proceso de la construcción de subconjuntos. Esto lo veremos más adelante.

---

## Definición Función de transición extendida para AFNDs: $\hat{\Delta}$

> **Definición:** Sea $N = (Q, \Sigma, \Delta, S, F)$ un **AFND**. La **función de transición extendida**, denotada $\hat{\Delta}$, está recursivamente definida por:
>
> $$
\begin{align}
    \hat{\Delta} : 2^Q \times \Sigma^* &\to 2^Q \\
    \hat{\Delta}(A, \varepsilon) &\stackrel{\text{def}}{=} A, \\
    \hat{\Delta}(A, xa) &\stackrel{\text{def}}{=} \bigcup_{q \in \hat{\Delta}(A, x)} \Delta(q, a) %= \bigcup \left\{\Delta(q, a) \mid q \in \hat{\Delta}(A, x) \right\}.
\end{align}
$$

### Ejemplo 2. Procesando una cadena con la definición recursiva

Para el AFND del ejemplo de [más arriba](#ejemplo-1) $N = (Q,\Sigma, \Delta, S, F)$  así se procesaría la cadena de entrada $01$ a través de la función de transición extendida $\hat{\Delta}$:

<!--
$$
\begin{align}
   \hat{\Delta}(S, 101) &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \hat{\Delta}(S, 10) \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(q_1, 0) \mid q_1 \in \hat{\Delta}(S, 1) \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(q_1, 0) \mid q_1 \in \hat{\Delta}(S, \varepsilon 1) \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(q_1, 0) \mid q_1 \in \bigcup \left\{\Delta(q_3, 1) \mid q_3 \in \hat{\Delta}(S, \varepsilon) \right\} \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(q_1, 0) \mid q_1 \in \bigcup \left\{\Delta(q_3, 1) \mid q_3 \in S \right\} \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(q_1, 0) \mid q_1 \in \bigcup \left\{\Delta(q_3, 1) \mid q_3 \in \left\{p\right\} \right\} \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(q_1, 0) \mid q_1 \in \Delta(p, 1) \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(q_1, 0) \mid q_1 \in \left\{p, q\right\} \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(p, 0), \Delta(q, 0)\right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup  \left\{\left\{p \right\}, \left\{r \right\}\right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \left\{p, r\right\} \right\} \\
\end{align}
$$
-->

$$
\begin{align}
   \hat{\Delta}(S, 01) &= \bigcup_{q_0 \in \hat{\Delta}(S, 0)} \Delta(q_0, 1) \\

   &= \bigcup_{q_0 \in \hat{\Delta}(S, \varepsilon 0)} \Delta(q_0, 1) \\

   &= \bigcup_{q_0 \in \bigcup_{q_1 \in \hat{\Delta}(S, \varepsilon)} \Delta(q_1, 0)} \Delta(q_0, 1) \\

   &= \bigcup_{q_0 \in \bigcup_{q_1 \in S} \Delta(q_1, 0)} \Delta(q_0, 1) \\

   &= \bigcup_{q_0 \in \bigcup_{q_1 \in \left\{p \right\}} \Delta(q_1, 0)} \Delta(q_0, 1) \\

   &= \bigcup_{q_0 \in \Delta(p, 0)} \Delta(q_0, 1) \\

   &= \bigcup_{q_0 \in \left\{p \right\}} \Delta(q_0, 1) \\

   &= \Delta(p, 1) \\
   
   &= \left\{p, q \right\}.
\end{align}
$$
   
<!--
$$
\begin{align}
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(q_1, 0) \mid q_1 \in \hat{\Delta}(S, \varepsilon) \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(q_1, 0) \mid q_1 \in S \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(q_1, 0) \mid q_1 \in \left\{p \right\} \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\Delta(p, 0) \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \bigcup \left\{\left\{p \right\} \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(q_0, 1) \mid q_0 \in \left\{p \right\} \right\} \\
   
   &= \bigcup \left\{\Delta(p, 1) \right\} \\
   
   &= \bigcup \left\{\left\{p, q \right\} \right\} \\
   
   &= \left\{p, q \right\}
\end{align}
$$
-->

**Pregunta:** ¿Qué es $\hat{\Delta}(S, 01) \cap F$?

**Observación:** La manera de calcular $\hat{\Delta}(S, 01)$ con la definición recursiva tiene a no ser una manera "intuitiva" para poder determinar. Sin embargo en virtud al lema que sigue a continuación podremos considerar un procedimiento más adecuado para procesar cadenas.

---

## Lema para determinar $\hat{\Delta}(A, xy)$

> **Lema:** Sea $N = (Q,\Sigma, \Delta, S, F)$ un AFND, con $x, y \in \Sigma^\ast$. Entonces
> 
> $$\hat{\Delta}(A, xy) = \hat{\Delta}(\hat{\Delta}(A, x), y).$$

### Ejemplo 2. Procesando una cadena en un AFND de forma fácil

Para determinar $\hat{\Delta}(S, 01)$ del elemplo de [más arriba](#ejemplo-1) se hace lo siguiente:

$$
\begin{align}
   \hat{\Delta}(S, 01) &= \hat{\Delta}(S, 01) \\
   &= \hat{\Delta}(\hat{\Delta}(S, 0), 1) \\
   &= \hat{\Delta}(\hat{\Delta}(\left\{p \right\}, 0), 1) \\
   &= \hat{\Delta}(\left\{p \right\}, 1) \\
   &= \left\{p, q \right\}.\\
\end{align}
$$

### Actividad 2

Determinar $\hat{\Delta}(S, 011101)$ del elemplo de [más arriba](#ejemplo-1).

---

## Definición de lenguajes aceptados por los AFNDs

De forma similar a los ADF, podemos definir también el lenguaje de aceptación generado por un AFND. Sólo que esta vez debemos tener cuidado con "**comprender porqué usamos intersección en lugar de pertenencia a $F$**"

> **Definición:** Sea $N = (Q, \Sigma, \Delta, S, F)$ un **AFND** y sea $x \in \Sigma^*$.
> 
> 1. La palabra $x$ es **aceptada** por $N$ sí y sólo sí $\hat{\Delta}(S, x) \cap F \neq \emptyset$.
> 
> 1. La palabra $x$ es **rechazada** por $N$ sí y sólo sí $\hat{\Delta}(S, x) \cap F = \emptyset$.
> 
> 1. El **lenguaje aceptado** por el autómata $N$, denotado $L(N)$, es el conjunto de palabras aceptadas por $N$, es decir,
> 
>    $$L(N) \stackrel{\text{def}}{=} \{ x \in \Sigma^* \mid \hat{\Delta}(S, x) \cap F \neq \emptyset \}.$$

**Pregunta:** Dado un AFD $M = (Q_M, \Sigma, \delta, s, F_M)$, ¿podemos construir un AFND $N = (Q_N, \Sigma, \Delta, S, F_N)$ que sólo sea capaz de aceptar a $L(M)$?

**Observación:** Dada la flexibilidad que tenemos ahora para solucionar problemas con AFND, parece que los AFND tienen mayor poder computacional que los AFD. Sin embargo, temo que no podemos estar más alejados de la realidad. **Los lenguajes que son capaces de aceptar los AFNDs son exactamente los mismos que aceptan los AFDs**, es decir, **los AFDs y los AFNDs tienen el mismo poder computacional.**

---

## Igualdad del poder computacional de los AFDs y los AFNDs

El resultado principal de este artículo es que los AFDs y los AFNDs tienen el mismo poder computacional. Y esto lo dejaremos consolidado en los siguiente teoremas.

### Teorema transformar un AFD en un AFND

> **Teorema:** Sea $M = (Q, \Sigma, \delta_M, s_M, F)$ un AFD. Entonces existe un AFND $N = (Q, \Sigma_N, \Delta_N, S_N, F)$ tal que
> 
> $$L(M) = L(N).$$

**Observación:** Para la demostración, clave secreta es definir de manera adecuada $\Delta_N$ y $S_N$.

### Teorema transformar un AFND en un AFD

> **Teorema:** Sea $N = (Q_N, \Sigma, \Delta_N, S_N, F_N)$ un AFND. Entonces existe un AFD $M = (Q_M, \Sigma, \delta_M, s_M, F_M)$ tal que
> 
> $$L(N) = L(M).$$

**Observación:** Para la demostración del teorema [de arriba](#teorema-transformar-un-afnd-en-un-afd) necesitamos construir el AFD $M$ usando la **construcción por subconjuntos** y un lema que describe una propiedad clave de esta construcción.

### Definición de construcción del AFD por subconjunto

> **Definición:** Dado $N = (Q_N, \Sigma, \Delta_N, S_N, F_N)$ un AFND. Sea $M = (Q_M, \Sigma, \delta_M, s_M, F_M)$ el **AFD construido por subconjuntos** donde
>
> $$
\begin{align}
   Q_M &\stackrel{\text{def}}{=} 2^{Q_N}, \\
   \delta_M(A, a) &\stackrel{\text{def}}{=} \hat{\Delta}_N(A, a), \ \text{para todo} \ A \in Q_M \ \text{y} \ a \in \Sigma, \\
   s_M &\stackrel{\text{def}}{=} S_N, \\
   F_M &\stackrel{\text{def}}{=} \left\{A \subseteq Q_N \mid A \cap F_N \neq \emptyset \right\}.
\end{align}
$$

**Pregunta:** ¿$A \in Q_M$ significa lo mismo que $A \subseteq Q_N$?

### Lema sobre el AFD construido por subconjuntos

> **Lema:** Sean $N = (Q_N, \Sigma, \Delta_N, S_N, F_N)$ un AFND y $M = (Q_M, \Sigma, \delta_M, s_M, F_M)$ el AFD construido por subconjuntos. Entonces para todo $A \subseteq Q_N$ y $x \in \Sigma^\ast$.
>
> $$\hat{\delta}_M(A, x) = \hat{\Delta}_N(A, x).$$

**Observacies:** La demostración de este lema se hace por inducción sobre $x$.

**Pregunta:** Dado el [lema de arriba](#lema-sobre-el-afd-construido-por-subconjuntos) ¿Cómo demostramos el [teorema principal](#teorema-transformar-un-afnd-en-un-afd)?

### Definición de autómatas finitos (AFs)

Dado que a todos los lenguajes regulares los podemos asociar tanto con AFDs como con AFNDs podemos tener la siguiente definición

> **Definición:** Un autómata finito determinista o no determinista es un **autómata finito**.

---

## "Más ventajas de los AFND": Las $\varepsilon$-transiciones

Para definir un AFND podemos utilizar $\varepsilon$-transiciones, lo cual es de gran ventaja para el diseño de AFNDs, sin embargo no representa un aumento en el poder computacional.

> **Definición:** Una **$\varepsilon$-transición** es una transición con etiqueta $\varepsilon$ y está reservada sólo para AFNDs.

### Ejemplo 3

Determinar si el lenguaje conformado por cadenas de $a$es de longitudes $5$ o $3$ es un lenguaje regular.

**Pregunta:** ¿Por qué no es adecuado definir $\varepsilon$-transiciones sobre AFDs?

---

## Propiedades de clausura sobre los lenguajes regulares

Recordemos que en el artículo [Autómatas finitos deterministas y lenguajes regulares](https://opraupe0017.github.io/LFCBlog/aut%C3%B3matas/finitos/lenguajes/regulares/2024/07/19/automatas-finitos-deterministas-y-lenguajes-regulares.html#teorema-clausura-de-la-uni%C3%B3n-de-lenguajes-regulares) vimos algunas propiedades de clausura sobre lesnguajes regulares. Resulta que hay más.

> **Teorema:** Dados dos lenguajes regulares $L_1$ y $L_2$ se cumple la **propiedad de clausura** sobre las operaciones $\sim$, $\cap$, $\cup$, $\cdot$ y $\ast$, es decir, los siguientes lenguajes son **lenguajes regulares**:
>
> $$
\begin{align}
\sim &L_1 \\
L_1 &\cap L_2 \\
L_1 &\cup L_2 \\
&L_1L_2 \\
&L_1^\ast
\end{align}
$$

**Observación:** Sólo faltaba comentar que la operación **concatenación** y la **clausura de Kleene**.

---

### Teorema clausura de la concatenación de lenguajes regulares

> **Teorema:** Dados los lenguajes $L_1$ y $L_2$. Si $L_1$ y $L_2$ son **lenguajes regulares**, entonces 
>
> $$L_1L_2$$
>
> también es un **lenguaje regular**.

**Observación:** Sólo basta con agregar $\varepsilon$-transiciones de manera adecuada en algunos lugares...

---

### Teorema clausura de la clausura de Kleene de lenguajes regulares

> **Teorema:** Dados el lenguaje $L$. Si $L$ es un **lenguaje regulare**, entonces 
>
> $$L^\ast$$
>
> también es un **lenguaje regular**.

**Observación:** Sólo basta con agregar $\varepsilon$-transiciones de manera adecuada en algunos lugares...

---

## Referencias

- _Hopcroft, John E., Rajeev Motwani y Jefferey D. Ullman_ [1979] (2007). **Introduction to Automata Theory, Languages, and Computation**. 3.a ed. Pearson Education.

- _Kozen, Dexter C._ [1997] (2012). **Automata and Computability**. Third printing. Undergraduate Texts in Computer Science. Springer. doi: [10.1007/978-1-4612-1844-9](https://doi.org/10.1007/978-1-4612-1844-9)

---

[^1]: http://www1.eafit.edu.co/asr/cursos/st0270-lenguajes-formales-y-compiladores/index.html

---

**¡Gracias por leer este post!**
