# Ejercicios Práctica 1

## Sección 1: Lexers y Autómatas (Ejercicios 1-8)

1. Diseñar un autómata finito determinista (AFD) para reconocer identificadores en un lenguaje tipo C.

<font color="red">**Falta**</font>

  > <font color="#6564b3">**Solucion**</font>
  >
  >Sea un AFD `M:(Q,∑,δ,q1,F)` con: 
  >
  >```
  >Q={q1,…,qn};
  >∑={a,…,z,A,…,Z,0,…,9,_};
  >δ={
  >    δ(q1,[a,…,z,A,…,Z,_])=q2
  >    δ(q2,[a,…,z,A,…,Z,0,…,9,_])=q2
  >}
  >q1: estado inicial;
  >F={q2}
	>```
	
2. Transformar un autómata finito no determinista (AFND) en un AFD equivalente.

<font color="yellow">**Revisar**</font>

  > <font color="#6564b3">**Solucion**</font>
  >
  >> **_Ref:_** 3.7.1 Conversión de un AFN a AFD [pagina 152]
  ></br>
  >> https://www.geeksforgeeks.org/theory-of-computation/conversion-from-nfa-to-dfa/
  >
  >Consider the following NFA
  >
  >![Ejercicio 2 - AFND](./assets/e2-1.drawio.svg)
  >
  >Following are the various parameters for NFA. Q = { q0, q1, q2 } ? = ( a, b ) F = { q2 } ? (Transition Function of NFA)
  >
  >| Estado | a | b |
  >|:--|:-------------:|:------:|
  >| q<sub>0</sub> | q<sub>0</sub>,q<sub>1</sub> | q<sub>0</sub> |
  >| q<sub>1</sub> |  | q<sub>2</sub> |
  >| q<sub>2</sub> |  |  |
  >
  >Step 1: Q’ = ? Step 2: Q’ = {q0} Step 3: For each state in Q’, find the states for each input symbol. Currently, state in Q’ is q0, find moves from q0 on input symbol a and b using transition function of NFA and update the transition table of DFA. ?’ (Transition Function of DFA) 
  >
  >| Estado | a | b |
  >|:--|:-------------:|:------:|
  >| q<sub>0</sub> | {q<sub>0</sub>,q<sub>1</sub>} | q<sub>0</sub> |
  >
  >Now { q0, q1 } will be considered as a single state. As its entry is not in Q’, add it to Q’. So Q’ = { q0, { q0, q1 } } Now, moves from state { q0, q1 } on different input symbols are not present in transition table of DFA, we will calculate it like: ?’ ( { q0, q1 }, a ) = ? ( q0, a ) ? ? ( q1, a ) = { q0, q1 } ?’ ( { q0, q1 }, b ) = ? ( q0, b ) ? ? ( q1, b ) = { q0, q2 } Now we will update the transition table of DFA. ?’ (Transition Function of DFA) 
  >
  >| Estado | a | b |
  >|:--|:-------------:|:------:|
  >| q<sub>0</sub> | {q<sub>0</sub>,q<sub>1</sub>} | q<sub>0</sub> |
  >| {q<sub>0</sub>,q<sub>1</sub>} | {q<sub>0</sub>,q<sub>1</sub>} | {q<sub>0</sub>,q<sub>2</sub>} |
  >
  >Now { q0, q2 } will be considered as a single state. As its entry is not in Q’, add it to Q’. So Q’ = { q0, { q0, q1 }, { q0, q2 } } Now, moves from state {q0, q2} on different input symbols are not present in transition table of DFA, we will calculate it like: ?’ ( { q0, q2 }, a ) = ? ( q0, a ) ? ? ( q2, a ) = { q0, q1 } ?’ ( { q0, q2 }, b ) = ? ( q0, b ) ? ? ( q2, b ) = { q0 } Now we will update the transition table of DFA. ?’ (Transition Function of DFA) 
  >
  >| Estado | a | b |
  >|:--|:-------------:|:------:|
  >| q<sub>0</sub> | {q<sub>0</sub>,q<sub>1</sub>} | q<sub>0</sub> |
  >| {q<sub>0</sub>,q<sub>1</sub>} | {q<sub>0</sub>,q<sub>1</sub>} | {q<sub>0</sub>,q<sub>2</sub>} |
  >| {q<sub>0</sub>,q<sub>2</sub>} | {q<sub>0</sub>,q<sub>1</sub>} | q<sub>0</sub> |
  >
  >As there is no new state generated, we are done with the conversion. Final state of DFA will be state which has q2 as its component i.e., { q0, q2 } Following are the various parameters for DFA. Q’ = { q0, { q0, q1 }, { q0, q2 } } ? = ( a, b ) F = { { q0, q2 } } and transition function ?’ as shown above. The final DFA for above NFA has been shown in Figure 2. 
  >
  >![Ejercicio 2 - AFND](./assets/e2-2.drawio.svg)

