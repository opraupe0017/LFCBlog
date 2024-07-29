---
title:  "Introducción"
date:   2024-07-11 06:00:00 -0500
categories: [introducción]
---

El contenido de este artículo le pertenece al Profesor [**Andrés Sicard Ramírez**]: http://www1.eafit.edu.co/asr/cursos/st0270-lenguajes-formales-y-compiladores/index.html, quien me ha permitido compartirlo por este medio.

Este artículo tiene como objetivo establecer relaciones entre los modelos de computación, los lenguajes formales, las gramáticas y los compiladores.

## Contenidos
{:.no_toc}

* TOC
{:toc}

---

## Tópicos principales y bibliografía

1. **Teoría de los lenguajes formales:** Definiciones y operaciones básicas (Kozen 2012, Lectura 2).
2. **Lenguajes regulares y autómatas finitos:** (Kozen 2012, Lecturas 3–6, 11).
3. **Lenguajes libres de contexto y autómatas a pila:** (Kozen 2012, Lecturas 19–21, 23, 24).
4. **Máquinas de Turing y clasificación de Chomsky:** (Kozen 2012, Lecturas 28, 29).
5. **Análisis sintáctico descendente:** (Aho et al. 2006, § 4.4.1–4.4.5).
6. **Análisis sintáctico ascendente:** (Aho et al. 2006, § 4.5.1–4.5.5, § 4.6.1–4.6.4, § 4.6.6).
7. **Semántica de traducción y análisis estático:** (Crespi Reghizzi et al. 2019, § 5.1–5.4, § 5.5–5.7).

---

## Abstracción

En relación con la **abstracción**, *Kozen (2012, pág. 5)* escribió:
*Cuando se estudian fenómenos del mundo real, uno se da cuenta de patrones y temas recurrentes que aparecen de diversas formas. Estas formas pueden diferir sustancialmente a un nivel superficial, pero pueden tener suficiente semejanza entre sí como para sugerir que hay principios subyacentes comunes en juego. Cuando esto sucede, tiene sentido intentar construir un modelo abstracto que capture estos principios subyacentes de la manera más simple posible, desprovisto de los detalles no importantes de cada manifestación particular. Este es el proceso de abstracción. La abstracción es la esencia del progreso científico, porque centra la atención en los principios importantes, sin estar cargado de detalles irrelevantes.*

En relación con la **abstracción**, *Aho et al. (2006, pág. 15)* escribieron:
*El diseño de compiladores está lleno de bellos ejemplos donde problemas del mundo real complicados se resuelven al abstraer la esencia del problema matemáticamente. Estos sirven como excelentes ilustraciones de cómo se pueden usar abstracciones para resolver problemas: tomar un problema, formular una abstracción matemática que capture las características clave y resolverlo usando técnicas matemáticas. La formulación del problema debe estar fundamentada en una comprensión sólida de las características de los programas informáticos, y la solución debe ser validada y refinada empíricamente.*

---

## Modelos de computaciónen orden creciente de poder computacional

- **Memoria finita**
  1. **Autómatas finitos** (*McCulloch y Pitts 1943*).
  2. **Expresiones regulares** (*Kleene 1956*).

- **Memoria finita y una pila:** Autómatas a pila (*Oettinger 1961*).

- **Memoria linealmente acotada:** Autómatas linealmente acotados (*Myhill 1960*).

- **Memoria no acotada (infinita)**
  1. **Máquinas de Turing** (*Turing 1936-1937*).
  2. **Cálculo lambda** (*Church 1936*).

**Observación:** Algunos de los modelos anteriores fueron definidos antes de que los computadores fueran creados.

---

## Gramáticas y lenguajes

### Descripción

Una **gramática** es un **meta-lenguaje** para describir lenguajes.

### Acerca de los lenguajes formales

En relación a los **lenguajes formales**, *Crespi Reghizzi et al. (2019, pág. 5)* escribieron:
*Para que un lenguaje sea formalizado (o formal), la forma de sus oraciones (o sintaxis) y su significado (o semántica) deben estar definidos de manera precisa y algorítmica.*

### Jerarquía de Chomsky (1959) para las gramáticas

Las gramáticas en la tabla están en orden creciente de acuerdo a la clase de lenguaje que generan.

| **Tipo de gramática** | **Clase de lenguaje generado**      |
|-----------------------|-------------------------------------|
| 3                     | **Regulares**                       |
| 2                     | **Libres (independientes) de contexto** |
| 1                     | **Dependientes del contexto**       |
| 0                     | **Recursivamente enumerable**       |

## Gramáticas y modelos de computación

### Correspondencia entre las gramáticas y los modelos de computación

Un tipo de gramática genera una clase de lenguajes y un modelo de computación reconoce una clase de lenguajes.

