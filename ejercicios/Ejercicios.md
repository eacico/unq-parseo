# Ejercicios Prácticos - Parseo de código

## Sección 1: Lexers y Autómatas (Ejercicios 1-8)

1. <font color="red">**[FALTA]**</font> Diseñar un autómata finito determinista (AFD) para reconocer identificadores en un lenguaje tipo C.

	Sea un AFD `M:(Q,∑,δ,q1,F)` con: 

		Q={q1,…,qn};
		∑={a,…,z,A,…,Z,0,…,9,_};
		δ={
			δ(q1,[a,…,z,A,…,Z,_])=q2
			δ(q2,[a,…,z,A,…,Z,0,…,9,_])=q2
		}
		q1: estado inicial;
		F={q2} 
	
2. <font color="yellow">**[Revisar]**</font> Transformar un autómata finito no determinista (AFND) en un AFD equivalente.

	> **_Ref:_** 3.7.1 Conversión de un AFN a AFD [pagina 152]
	</br>
	> https://www.geeksforgeeks.org/theory-of-computation/conversion-from-nfa-to-dfa/

	Consider the following NFA

	![Ejercicio 2 - AFND](./assets/e2-1.drawio.svg)

	Following are the various parameters for NFA. Q = { q0, q1, q2 } ? = ( a, b ) F = { q2 } ? (Transition Function of NFA)

	| Estado | a | b |
	|:--|:-------------:|:------:|
	| q<sub>0</sub> | q<sub>0</sub>,q<sub>1</sub> | q<sub>0</sub> |
	| q<sub>1</sub> |  | q<sub>2</sub> |
	| q<sub>2</sub> |  |  |
	
	Step 1: Q’ = ? Step 2: Q’ = {q0} Step 3: For each state in Q’, find the states for each input symbol. Currently, state in Q’ is q0, find moves from q0 on input symbol a and b using transition function of NFA and update the transition table of DFA. ?’ (Transition Function of DFA) 

	| Estado | a | b |
	|:--|:-------------:|:------:|
	| q<sub>0</sub> | {q<sub>0</sub>,q<sub>1</sub>} | q<sub>0</sub> |

	Now { q0, q1 } will be considered as a single state. As its entry is not in Q’, add it to Q’. So Q’ = { q0, { q0, q1 } } Now, moves from state { q0, q1 } on different input symbols are not present in transition table of DFA, we will calculate it like: ?’ ( { q0, q1 }, a ) = ? ( q0, a ) ? ? ( q1, a ) = { q0, q1 } ?’ ( { q0, q1 }, b ) = ? ( q0, b ) ? ? ( q1, b ) = { q0, q2 } Now we will update the transition table of DFA. ?’ (Transition Function of DFA) 

	| Estado | a | b |
	|:--|:-------------:|:------:|
	| q<sub>0</sub> | {q<sub>0</sub>,q<sub>1</sub>} | q<sub>0</sub> |
	| {q<sub>0</sub>,q<sub>1</sub>} | {q<sub>0</sub>,q<sub>1</sub>} | {q<sub>0</sub>,q<sub>2</sub>} |

	Now { q0, q2 } will be considered as a single state. As its entry is not in Q’, add it to Q’. So Q’ = { q0, { q0, q1 }, { q0, q2 } } Now, moves from state {q0, q2} on different input symbols are not present in transition table of DFA, we will calculate it like: ?’ ( { q0, q2 }, a ) = ? ( q0, a ) ? ? ( q2, a ) = { q0, q1 } ?’ ( { q0, q2 }, b ) = ? ( q0, b ) ? ? ( q2, b ) = { q0 } Now we will update the transition table of DFA. ?’ (Transition Function of DFA) 

	| Estado | a | b |
	|:--|:-------------:|:------:|
	| q<sub>0</sub> | {q<sub>0</sub>,q<sub>1</sub>} | q<sub>0</sub> |
	| {q<sub>0</sub>,q<sub>1</sub>} | {q<sub>0</sub>,q<sub>1</sub>} | {q<sub>0</sub>,q<sub>2</sub>} |
	| {q<sub>0</sub>,q<sub>2</sub>} | {q<sub>0</sub>,q<sub>1</sub>} | q<sub>0</sub> |

	As there is no new state generated, we are done with the conversion. Final state of DFA will be state which has q2 as its component i.e., { q0, q2 } Following are the various parameters for DFA. Q’ = { q0, { q0, q1 }, { q0, q2 } } ? = ( a, b ) F = { { q0, q2 } } and transition function ?’ as shown above. The final DFA for above NFA has been shown in Figure 2. 

	![Ejercicio 2 - AFND](./assets/e2-2.drawio.svg)