3. Dado un conjunto de expresiones regulares, generar el AFND correspondiente.

<font color="yellow">**Revisar**</font>

  > <font color="#6564b3">**Solucion**</font>
  >
  >> **_Ref:_** 3.7.4 Construcción de un AFN a partir de una expresión regular [pagina 159]
  ></br>
  >> https://www.geeksforgeeks.org/theory-of-computation/regular-expression-to-nfa/
  >
  >`(a/b)*a`
  >
  >![Ejercicio 3 - AFND](./assets/e3-1.drawio.svg)

<font color="red">**Falta**</font>
4. Implementar un lexer que reconozca números enteros y reales usando expresiones regulares.

	> **_Ref:_** https://www.geeksforgeeks.org/compiler-design/working-of-lexical-analyzer-in-compiler/
	</br>
	> https://www.geeksforgeeks.org/compiler-design/lex-program-to-identify-the-identifier/

5. Construir un autómata para reconocer comentarios estilo C (`/* ... */`) y línea (`//...`).

<font color="yellow">**Revisar**</font>

  > <font color="#6564b3">**Solucion**</font>
  >
  >![Ejercicio 5 - AFD](./assets/e5.drawio.svg)

<font color="red">**Falta**</font>
6. Comparar la eficiencia de un AFD versus un AFND para el mismo lenguaje.

	> **_Ref:_** 3.7.3 Eficiencia de la simulación de un AFN [pagina 157]

<font color="red">**Falta**</font>
7. Diseñar un lexer que distinga entre palabras reservadas e identificadores.

<font color="red">**Falta**</font>
8. Implementar un autómata que reconozca literales de cadena y escape sequences.

---

## Sección 2: Lenguajes Regulares y Normalización de Gramáticas (Ejercicios 9-14)

9. Determinar si el lenguaje definido por la expresión regular `(a|b)*abb` es regular y construir su AFD.

<font color="yellow">**Revisar**</font>

> <font color="#6564b3">**Solucion**</font>
>
> Un lenguaje es regular si puedes:
> * Construir un autómata finito (AFD o AFN) que lo reconozca.
> * O escribir una expresión regular que lo genere.
> * O describirlo con una gramática regular.
> 
> ```
> S → Tabb | abb
> T → a | b | aT | bT
> ```
> 
> ![Ejercicio 5 - AFD](./assets/p1-s2-e9.drawio.svg)

10. Clasificar la gramática `S→aSb∣bSa∣ε` según forma normal de Chomsky.

<font color="yellow">**Revisar**</font>

> <font color="#6564b3">**Solucion**</font>
>
> <table><tr><td style="vertical-align: top;">
> 
> ```
> S → aSb ∣ bSa ∣ ε
> ```
> 
> </td><td></td><td style="vertical-align: top;">
> 
> ⇒
> 
> </td><td></td><td style="vertical-align: top;">
> 
> ```
> S → ASB ∣ BSA ∣ ε  
> A → a  
> B → b
> ```
> 
> </td><td></td><td style="vertical-align: top;">
> 
> ⇒
> 
> </td><td></td><td style="vertical-align: top;">
> 
> ```
> S → AX ∣ BY ∣ ε  
> X → SB
> Y → SA
> A → a  
> B → b
> ```
> 
> </td></tr></table>

