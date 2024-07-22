---
layout: post
title:  "Autómatas finitos no deterministas"
date:   2024-07-29 14:43:00 -0500
categories: autómatas finitos lenguajes regulares
author: Oscar García
---

{% if page.my_variable %}
  {% include {{ page.my_variable }} %}
{% endif %}

## Contenidos
{:.no_toc}

* TOC
{:toc}

---
## Preliminares

### Referencias

Las referencias principales para este artículo son (*Kozen 2012, Lecturas 5 y 6*).

### Convenciones

1. Los números naturales incluyen el cero, es decir, $N = \\{0, 1, 2, \ldots\\}$.
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

> **Definicón:** Un **autómata finito no determinista** (**AFND**) es una estructura
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

> Sea $N = (Q, \Sigma, \Delta, S, F)$ un **AFND**. La **función de transición extendida**, denotada $\hat{\Delta}$, está recursivamente definida por:
>
> $$
> \begin{align*}
>     \hat{\Delta} : 2^Q \times \Sigma^* &\to 2^Q \\
>     \hat{\Delta}(A, \varepsilon) &= A, \\
>     \hat{\Delta}(A, xa) &= \bigcup_{q \in \hat{\Delta}(A, x)} \Delta(q, a).
> \end{align*}
> $$

<blockquote class="green">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse varius enim in eros elementum tristique.</blockquote>

---

## Referencias

- _Hopcroft, John E., Rajeev Motwani y Jefferey D. Ullman_ [1979] (2007). **Introduction to Automata Theory, Languages, and Computation**. 3.a ed. Pearson Education.

- _Kozen, Dexter C._ [1997] (2012). **Automata and Computability**. Third printing. Undergraduate Texts in Computer Science. Springer. doi: [10.1007/978-1-4612-1844-9](https://doi.org/10.1007/978-1-4612-1844-9)

---

**¡Gracias por leer este post!**
