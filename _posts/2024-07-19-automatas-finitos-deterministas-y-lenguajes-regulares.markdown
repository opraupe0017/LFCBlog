---
title:  "Autómatas finitos deterministas y lenguajes regulares"
date:   2024-07-19 14:43:00 -0500
categories: [Autómatas finitos deterministas, Lenguajes regulares]
tags: [afd, lr]
author: ok
---

El contenido de este artículo le pertenece al Profesor **Andrés Sicard Ramírez**[^1], quien me ha permitido compartirlo por este medio.

---
## Preliminares

### Referencias

Las referencias principales para este artículo son (*Kozen 2012, Lecturas 3 y 4*).

### Convenciones

1. Los números naturales incluyen el cero, es decir, $\mathbb{N} = \\{0, 1, 2, \ldots\\}$.
2. El conjunto potencia de un conjunto $A$ es denotado $2^A$.
3. Los términos *definición inductiva* y *definición recursiva* se usan como sinónimos.

---
## Descripción informal de autómatas finitos

> - *Un **estado de un sistema** es una descripción instantánea de ese sistema, una captura de la realidad congelada en el tiempo. Un estado proporciona toda la información relevante necesaria para determinar cómo el sistema puede evolucionar a partir de ese punto. Las **transiciones** son cambios de estado; pueden ocurrir espontáneamente o en respuesta a entradas externas.* (*Kozen 2012, pág. 14*)
{: .prompt-info }

> - *El **autómata finito** es un modelo matemático de un sistema, con entradas y salidas discretas. El sistema puede estar en cualquiera de un número finito de configuraciones internas o **"estados"**. El estado del sistema resume la información concerniente a entradas pasadas que es necesaria para determinar el comportamiento del sistema en entradas subsecuentes.* (*Hopcroft y Ullman 1979, p. 13*)
{: .prompt-info }

---
## Definición de autómata finito determinista (AFD)

> **Definición:** Un **autómata finito determinista** (**AFD**) es una estructura
> 
> $$M = (Q, \Sigma, \delta, s, F),$$
> 
> donde:
> 
> - $Q$ es un conjunto finito, los **estados**.
> - $\Sigma$ es un conjunto finito, el **alfabeto de entrada**.
> - $\delta : Q \times \Sigma \to Q$, la **función de transición**.
> - $s \in Q$, el **estado inicial**.
> - $F \subseteq Q$, el conjunto de **estados finales**.
{: .prompt-warning }

---
## Representaciones del AFD

Los AFDs se pueden representar de varias formas equivalentes:

- **Listando cada una de sus partes:** Consiste en describir $ Q, \Sigma $, los pares ordenados de la función de transición $ \delta $, $ s $ y $ F $.
- **Diagrama de transición:** Un diagrama que muestra los estados como nodos y las transiciones como aristas dirigidas etiquetadas con los símbolos del alfabeto de entrada.
- **Tabla de transición:** Una tabla donde las filas representan los estados y las columnas representan los símbolos del alfabeto de entrada, y cada celda indica el estado resultante de aplicar la función de transición a un estado y un símbolo dados. Se indica con $\to$ el estado inicial y con $F$ todos los estados finales.

### Ejemplo 1

Para el siguiente AFD representado listando cada una de sus partes, encontrar las otras dos representaciones si es posible: $M = (Q, \Sigma, \delta, s, F)$

$$
\begin{align*}
    Q &= \{0, 1, 2, 3\} \\
    \Sigma &= \{a, b\} \\
    \delta(0, a) &= 1 \\
    \delta(1, a) &= 2 \\
    \delta(2, a) &= 3 \\
    \delta(3, a) &= 3 \\
    \delta(q, b) &= q \quad \text{para todo } q \in Q \\
    s &= 0 \\
    F &= \{3\}
\end{align*}
$$

**Observación:** Siempre es posible representar un AFD de las $3$ formas.

---
## Definición función de transición extendida para AFDs: $\hat{\delta}$

> **Definición:** Sea $M = (Q, \Sigma, \delta, s, F)$ un AFD. La **función de transición extendida**[^1], denotada $\hat{\delta}$, es recursivamente definida por:
> 
> $$
> \begin{align}
    \hat{\delta} : Q \times \Sigma^* &\to Q \\
    \hat{\delta}(q, \varepsilon) &= q, \\
    \hat{\delta}(q, xa) &= \delta(\hat{\delta}(q, x), a).
\end{align}
$$
{: .prompt-warning }

### Ejemplo 2.