3. <font color="yellow">**[Revisar]**</font> Dado un conjunto de expresiones regulares, generar el AFND correspondiente.

	> **_Ref:_** 3.7.4 Construcción de un AFN a partir de una expresión regular [pagina 159]
	</br>
	> https://www.geeksforgeeks.org/theory-of-computation/regular-expression-to-nfa/

	`(a/b)*a`

	![Ejercicio 3 - AFND](./assets/e3-1.drawio.svg)

4. <font color="red">**[FALTA]**</font> Implementar un lexer que reconozca números enteros y reales usando expresiones regulares.

	> **_Ref:_** https://www.geeksforgeeks.org/compiler-design/working-of-lexical-analyzer-in-compiler/
	</br>
	> https://www.geeksforgeeks.org/compiler-design/lex-program-to-identify-the-identifier/

5. <font color="Yellow">**[Revisar]**</font> Construir un autómata para reconocer comentarios estilo C (`/* ... */`) y línea (`//...`).

	![Ejercicio 5 - AFD](./assets/e5.drawio.svg)

6. <font color="red">**[FALTA]**</font> Comparar la eficiencia de un AFD versus un AFND para el mismo lenguaje.

	> **_Ref:_** 3.7.3 Eficiencia de la simulación de un AFN [pagina 157]

7. <font color="red">**[FALTA]**</font> Diseñar un lexer que distinga entre palabras reservadas e identificadores.

8. <font color="red">**[FALTA]**</font> Implementar un autómata que reconozca literales de cadena y escape sequences.


## Sección 2: Lenguajes Regulares y Normalización de Gramáticas (Ejercicios 9-14)

9. <font color="red">**[FALTA]**</font> Determinar si el lenguaje definido por la expresión regular `(a|b)*abb` es regular y construir su AFD.

	Un lenguaje es regular si puedes:
	* Construir un autómata finito (AFD o AFN) que lo reconozca.
	* O escribir una expresión regular que lo genere.
	* O describirlo con una gramática regular.

10. <font color="red">**[FALTA]**</font> Clasificar la gramática `S→aSb∣bSa∣ε` según forma normal de Chomsky.

	Se dice que una gramática está en Forma Normal de Chomsky (FNC) si toda producción es de la forma A → BC o de la forma A → a, en donde A, B y C son no terminales, y a es un terminal.

11. <font color="red">**[FALTA]**</font> Simplificar la gramática anterior. Explicar paso a paso

	Diapo: file:///C:/Users/CicoNote/Desktop/UNQ/Parseo/Teorico2-Simplificaci%C3%B3n%20de%20gram%C3%A1ticas%20-%20Normalizaci%C3%B3n.pdf
	Pagina 11

12. <font color="red">**[FALTA]**</font> Diseñar una gramática regular para reconocer números binarios múltiplos de 3.

13. <font color="red">**[FALTA]**</font> Dado un lenguaje regular, construir su expresión regular equivalente a partir del AFD.

14. <font color="red">**[FALTA]**</font> Normalizar la gramática de una mini-lenguaje de expresiones aritméticas a forma normal de Chomsky.

## Sección 3: Análisis Sintáctico Descendente (Ejercicios 15-22)

15. <font color="red">**[FALTA]**</font> Construir un parser descendente recursivo para expresiones aritméticas con operadores `+` y `*`.

	> **_Ref:_** 4.4.1 Análisis sintáctico de descenso recursivo [pagina 219]

16. <font color="red">**[FALTA]**</font> Eliminar la recursión izquierda de la gramática `E -> E + T | T`.

17. <font color="red">**[FALTA]**</font> Construir la tabla de predicción para un parser LL(1) de expresiones booleanas.

	> **_Ref:_** 4.4.3 Gramáticas LL(1) [pagina 222]