| **Tipo de gramática** | **Clase de lenguaje generado**         | **Modelo de computación**           |
|-----------------------|----------------------------------------|-------------------------------------|
| 3                     | **Regulares**                          | **Autómatas finitos**               |
| 2                     | **Libres (independientes) de contexto**| **Autómatas a pila**                |
| 1                     | **Dependientes del contexto**          | **Autómatas linealmente acotados**  |
| 0                     | **Recursivamente enumerables**         | **Máquinas de Turing**              |

**Observación:** La correspondencia indicada en la tabla es un resultado de la **abstracción**.

---

## Compiladores

### Descripción

Usualmente la **compilación** es la translación de un programa en un lenguaje de programación (lenguaje fuente) en un programa ejecutable en un lenguaje de máquina[^1] (lenguaje destino).

Un **compilador** es un **programa** que realiza una compilación.

### Otros programas requeridos para generar un programa ejecutable

![Figura 1.5 de (Aho et al. 2008)](/assets/img/0001_compilador.png)
_Figura 1.6 de (Aho et al. 2008)_

### Partes de un compilador

Las partes generales de un compilador son la **parte de análisis** (o *front-end*) y la **parte de síntesis** (o *back-end*) (*Aho et al. 2008*, pág. 4):

1. **Parte de análisis**: 
   - *«La parte del análisis divide el programa fuente en componentes e impone una estructura gramatical sobre ellas. Después utiliza esta estructura para crear una representación intermedia del programa fuente... La parte del análisis también recolecta información sobre el programa fuente y la almacena en una estructura de datos llamada tabla de símbolos.»*

2. **Parte de síntesis**:
   - *«La parte de la síntesis construye el programa destino deseado a partir de la representación intermedia y de la información en la tabla de símbolos.»*

### Fases de un compilador

![Figura 1.6 de (Aho et al. 2008)](/assets/img/0002_compilador.png)
_Figura 1.6 de (Aho et al. 2008)_

---

## Referencias

- Aho, Alfred V., Monica S. Lam, Ravi Sethi y Jeffrey D. Ullman [1986] (2006). *Compilers: Principles, Techniques, & Tools*. 2.a ed. Addison-Wesley (vid. págs. 8, 9, 11).
- — [1986] (2008). *Compiladores: Principios, Técnicas y Herramientas*. Trad. por Alfonso Vidal Romero Elizondo. 2.a ed. Pearson Educación (vid. págs. 21, 22, 24).
- Church, Alonzo (1936). «An Unsolvable Problem of Elementary Number Theory». En: *American Journal of Mathematics* 58.2, págs. 345-363. doi: [10.2307/2371045](https://doi.org/10.2307/2371045) (vid. págs. 12, 13).
- Crespi Reghizzi, Stefano, Luca Breveglieri y Angelo Morzenti [2009] (2019). *Formal Languages and Compilation*. 3.a ed. Texts in Computer Science. Springer. doi: [10.1007/978-3-030-04879-2](https://doi.org/10.1007/978-3-030-04879-2) (vid. págs. 8, 9, 14, 15).
- Kleene, Stephen C. (1956). «Representation of Events in Nerve Nets and Finite Automata». En: *Automata Studies*. Ed. por C. E. Shannon y J. McCarthy. Vol. 34. Annals of Mathematics Studies. Princeton University Press, págs. 3-42 (vid. págs. 12, 13).
- Kozen, Dexter C. [1997] (2012). *Automata and Computability*. Third printing. Undergraduate Texts in Computer Science. Springer. doi: [10.1007/978-1-4612-1844-9](https://doi.org/10.1007/978-1-4612-1844-9) (vid. págs. 8-10).
- McCulloch, W. S. y W. Pitts (1943). «A Logical Calculus of The Ideas Immanent in Nervous Activity». En: *Bulletin of Mathematical Biophysics* 5.4, págs. 115-133. doi: [10.1007/BF02478259](https://doi.org/10.1007/BF02478259) (vid. págs. 12, 13).
- Oettinger, Anthony G. (1961). «Automatic Syntactic Analysis and The Pushdown Store». En: *Proc. Symp. App. Math.* Vol. 12, págs. 104-129 (vid. págs. 12, 13).
- Turing, Alan M. (1936-1937). «On Computable Numbers, with an Application to the Entscheidungsproblem». En: *Proceedings of the London Mathematical Society* s2-42, págs. 230-265. doi: [10.1112/plms/s2-42.1.230](https://doi.org/10.1112/plms/s2-42.1.230) (vid. págs. 12, 13).

[^1]: Lenguaje binario que es leído, interpretado y ejecutado por la CPU.

---

**¡Gracias por leer este post!**
