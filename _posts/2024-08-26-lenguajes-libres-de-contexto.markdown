---
title:  "Lenguajes libres de contexto"
date:   2024-08-26 08:25:00 -0500
categories: [Gramáticas libres de contexto, Lenguajes libres de contexto]
tags: [glc, llc] 
author: ok
---

El contenido de este artículo le pertenece al Profesor **Andrés Sicard Ramírez**[^1], quien me ha permitido compartirlo por este medio.

---
## Preliminares

### Referencias

Las referencias principales para este artículo son (*Kozen 2012, Lecturas 19 y 21*).

### Convenciones

1. Los números naturales incluyen el cero, es decir, $\mathbb{N} = \\{0, 1, 2, \ldots\\}$.
2. El conjunto potencia de un conjunto $A$ es denotado $2^A$.
3. Los términos *definición inductiva* y *definición recursiva* se usan como sinónimos.

---

## Definición de gramática libre de contexto (GLC)

> **Definición:** Una **gramática libre de contexto** (**GLC**), es una estructura
>
> $$G = (N, \Sigma, P, S),$$
>
>donde:
> 
> 1. $N$ es un conjunto <span style="color:red;">finito</span> (los símbolos no terminales).
> 2. $\Sigma$ es un conjunto <span style="color:red;">finito</span> (los símbolos terminales); los conjuntos $\Sigma$ y $N$ son disjuntos.
> 3. $P$ es un subconjunto <span style="color:red;">finito</span> de $N \times (N \cup \Sigma)^\ast$ (las producciones).
> 4. $S \in N$ (el símbolo inicial).
{: .prompt-warning .shadow }

> **Convenciones:**
> 
> - Los **símbolos no terminales** serán denotados con letras mayúsculas: $A$, $B$, $C$, $\dots$.
> - Los **símbolos terminales** serán denotados con letras minúsculas: $a$, $b$, $c$, $\dots$.
> - Las **cadenas** en $(N \cup \Sigma)^\ast$ serán denotadas por letras griegas minúsculas: $\alpha$, $\beta$, $\delta$, $\dots$.
> - Las **producciones** serán escritas como $A \to \alpha$ en lugar de $(A, \alpha)$.
> - La **barra vertical** « $\mid$ » significa la disyunción « $o$ ».
> - Las **gramáticas libres de contexto** serán llamadas **gramáticas** o **GLC**.
{: .prompt-info .shadow }

---

## Definición de derivación $\ \xrightarrow[G]{1}$

> **Definición:** Sea $G = (N, \Sigma, P, S)$ una **gramática**. La **relación derivable en un paso**, denotada $\ \xrightarrow[G]{1}$ , es una relación binaria sobre $(N \cup \Sigma)^\ast$, definida por:
> 
> Para toda $\alpha, \beta \in (N \cup \Sigma)^\ast$
> 
> $$\alpha \xrightarrow[G]{1} \beta$$
>
> **si y solo si** existen cadenas $\alpha_1, \alpha_2 \in (N \cup \Sigma)^\ast$ y una producción $A \to \gamma \in P$, tales que
>
> $$\alpha = \alpha_1 A \alpha_2 \quad \text{y} \quad \beta = \alpha_1 \gamma \alpha_2.$$
{: .prompt-warning .shadow }

> **Observaciónes:**
> 1. $\alpha \xrightarrow[G]{1} \beta$ significa que existe una producción $A \to \gamma \in P$ tal que podemos producir a $\beta$ desde $\alpha$ sólo con aplicar la producción $A \to \gamma$ en $\alpha$.
> 2. Si $\alpha \xrightarrow[G]{1} \beta$, decimos que $\beta$ es derivable de $\alpha$ en **un solo paso**.
{: .prompt-danger .shadow }

---

## Definición de clausura reflexivo-transitiva de $\ \xrightarrow[G]{\ast}$

> **Definición:** Sea $G = (N, \Sigma, P, S)$ una **gramática**. La **relación derivable en $n$ pasos**, denotada $\ \xrightarrow[G]{n}$ , es una relación binaria sobre $(N \cup \Sigma)^\ast$, definida por:
> 
> Para toda $\alpha, \beta \in (N \cup \Sigma)^\ast$
> 
> - $\alpha \xrightarrow[G]{0} \alpha$.
> - $\alpha \xrightarrow[G]{n+1} \beta$ si existe un $\delta$ tal que $\alpha \xrightarrow{n}_G \delta$ y $\delta \xrightarrow[G]{1} \beta$.
> - $\alpha \xrightarrow[G]{\ast} \beta$ si $\alpha \xrightarrow[G]{n} \beta$ para algún $n \geq 0$.
{: .prompt-warning .shadow }

---

## Lenguaje generado por una gramática libre de contexto $L(G)$

> **Definición:** Sea $G = (N,\Sigma,P,S)$ una gramática.
> 
> - Una cadena $\alpha \in (N \cup \Sigma)^\ast$ derivable del símbolo inicial $S$ es llamada una **forma sentencial**.
> 
> - Una forma sentencial $x$ es llamada una **sentencia** si esta solo consiste de símbolos terminales, es decir, $x \in \Sigma^\ast$.
> 
> - El **lenguaje generado** por $G$, denotado por $L(G)$, es el conjunto de todas las sentencias:
> 
> $$
> L(G) = \left\lbrace x \in \Sigma^* \biggm| S \xrightarrow[G]{*} x \right\rbrace
> $$
{: .prompt-warning .shadow }

## Definición de lenguaje libre de contexto (LLC)

> **Definición:** Sea $\Sigma$ un alfabeto y $L \subseteq \Sigma^\ast$ un lenguaje. Se dice que $L$ es un **lenguaje libre de contexto** (**LLC**) si existe una gramática $G$ tal que
>
> $$L = L(G).$$
>
{: .prompt-warning .shadow }

---

[^1]: http://www1.eafit.edu.co/asr/cursos/st0270-lenguajes-formales-y-compiladores/index.html

---

**¡Gracias por leer este post!**
