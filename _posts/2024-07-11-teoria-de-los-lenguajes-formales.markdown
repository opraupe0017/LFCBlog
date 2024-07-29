---
title:  "Teoría de los lenguajes formales"
date:   2024-07-11 20:00:00 -0500
categories: [Lenguajes-formales]
tags: [lf]
author: ok
---

El contenido de este artículo le pertenece al Profesor **Andrés Sicard Ramírez**[^1], quien me ha permitido compartirlo por este medio.

## Preliminares

### Referencia
La referencia principal para este artículo es _Kozen (2012, Lectura 2)_.

### Convenciones
1. Los números naturales incluyen el cero, es decir, $ \mathbb{N} = \\{0, 1, 2, \ldots\\} $.
2. El conjunto potencia de un conjunto $ A $ es denotado $ 2^A $.
3. Los términos **definición inductiva** y **definición recursiva** se usan como sinónimos.

---

## Problemas de decisión

Un **problema de decisión** sobre un conjunto $ A $ (el dominio del problema) es una función

$$ f : A \to \{0, 1\} .$$

**Observación:** Usualmente solo será necesario considerar los problemas de decisión.

---

## Definición del alfabeto $\Sigma$, símbolo $a$, cadena $x$ y cadena vacía $\varepsilon$

- **Alfabeto:** Un alfabeto es un conjunto **finito**, no vacío, de símbolos (letras) indivisibles.
- **Cadena:** Una cadena (palabra) es una secuencia **finita** de símbolos de un alfabeto.
- **Cadena vacía:** La cadena vacía, denotada $\varepsilon$, es la cadena con cero ocurrencias de símbolos.

### Convenciones
- Los alfabetos se denotarán por $\Sigma$ y $\Gamma$.
- Los símbolos se denotarán por las primeras letras minúsculas $a, b, c, \ldots$
- Las cadenas se denotarán por las últimas letras minúsculas $w, x, y, z, \ldots$

---

## Definición del conjunto de todas las cadenas: $\Sigma^\ast$

El **conjunto de todas las cadenas** (incluyendo la palabra vacía) sobre un alfabeto $\Sigma$ es denotado $\Sigma^\ast$. Este conjunto puede ser inductivamente definido por:
- **Paso base:** $\varepsilon \in \Sigma^\ast$,
- **Paso inductivo:** Si $x \in \Sigma^\ast$ y $a \in \Sigma$ entonces $xa \in \Sigma^\ast$.

---

## Definición de lenguaje

Un **lenguaje** sobre un alfabeto $\Sigma$ es cualquier subconjunto de $\Sigma^*$.

**Observaciones**

- El conjunto de todos los lenguajes es $2^{\Sigma^\ast}$.
- *Kozen (2012) no define el término «lenguaje» explícitamente. En su lugar el texto habla de conjuntos.*
- **Note que** $\emptyset \neq \\{\varepsilon\\} \neq \varepsilon$.

---

## Definición longitud de una cadena: $\|x\|$

La **longitud de una cadena** $x$ sobre un alfabeto $\Sigma$, denotada $\|x\|$, es el número de símbolos en $x$. Esta función es definida recursivamente por:

- $\|\varepsilon\| = 0$
- $\|xa\| = 1 + \|x\|$, para toda $a \in \Sigma$ y $x \in \Sigma^*$.

<!-- $$
\begin{align*}
| \cdot | &: \Sigma^* \rightarrow \mathbb{N} \\
|\varepsilon| & \overset{\text{def}}{=} 0, \\
|xa| & \overset{\text{def}}{=} 1 + |x|.
\end{align*}
$$ -->

---

## Definición $a^n$ ($n$ potencia de $a$)

Sea $a$ un símbolo de un alfabeto $\Sigma$. Las **potencias de** $a$, para $n \geq 0$, denotadas $a^n$, es la palabra formada por $n$ repeticiones del símbolo $a$. Esta operación es definida recursivamente por:

- $a^0 = \varepsilon$
- $a^{n+1} = a^n a$.

---

## Definición concatenación $xy$

