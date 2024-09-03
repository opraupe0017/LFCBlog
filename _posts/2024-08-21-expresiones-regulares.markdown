---
title:  "Expresiones regulares"
date:   2024-08-21 08:25:00 -0500
categories: [Expresiones regulares, Autómatas finitos no deterministas, Lenguajes regulares]
tags: [er, afnd, lr] 
author: ok
---

El contenido de este artículo le pertenece al Profesor **Andrés Sicard Ramírez**[^1], quien me ha permitido compartirlo por este medio.

---
## Preliminares

### Referencias

Las referencias principales para este artículo son (*Kozen 2012, Lecturas 8 y 11*).

### Convenciones

1. Los números naturales incluyen el cero, es decir, $\mathbb{N} = \\{0, 1, 2, \ldots\\}$.
2. El conjunto potencia de un conjunto $A$ es denotado $2^A$.
3. Los términos *definición inductiva* y *definición recursiva* se usan como sinónimos.

---

## Expresiones regulares

- Descripsión algebráica:
  
  $$(01)(01)^\ast + (010)(010)^\ast$$

- Descripsión de una máquina:

  ![img2](/assets/img/0003_afnd.png){: .shadow }

---

## Introducción

- Las expresiones regulares son una especificación algebraica y declarativa para los lenguajes regulares.
- Las expresiones regulares son usadas por ejemplo en comandos de búsqueda para encontrar archivos o contenidos en los mismos, búsquedas robustas en bases de datos, ..., en los generadores de analizadores lexicográficos (p. ej. lex).

---

## Definición de expresión regular

> **Definición:** Las **expresiones regulares** (**er** o **regex**) sobre un alfabeto $\Sigma$ es el conjunto más pequeño definido recursivamente por:
> 1. Paso base:
>    - Si $a \in \Sigma$, entonces $a$ es una expresión regular.
>    - $\varepsilon$ y $\emptyset$ son expresiones regulares.
> 2. Paso recursivo (inductivo): Si $\alpha$ y $\beta$ son expresiones regulares, entonces son expresiones regulares:
>    - $\alpha + \beta$.
>    - $\alpha \cdot \beta$.
>    - $\alpha^\ast$.
>    - $(\alpha)$.
{: .prompt-warning .shadow }

> **Convenciones:** Las expresiones regulares se denotarán por letras griegas minúsculas $\alpha, \beta, \gamma, \ldots$. El operador «$\cdot$» se puede omitir, es decir, $\alpha \beta = \alpha \cdot \beta$.
{: .prompt-info .shadow }

> **Precedencia y asociatividad de los operadores**
> 1. El operador «$\ast$» tiene mayor precedencia que el operador «$\cdot$» que a su vez tiene mayor precedencia que el operador «$+$».
> 2. Los operadores «$\cdot$» y «$+$» son asociativos.

---

## Definición de lenguaje denotado por una expresión regular

> **Definición:** El lenguaje denotado por una expresión regular $\alpha$, denotado $L(\alpha)$, es definido recursivamente por:
> 1. Paso base: Para $a \in \Sigma$
>    - $L(a) = \\{a\\}$.
>    - $L(\varepsilon) = \\{\varepsilon\\}$.
>    - $L(\emptyset) = \emptyset$.
> 2. Paso recursivo (inductivo): Sean $L(\alpha)$ y $L(\beta)$ los lenguajes denotados por las
expresiones regulares $\alpha$ y $\beta$, entonces
>    - $L(\alpha + \beta) = L(\alpha) \cup L(\beta)$.
>    - $L(\alpha \cdot \beta) = L(\alpha) \cdot L(\beta) = L(\alpha) L(\beta)$.
>    - $L(\alpha^\ast) = (L(\alpha))^\ast$.
>    - $L((\alpha)) = L(\alpha)$.
{: .prompt-warning .shadow }

---

## Ejemplo 1.

> | **Expresión regular $\alpha$** | **Lenguaje Generado $L(\alpha)$** |
> |--------------------------------|----------------------------------|
> | $a + b$                        | $L(a) \cup L(b) = \\{a\\} \cup \\{b\\} = \\{a, b\\}$ |
> | $a^\ast$                          | $\\{\epsilon, a, aa, aaa, \dots\\}$ |
> | $(a + b)(a + b)$               | $L(a + b)L(a + b) = \\{a, b\\}\\{a, b\\} = \\{aa, ab, ba, bb\\}$ |
> | $a + (ab)^\ast$                   | $\\{a, \epsilon, ab, abab, ababab, \\dots\\}$ |
> | $(0 + 1)^\ast 01(0 + 1)^\ast$         | $\\{ x01y \mid x, y \\in \\{0, 1\\}^\ast \\}$ |
> | $a_i(a_1 + a_2 + \dots + a_n)^\ast$ | $\\{ x \in \Sigma^\ast \mid x \text{ comienza por } a_i \\}$ |
{: .prompt-info .shadow }

## Ejemplo 2.

> Escribir una expresión regular para el lenguaje definido por
>
> $$L = \{x \in \{a, b\}^\ast \mid \text{$a$ y $b$ están alternadas en $x$}\}.$$
{: .prompt-info .shadow }