18. <font color="red">**[FALTA]**</font> Implementar un parser LL(1) que reconozca declaraciones de variables en un lenguaje tipo Pascal.

19. <font color="red">**[FALTA]**</font> Determinar si la gramática `S -> aSb | ε` es LL(1) y justificar.

20. <font color="red">**[FALTA]**</font> Modificar la gramática para que sea apta para un parser descendente predictivo.

21. <font color="red">**[FALTA]**</font> Implementar un parser recursivo para estructuras condicionales `if-then-else`.

22. <font color="red">**[FALTA]**</font> Diseñar un parser LL(1) para una pequeña gramática de sentencias repetitivas (`while` loops).

## Sección 4: Análisis Sintáctico Ascendente (Ejercicios 23-30)

23. <font color="red">**[FALTA]**</font> Construir la tabla LR(0) para la gramática `S -> CC, C -> cC | d`.

	> **_Ref:_** 4.6.4 Construcción de tablas de análisis sintáctico SLR [pagina 252]

24. <font color="red">**[FALTA]**</font> Identificar los conflictos shift/reduce en una gramática y proponer soluciones.

25. <font color="red">**[FALTA]**</font> Diseñar un parser SLR(1) para un subconjunto de expresiones aritméticas.

26. <font color="red">**[FALTA]**</font> Construir el autómata de elementos canónicos para un parser LR(1) de expresiones lógicas.

27. <font color="red">**[FALTA]**</font> Implementar un parser ascendente para declaraciones de variables con tipos `int` y `float`.

28. <font color="red">**[FALTA]**</font> Analizar una gramática ambigua y generar su versión no ambigua para parsing LR.

29. <font color="red">**[FALTA]**</font> Implementar un parser LALR(1) para sentencias de asignación y expresiones aritméticas.

30. <font color="red">**[FALTA]**</font> Comparar la complejidad y ventajas de los parsers descendentes vs ascendentes para un lenguaje pequeño.

***
***
## Ejercicios adicionales

a. Simplificar la siguiente gramatica regular

	S → aaA | aS | E | bA | BD
	A → aaA | D
	B → Bbb | bb
	C → bC | b
	D → Db | aA
	E → aEb | aF
	F → aFb | ɛ

	a.1. Elimino producciones-ɛ

		Las producciones afectadas son:

			E → aEb | aF
			F → aFb | ɛ

		quedando:

			E → aEb | aF | a
			F → aFb | ab

		gramatica parcial:

			S → aaA | aS | E | bA | BD
			A → aaA | D
			B → Bbb | bb
			C → bC | b
			D → Db | aA
			E → aEb | aF | a
			F → aFb | ab
			
	a.2. Elimino producciones unitarias

		Las producciones afectadas son:

			S → E
			A → D

		quedando:

			S → aEb | aF | a
			A → Db | aA

		gramatica parcial:
		
			S → aaA | aS | bA | BD | aEb | aF | a
			A → aaA | Db | aA
			B → Bbb | bb
			C → bC | b
			D → Db | aA
			E → aEb | aF | a
			F → aFb | ab
			
	a.3. Elimino variables NO positivas

		POS = {F,E,C,B,S}

		gramatica parcial:
		
			S → aS | aEb | aF | a
			B → Bbb | bb
			C → bC | b
			E → aEb | aF | a
			F → aFb | ab
			
	a.4. Elimino variables NO alcanzables

		ALC= {S, E, F}

		gramatica final:
		
			S → aS | aEb | aF | a
			E → aEb | aF | a
			F → aFb | ab

b. Usando la gramática del ejemplo CALCULATOR