Sean $x$ y $y$ dos palabras sobre un alfabeto $\Sigma$. La **concatenación de** $x$ **y** $y$, denotada $xy$ o $x\cdot y$, es la palabra que se obtiene al yuxtaponer $y$ después de $x$. Esta operación es definida recursivamente por:

- $x\cdot \varepsilon = x \varepsilon = x$
- $x\cdot (ya) = (x \cdot y)a = xya$.

En general, si $x = a_1a_2\cdots a_n$ y $y = b_1b_2\cdots b_m$ donde $a_i, b_j \in \Sigma$ para $i = 1, 2, \ldots, n$ y $j = 1, 2, \ldots, m$, entonces

$$xy = a_1a_2\cdots a_nb_1b_2\cdots b_m.$$

---

## Algunas propiedades de la concatenación

Sean $x,y,z \in \Sigma^\ast$ cadenas.

1. La **concatenación es asociativa**, es decir,

   $$x(yz) = (xy)z = xyz.$$

2. La **cadena vacía** es el **elemento neutro** para la concatenación, es decir,

   $$x\varepsilon = \varepsilon x = x.$$

3. La **concatenación no es conmutativa**, es decir

   $$xy \neq yx.$$

4. $\|xy\| = \|x\| + \|y\|$.

---

## Definición operaciones entre lenguajes $\cup$, $\cap$, $\sim$, $\cdot$. $\ast$ y $+$

Sean $L$, $L_1$ y $L_2$ lenguajes sobre un alfabeto $\Sigma$.

1. **Unión de lenguajes**:
    
    $$
    L_1 \cup L_2 = \{ x \mid x \in L_1 \text{ o } x \in L_2 \}.
    $$

2. **Intersección de lenguajes**:
    
    $$
    L_1 \cap L_2 = \{ x \mid x \in L_1 \text{ y } x \in L_2 \}.
    $$

3. **Complemento de un lenguaje**:
    
    $$
    \sim L = \{ x \in \Sigma^* \mid x \notin L \}.
    $$

4. **Concatenación de lenguajes**:
    
    $$
    L_1 \cdot L_2 = L_1L_2 = \{ xy \mid x \in L_1 \text{ y } y \in L_2 \}.
    $$

5. **Potencias de un lenguaje**, para $n \ge 0$:

   $$
   \begin{align*}
   L^0 &= \{ \varepsilon \} \\
   L^{n+1} &= L L^n.
   \end{align*}
   $$

6. **Clausura de Kleene** de un lenguaje es la unión de las potencias finitas del lenguaje:
    
    $$
    L^\ast = \bigcup_{n \ge 0} L^n.
    $$

7. **Clausura positiva de Kleene** de un lenguaje es la unión de las potencias positivas del lenguaje:
    
    $$
    L^+ = L L^\ast = \bigcup_{n \ge 1} L^n.
    $$

---

## Algunas propiedades de las operaciones entre lenguajes

1. Dado que los lenguajes son conjuntos, las operaciones de unión e intersección sobre lenguajes son **asociativas**, **conmutativas** y cada una distribuye sobre la otra. Además, satisfacen las **leyes de De Morgan** y el lenguaje $\emptyset$ es la **identidad para la unión**.

2. El lenguaje $\\{\varepsilon\\}$ es la **identidad para la concatenación**, es decir,

   $$L \{\varepsilon\} = \{\varepsilon\} L = L.$$

3. El lenguaje $\emptyset$ es el **aniquilador para la concatenación**, es decir,

   $$L \emptyset = \emptyset L = \emptyset.$$

4. **Propiedades de la clausura de Kleene**:

   $$
   \begin{align*}
   L^\ast L^\ast &= L^\ast, \\
   (L^\ast)^\ast &= L^\ast, \\
   L^\ast &= L^+ \cup \{\varepsilon\}, \\
   \emptyset^\ast &= \{\varepsilon\}.
   \end{align*}
   $$

---

## Referencias

- Kozen, Dexter C. [1997] (2012). *Automata and Computability*. Third printing. Undergraduate Texts in Computer Science. Springer. doi: 10.1007/978-1-4612-1844-9.

---

[^1]: http://www1.eafit.edu.co/asr/cursos/st0270-lenguajes-formales-y-compiladores/index.html

---

**¡Gracias por leer este post!**
