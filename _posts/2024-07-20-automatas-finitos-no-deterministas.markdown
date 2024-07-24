---
layout: post
title:  "Autómatas finitos no deterministas"
date:   2024-07-29 14:43:00 -0500
categories: autómatas finitos lenguajes regulares
author: Oscar García
---

El contenido de este artículo le pertenece al Profesor [**Andrés Sicard Ramírez**](http://www1.eafit.edu.co/asr/cursos/st0270-lenguajes-formales-y-compiladores/index.html), quien me ha permitido compartirlo por este medio.

## Contenidos
{:.no_toc}

* TOC
{:toc}

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
> - $\Delta : 2^Q \times \Sigma \to 2^Q$, la **función de transición**.
> - $S \subseteq Q$, el conjunto de **estados iniciales**.
> - $F \subseteq Q$, el conjunto de **estados finales**.

---

## Definición Función de transición extendida para AFNDs: $\hat{\Delta}$

> **Definición:** Sea $N = (Q, \Sigma, \Delta, S, F)$ un **AFND**. La **función de transición extendida**, denotada $\hat{\Delta}$, está recursivamente definida por:
>
> $$
> \begin{align*}
>     \hat{\Delta} : 2^Q \times \Sigma^* &\to 2^Q \\
>     \hat{\Delta}(A, \varepsilon) &= A, \\
>     \hat{\Delta}(A, xa) &= \bigcup_{q \in \hat{\Delta}(A, x)} \Delta(q, a).
> \end{align*}
> $$

---

## Representaciones del AFD

De forma similar a los **AFD**s, los **AFND**s tienen dos maneras de ser representados:

- **Diagrama de transición:** Un diagrama que muestra los estados como nodos y las transiciones como aristas dirigidas etiquetadas con los símbolos del alfabeto de entrada, *permitiendo transiciones simultáneas, ausencia de algunas transiciones y transiciones $\varepsilon$* (**VER AQUÍ**). Esta es la forma más sencilla de representar un AFND.
- **Listando cada una de sus partes:** Consiste en describir $Q$, $\Sigma$, los pares ordenados de la función de transición $\Delta$, $S$ y $F$.

### Ejemplo

Encontrar un **AFND** que "acepte" el lenguaje

$$L = \{ x \in \{0, 1\}^* \mid \text{el segundo símbolo desde la derecha es} \ 1\}.$$

y expresarlo con las dos representaciones.

### Actividad 1

1. Encontrar un **AFND**, con la representación de su preferencia, que "acepte" el lenguaje

   $$L = \{ x \in \{ 0, 1 \}^* \mid \text{el quinto símbolo desde la derecha es} \ 1 \ \text{y el tercero es} \ 0\}.$$

1. Encontrar un **AFND**, con la representación de su preferencia, que "acepte" la palabra `help`, es decir, que "acepte" el lenguaje

   $$L = \{ \text{help} \}.$$

> **Observaciones:** 
>
> - _Estamos hablando desde ahora de lo que puede aceptar un AFND mas no lo hemos definido formalmente aún. En la próxima sección vamos a ver qué es lo que significa._
> - _También para representar un AFND, contamos con una representación adicional, la de tabla, esta se obtiene por medio del proceso de la construcción de subconjuntos. Esto lo veremos más adelante._

---

## Definición de lenguajes aceptados por los AFNs

> **Definición:** Sea $N = (Q, \Sigma, \Delta, S, F)$ un **AFND** y sea $x \in \Sigma^*$.
> 
> 1. La palabra $x$ es **aceptada** por $N$ sí y sólo sí $\Delta(\hat{S}, x) \cap F \neq \emptyset$.
> 
> 1. La palabra $x$ es **rechazada** por $N$ sí y sólo sí $\Delta(\hat{S}, x) \cap F = \emptyset$.
> 
> 1. El **lenguaje aceptado** por el autómata $N$, denotado $L(N)$, es el conjunto de palabras aceptadas por $N$, es decir,
> 
>    $$L(N) \stackrel{\text{def}}{=} \{ x \in \Sigma^* \mid \Delta(\hat{S}, x) \cap F \neq \emptyset \}.$$


---

## Referencias

- _Hopcroft, John E., Rajeev Motwani y Jefferey D. Ullman_ [1979] (2007). **Introduction to Automata Theory, Languages, and Computation**. 3.a ed. Pearson Education.

- _Kozen, Dexter C._ [1997] (2012). **Automata and Computability**. Third printing. Undergraduate Texts in Computer Science. Springer. doi: [10.1007/978-1-4612-1844-9](https://doi.org/10.1007/978-1-4612-1844-9)

---

**¡Gracias por leer este post!**