| | | |
|:--|:--|:--|
| 1. |Program |-> CLASS ID FeatureBlock END |
| 2. |FeatureBlock |-> FEATURE VarDeclList DO StmtList END |
| 3. |VarDeclList |-> VarDecl VarDeclList &#124; ε |
| 4. |VarDecl |-> ID COLON TYPE |
| 5. |StmtList |-> Stmt StmtList | ε |
| 6. |Stmt |-> Assign |
| 7. |Assign |-> ID ASSIGN Expr |
| 8. |Expr |-> NUMBER | ID |


	b.1. Calcular FIRST

	FIRST(Program) = { CLASS }
	FIRST(FeatureBlock) = { FEATURE }
	FIRST(VarDeclList) = { ID, ε }
	FIRST(VarDecl) = { ID }
	FIRST(StmtList) = { ID, ε }
	FIRST(Stmt) = { ID }
	FIRST(Assign) = { ID }
	FIRST(Expr) = { NUMBER, ID }

	b.1. Calcular FOLLOW

	FOLLOW(Program) = { $ } <- porque es el estado inicial
	FOLLOW(FeatureBlock) = { END }
	FOLLOW(VarDeclList) = { DO }
	FOLLOW(VarDecl) = { ID, DO }
	FOLLOW(StmtList) = { END }
	FOLLOW(Stmt) = { ID, END }
	FOLLOW(Assign) = { ID, END }
	FOLLOW(Expr) = { ID, END }


4.4.4. Compute the FIRST and FOLLOW sets for each grammar in Exercise 4.2.2.

1. S -> 0 S 1 | 0 1

	- FIRST(S) = [0]
	- FOLLOW(S) = [1, $]

2. S -> + S S | * S S | a

	- FIRST(S) = [+, *, a]
	- FOLLOW(S) = [+, *, a, $]

3. S -> S (S) S | ε

	- FIRST(S) = [(, ε]
	- FOLLOW(S) = [), $]

4. S -> S + S | S S | (S) | S * | a

	- FIRST(S) = [(, a]
	- FOLLOW(S) = [+, (, ), a, *, $]

5. S -> (L) | a and L -> L, S | S

	- FIRST(S) = [(, a]
	- FOLLOW(S) = [",", $]
	- FIRST(L) = FOLLOW(S) = [(, a]
	- FOLLOW(L) = [), ",", $]

6. S -> a S b S | b S a S | ε

	FIRST(S) = [a, b, ε]
	follow(S) = [a, b, $]

7. The following Boolean expressions correspond to the grammar:

 bexpr -> bexpr or bterm | bterm
 bterm -> bterm and bfactor | bfactor
 bfactor -> not bfactor | (bexpr) | true | false


***
***
## Ejercicios Clase
ejercicio-clase_1-10.pdf

	class CALCULATOR
	feature
		x: INTEGER
		y: INTEGER
		do
			x := 5
			y := x
		end
	end
	
	1.Definir Tokens
		token_class 	→ class
		token_feature 	→ feature
		token_do 		→ do
		token_end 		→ end
		ID 				→ [a-z,A-Z,_]*[a-z,A-Z,0-9,_]
		TYPE 			→ INTEGER | STRING | DOUBLE | BOOL
		token_assign 	→ :=
		token_colon 	→ :
		NUM 			→ [0-9]+
		
	2.Proponer una Gramática Libre de Contexto (GLC)
		tomando los tokens definidos en el punto anterior como base, agrego las reglas de deriacion para los no terminales.
		
		Producciones: {
			Program 		→ <token_class> <ID> <FeatureBlock> <token_end>
			FeatureBlock 	→ <token_feature> <VarDeclList> <token_do> <StmtList> <token_end>
			VarDeclList 	→ <VarDecl> <VarDeclList> | <VarDecl>
			VarDecl 		→ <ID> <token_colon> <TYPE>
			StmtList 		→ <Stmt> <StmtList> | <Stmt>
			Stmt 			→ <Assign>
			Assign 			→ <ID> <token_assign> <Expr>
			Expr 			→ <NUM> | <ID>
		}
		Terminales{ 
			token_class,
			token_feature,
			token_do,
			token_end,
			ID,
			TYPE,
			token_assign,
			token_colon,
			NUM
		}
			
		Not Terminales{
			Program,
			FeatureBlock,
			VarDeclList,
			VarDecl,
			StmtList,
			Stmt,
			Assign,
			Expr
		}

	2.1. Preparar Gramática para Top-Down Parsing (LL(1))
		No se identifian recursiones por izquierda, asi que la gramatica se podria considerar top-down
	
	2.2. Eliminar recursión izquierda si aparece.
		No las hay
		
	2.3. Calcular FIRST y FOLLOW de cada no terminal.
		
		
	2.4. Construir la tabla LL(1).
	
	
	3.Implementar Parser Descendente