11. Simplificar la gramática anterior. Explicar paso a paso

<font color="yellow">**Revisar**</font>

> <font color="#6564b3">**Solucion**</font>
>
> ```
> S → AX ∣ BY ∣ ε  
> X → SB
> Y → SA
> A → a  
> B → b
> ```
> 
> <table><tr><td style="vertical-align: top;">
> 
> **Elim. prod. ε**
> 
> ```
> S → AX ∣ BY
> X → SB | B
> Y → SA | A
> A → a  
> B → b
> ```
> 
> </td><td></td><td style="vertical-align: top;">
> 
> **Elim. prod. Unitarias**  
> 
> ```
> S → AX ∣ BY
> X → SB | b
> Y → SA | a
> A → a  
> B → b
> ```
> 
> </td><td></td><td style="vertical-align: top;">
> 
> **Elim. var. no Positivas**  
> No hay  
> **Elim. var. no Alcanzables**  
> No hay
> 
> </td><td></td><td style="vertical-align: top;">
> 
> **Resultado Final**
> 
> ```
> S → AX ∣ BY
> X → SB | b
> Y → SA | a
> A → a  
> B → b
> ```
> 
> </td></tr></table>

<font color="red">**Falta**</font>
12. Diseñar una gramática regular para reconocer números binarios múltiplos de 3.

<font color="red">**Falta**</font>
13. Dado un lenguaje regular, construir su expresión regular equivalente a partir del AFD.

<font color="red">**Falta**</font>
14. Normalizar la gramática de una mini-lenguaje de expresiones aritméticas a forma normal de Chomsky.

---

## Sección 3: Análisis Sintáctico Descendente (Ejercicios 15-22)

<font color="red">**Falta**</font>
15. Construir un parser descendente recursivo para expresiones aritméticas con operadores `+` y `*`.

	> **_Ref:_** 4.4.1 Análisis sintáctico de descenso recursivo [pagina 219]

<font color="red">**Falta**</font>
16. Eliminar la recursión izquierda de la gramática `E -> E + T | T`.

<font color="red">**Falta**</font>
17. Construir la tabla de predicción para un parser LL(1) de expresiones booleanas.

	> **_Ref:_** 4.4.3 Gramáticas LL(1) [pagina 222]

<font color="red">**Falta**</font>
18. Implementar un parser LL(1) que reconozca declaraciones de variables en un lenguaje tipo Pascal.

<font color="red">**Falta**</font>
19. Determinar si la gramática `S -> aSb | ε` es LL(1) y justificar.

<font color="red">**Falta**</font>
20. Modificar la gramática para que sea apta para un parser descendente predictivo.

<font color="red">**Falta**</font>
21. Implementar un parser recursivo para estructuras condicionales `if-then-else`.

<font color="red">**Falta**</font>
22. Diseñar un parser LL(1) para una pequeña gramática de sentencias repetitivas (`while` loops).

---

## Sección 4: Análisis Sintáctico Ascendente (Ejercicios 23-30)

<font color="red">**Falta**</font>
23. Construir la tabla LR(0) para la gramática `S -> CC, C -> cC | d`.

	> **_Ref:_** 4.6.4 Construcción de tablas de análisis sintáctico SLR [pagina 252]

<font color="red">**Falta**</font>
24. Identificar los conflictos shift/reduce en una gramática y proponer soluciones.

<font color="red">**Falta**</font>
25. Diseñar un parser SLR(1) para un subconjunto de expresiones aritméticas.

<font color="red">**Falta**</font>
26. Construir el autómata de elementos canónicos para un parser LR(1) de expresiones lógicas.

<font color="red">**Falta**</font>
27. Implementar un parser ascendente para declaraciones de variables con tipos `int` y `float`.

<font color="red">**Falta**</font>
28. Analizar una gramática ambigua y generar su versión no ambigua para parsing LR.

<font color="red">**Falta**</font>
29. Implementar un parser LALR(1) para sentencias de asignación y expresiones aritméticas.

<font color="red">**Falta**</font>
30. Comparar la complejidad y ventajas de los parsers descendentes vs ascendentes para un lenguaje pequeño.