Para el AFD del ejemplo de [más arriba](#ejemplo-1) $M = (Q, \Sigma, \delta, s, F)$ así se consumiría la cadena de entrada $baa$ a través de la función de transición extendida $\hat{\delta}$:

$$
\begin{align}
    \hat{\delta}(0, baa) &= \hat{\delta}(0, \varepsilon baa) \\
    &= \delta(\hat{\delta}(0, \varepsilon ba), a) \\
    &= \delta(\delta(\hat{\delta}(0, \varepsilon b), a), a) \\
    &= \delta(\delta(\delta(\hat{\delta}(0, \varepsilon), b), a), a) \\
    &= \delta(\delta(\delta(0, b), a), a) \\
    &= \delta(\delta(0, a), a) \\
    &= \delta(1, a) \\
    &= 2 \notin F
\end{align}
$$

> **Pregunta:** ¿Porqué $2 \notin F$?
{: .prompt-danger }

---
## Definición de lenguaje aceptado por los AFDs: $L(M)$

> **Definición:** Sea $M = (Q, \Sigma, \delta, s, F)$ un AFD y sea $x \in \Sigma^*$.
> 
> 1. La palabra $x$ es **aceptada** por el autómata $M$ sí y sólo sí $\hat{\delta}(s, x) \in F$.
> 
> 1. La palabra $x$ es **rechazada** por el autómata $M$ sí y sólo sí $\hat{\delta}(s, x) \notin F$.
> 
> 1. El **lenguaje aceptado** por el autómata $M$, denotado $L(M)$, es el *conjunto de palabras aceptadas* por $M$, es decir,
> 
> $$
> L(M) = \{ x \in \Sigma^\ast \mid \hat{\delta}(s, x) \in F \}.
> $$
{: .prompt-warning }

> **Pregunta:** ¿Cuál es el lenguaje de aceptación del ejemplo de [más arriba](#ejemplo-1)?
{: .prompt-danger }

---
## Definición Lenguajes regulares (LRs)

> **Definición:** Un lenguaje $L$ es un **lenguaje regular** (**LR**) si existe un AFD $M$ tal que
> 
> $$L = L(M).$$
{: .prompt-warning }

> **Observación:** Kozen (2012) no habla de «lenguajes regulares» sino de «conjuntos regulares».
{: .prompt-info }

### Actividad 1

1. Sea $L$ el lenguaje comformado por palabras sobre $\{a, b\}$ que tienen un número par de $a$es y tienen un número par de $b$es. Demostrar que el lenguaje $L$ es un lenguaje regular.
1. Dado un alfabeto $\Sigma$ ¿El conjunto $\Sigma^\ast$ es un lenguaje regular?
1. ¿$\emptyset$ es lenguaje regular?

---
## Propiedades de clausura sobre los lenguajes regulares

Resulta que para dos lenguajes regulares $L_1$ y $L_2$ se cumple la **propiedad de clausura** sobre las operaciones $\sim$, $\cap$ y $\cup$, es decir, los siguientes lenguajes son **lenguajes regulares**:

$$
\begin{align}
\sim &L_1 \\
L_1 &\cap L_2 \\
L_1 &\cup L_2
\end{align}
$$

Recordemos que una **propiedad de clausura** es una propiedad que indica que un *conjunto es cerrado* bajo ciertas operaciones, es decir, al aplicar estas operaciones sobre los elementos del conjunto, *el resultado es también pertenece al conjunto (no se sale)*.

**Ejemplo:** Dados los números complejos

$$
\begin{align}
z_1 &= 3 + 4i\\
z_2 &= 1 + 2i.
\end{align}
$$

Como se cumple la cerradura del producto en el conjunto de números complejos, entonces en particular

$$
\begin{align}
z_1 \cdot z_2 &= (3 + 4i)(1 + 2i) \\
&= 3 \cdot 1 + 3 \cdot 2i + 4i \cdot 1 + 4i \cdot 2i \\
&= 3 + 6i + 4i - 8 \\
&= -5 + 10i
\end{align}
$$

también es un número complejo.

---
### Teorema clausura del complemento de un lenguaje regular

> **Teorema:** Dado un lenguaje $L$. Si $L$ es un **lenguaje regular**, entonces
>
> $$\sim L$$
>
> también es un **lenguaje regular**.
{: .prompt-tip }

> **Observación:** La demostración de esta propiedad es muy sencilla. Solo basta con hacer una ligera modificación a un AFD...
{: .prompt-info }

---

### Teorema clausura de la intersección de lenguajes regulares

> **Teorema:** Dados los lenguajes $L_1$ y $L_2$. Si $L_1$ y $L_2$ son **lenguajes regulares**, entonces 
>
> $$L_1 \cap L_2$$
>
> también es un **lenguaje regular**.
{: .prompt-tip }

> **Observación:** Para demostrar que $L_1 \cap L_2$ es un **lenguaje regular**, construiremos un autómata $M_3$ tal que
>
> $$L(M_3) = L_1 \cap L_2.$$
>
> Se usan dos resultados preliminares[^2].
{: .prompt-info }

### Definición AFD producto

> **Definición:** Supongamos que $L_1$ y $L_2$ son lenguajes regulares. Entonces existen autómatas
> 
> $$
\begin{align}
M_1 &= (Q_1, \Sigma, \delta_1, s_1, F_1) \\
M_2 &= (Q_2, \Sigma, \delta_2, s_2, F_2) 
\end{align}
> $$
> 
> tal que $L(M_1) = L_1$ y $L(M_2) = L_2$. Sea
> 
> $$M_3 = (Q_3, \Sigma, \delta_3, s_3, F_3),$$
> 
> donde[^3]
> 
> $$
\begin{align}
Q_3 &= Q_1 \times Q_2 \\
F_3 &= F_1 \times F_2 \\
s_3 &= (s_1, s_2)
\end{align}
> $$
> 
> y sea la función de transición
> 
> $$
\begin{align}
\delta_3: Q_3 \times \Sigma &\to Q_3 \\
\delta_3((p, q), a) &= (\delta_1(p, a), \delta_2(q, a)).
\end{align}
> $$
> 
> El AFD $M_3$ se llama el **AFD producto** de $M_1$ y $M_2$.
{: .prompt-warning }

De acuerdo a la definición de función de transición extendida aplicada a $\delta_3$, esto da:

$$
\begin{align}
    \hat{\delta}_3 : Q_3 \times \Sigma^* &\to Q_3 \\
    \hat{\delta}_3((p, q), \epsilon) &= (p, q), \\
    \hat{\delta}_3((p, q), xa) &= \delta_3(\hat{\delta}_3((p, q), x), a).
\end{align}
$$

### Lema sobre el AFD producto

> **Lema:** Dado un AFD producto $M_3$ como el construido [más arriba](#definición-afd-producto). Para todo $x \in \Sigma^*$, $p \in Q_1$ y $q \in Q_2$ se tiene que
> 
> $$
\hat{\delta}_3((p, q), x) = (\hat{\delta}_1(p, x), \hat{\delta}_2(q, x)).
$$
{: .prompt-tip }

> **Observación:** La demostración se hace por inducción sobre $\|x\|$.
{: .prompt-info }

### Teorema sobre el AFD producto

> **Teorema:** Dado un AFD producto $M_3$ como el construido [más arriba](#definición-afd-producto). Se tiene que
> 
> $$
L(M_3) = L(M_1) \cap L(M_2).
$$
{: .prompt-tip }

> **Observación:** La demostración se hace por directa por equivalencias empezando con $x \in L(M_3)$ para todo $x \in \Sigma^\ast$.
{: .prompt-info }

> **Pregunta:** ¿Cómo demuestro el [teorema de la clausura de la intersección de lenguajes regulares](#teorema-clausura-de-la-intersección-de-lenguajes-regulares) con este último [teorema](#teorema-sobre-el-afd-producto)?
{: .prompt-danger }

---

### Teorema clausura de la unión de lenguajes regulares

> **Teorema:** Dados los lenguajes $L_1$ y $L_2$. Si $L_1$ y $L_2$ son **lenguajes regulares**, entonces 
>
> $$L_1 \cup L_2$$
>
> también es un **lenguaje regular**.
{: .prompt-tip }

> **Pregunta:** ¿Cómo demuestro este teorema utilizando los teoremas de clausura de las operaciones [complemento](#teorema-clausura-del-complemento-de-un-lenguaje-regular) e [intersección](#teorema-clausura-de-la-intersección-de-lenguajes-regulares) sobre lenguajes regulares?
{: .prompt-danger }

---

## Referencias

- _Hopcroft, John E., Rajeev Motwani y Jefferey D. Ullman_ [1979] (2007). **Introduction to Automata Theory, Languages, and Computation**. 3.a ed. Pearson Education.

- _Kozen, Dexter C._ [1997] (2012). **Automata and Computability**. Third printing. Undergraduate Texts in Computer Science. Springer. doi: [10.1007/978-1-4612-1844-9](https://doi.org/10.1007/978-1-4612-1844-9)

---

[^1]: _El nombre «extended transition function» es tomado de (Hopcroft, Motwani et al. 2007)._
[^2]: _Construcción producto, Lema 4.1 y Teorema 4.2 del libro de Kozen._
[^3]: _Para dos conjuntos $A$ y $B$, el conjunto producto cartesiano es $A \times B = \\{(x, y) \mid x \in A \text{ y } y \in B\\}$._
[^4]: http://www1.eafit.edu.co/asr/cursos/st0270-lenguajes-formales-y-compiladores/index.html

**¡Gracias por leer este post!**