<details>
  <summary>Solución 1.</summary>

  $$(ab)^\ast + (ba)^\ast + a(ba)^\ast + b(ab)^\ast.$$
</details>

<details>
  <summary>Solución 2.</summary>

  $$(\varepsilon + b)(ab)^\ast (\varepsilon + a).$$
</details>

## Ejemplo 3.

> La expresión regular
>
> $$(10 + 0)^\ast(\varepsilon + 1)$$
>
> denota el conjunto de palabras de $0$s y $1$s que no tienen dos $1$s adyacentes.
{: .prompt-info .shadow }

---

## Equivalencia entre las expresiones regulares y los autómatas finitos

> **Teorema:**
> 1. Para toda expresión regular $\alpha$ existe un AFND $M$ tal que
>
>    $$L(M) = L(\alpha)$$
> 2. Para todo AFND $M$ existe una expresión regular $\alpha$ tal que
>
>    $$L(M) = L(\alpha)$$
{: .prompt-tip .shadow }

> **Observación:** Dado un lenguaje formal $L$, si existe una expresión regular $\alpha$ tal que
>
> $$L(\alpha) = L,$$
> entonces el lenguaje $L$ es un lenguaje regular.
{: .prompt-danger .shadow }

---

## Limitaciones de los autómatas finitos

### Introducción

1. ¿Es $L_1 = \\{ 0^m1^n \mid m, n \geq 0 \\}$ un lenguaje regular?
   <details>
     <summary>Respuesta</summary>
   
     Sí, $L_1 = L(0^\ast1^\ast)$.
   </details>

2. ¿Es $L_2 = \\{ 0^m1^n \mid m, n \geq 1 \\}$ un lenguaje regular?
   <details>
     <summary>Respuesta</summary>
   
     Sí, $L_2 = L(00^\ast11^\ast)$.
   </details>

3. ¿Es $L_3 = \\{ 0^m1^n \mid m \geq 2, n \geq 4 \\}$ un lenguaje regular?
   <details>
     <summary>Respuesta</summary>
   
     Sí, $L_3 = L(000^\ast11111^\ast)$.
   </details>

4. ¿Es $L_4 = \\{ 0^n1^n \mid n \geq 1 \\}$ un lenguaje regular?
   <details>
     <summary>Respuesta</summary>
   
     No, por lema de bombeo.
   </details>

### Lema de bombeo (The Pumping Lemma)

> **Lema:** Sea $L$ un lenguaje regular. Entonces, $L$ satisface la siguiente propiedad **($P$)**:
>
> Existe $k \in \mathbb{N}$, tal que para todas las palabras $x$, $y$, $z$ con $xyz \in L$ y $\|y\| \geq k$, existen palabras $u$, $v$, $w$ tales que $y = uvw$, $v \neq \epsilon$ y para toda $i \in \mathbb{N}$, $xuv^iwz \in L$.
{: .prompt-tip .shadow }

![img2](/assets/img/0004_lema_bombeo.png)
_Imagen ejemplo del lema de bombeo._

### Contrarecíbroco del lema de bombeo

> **Lema:** Si lenguaje $L$ satisface la siguiente propiedad **($\neg P$)**:
>
> Para todo $k \in \mathbb{N}$, existen las palabras $x$, $y$, $z$ con $xyz \in L$ y $\|y\| \geq k$ y para todas las palabras $u$, $v$, $w$ tales que $y = uvw$ con $v \neq \epsilon$, existe $i \in \mathbb{N}$ tal que $xuv^iwz \notin L$.
> 
> Entonces $L$ no es un lenguaje regular.
{: .prompt-tip .shadow }

### Un juego entre adversarios

El **contrarrecíproco del lema del bombeo** se puede emplear para demostrar que un lenguaje no es regular. La demostración se puede pensar como un juego entre adversarios, en donde usted desea demostrar que un lenguaje $L$ es no regular y su adversario lo contrario.


> **Juego de adversarios:**
>
> 1. Su adversario selecciona $k \in \mathbb{N}$.
> 1. Usted selecciona $x$, $y$, $z$ con $xyz \in L$ y $\|y\| \geq k$.
> 1. Su adversario selecciona $u$, $v$, $w$ tales que $y = uvw$ con $v \neq \epsilon$.
> 1. Usted selecciona $i \in \mathbb{N}$ tal que $xuv^iwz \notin L$.
> 
> Usted gana si $xuv^iwz \notin L$ y su adversario gana de lo contrario.
{: .prompt-info .shadow }

---

## Referencias

- _Hopcroft, John E., Rajeev Motwani y Jefferey D. Ullman_ [1979] (2007). **Introduction to Automata Theory, Languages, and Computation**. 3.a ed. Pearson Education.

- _Kozen, Dexter C._ [1997] (2012). **Automata and Computability**. Third printing. Undergraduate Texts in Computer Science. Springer. doi: [10.1007/978-1-4612-1844-9](https://doi.org/10.1007/978-1-4612-1844-9)

---

[^1]: http://www1.eafit.edu.co/asr/cursos/st0270-lenguajes-formales-y-compiladores/index.html

---

**¡Gracias por leer este post!**
