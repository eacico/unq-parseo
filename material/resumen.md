# Resumen


## Gramatica ambigüa
	2.2.4 Ambigu¨edad............................................. 47
	Para mostrar que una gramática es ambigua, todo lo que debemos hacer es buscar una cadena de terminales que sea la derivación de más de un árbol de análisis sintáctico.
	Ejemplo 2.5:
		cadena → cadena + cadena | cadena − cadena | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9

							cadena
						/			|  \
			  cadena 		+ cadena
				/  |  \				 |
		cadena - cadena    2
		   |        |
			 9        5

							cadena
						 /   |  \
					cadena -	cadena
						 |			/  |  \
						 9	cadena + cadena
									|        |
									5        2

	4.2.5 Ambigüedad.............................................. 203
	Una gramática ambigua es aquella que produce más de una derivación por la izquierda, o más de una derivación por la derecha para el mismo enunciado.
	4.3.2 Eliminación de la ambigüedad............................ 210
	G(V,L,T,S) si existe algun w(arbol de derivacion) ∊ L(G) con al menos una de los siguientes escenarios:
		2 derivaciones mas a la izquierda distintas
		2 derivaciones mas a la derecha distintas
		2 arboles de derivacion distintos


## Definiciones

**Variables Positiva**
>A \*⇒ w &emsp; A ∊ V &emsp; w ∊ T\*

**Variables Alcanzable**
>S \*⇒ 𝛂A𝛃 &emsp; A ∊ V &emsp; 𝛂,𝛃 ∊ (V ∪ T)\*

**Variables Util**
>S \*⇒ 𝛂A𝛃 \*⇒ w &emsp; A ∊ V &emsp; w ∊ T\* &emsp; 𝛂,𝛃 ∊ (V ∪ T)\*

Notas:
- Util ⟾ Positiva y Alcanzable &emsp; (Pero no al revez)

**Producciones Unitarias**
>A → B &emsp; A, B ∊ V 

**Producciones Epsilon**
>A → ɛ &emsp; A ∊ V 

**Variables Nullables**
>A \*⇒ ɛ &emsp; A ∊ V

## Gramatica Simplificada
	es una gramatica G=(V,T,P,S) donde:
		- todas sus variables son Utiles
			S *=> αAβ *=> w    A ∊ V    w ∊ T*    α,β ∊ (V ∪ T*)
		- no tiene producciones Unitarias
			A -> B
		- no tiene producciones epsilon
			A -> ε
	Para simplificar
		(1) Eliminacion de producciones epsilon
		(2) eliminacion de producciones Unitarias
		(3) Obtencion de valiables Positivas
			A *=> w    A ∊ V    w ∊ T*
		(4) Obtencion de valiables Alcanzables
			S *=> αAβ    A ∊ V    α,β ∊ (V ∪ T*)

## Teorema General de Simplificacion


## Forma Normal de Chomsky (FNC)
	Se dice que una gramática está en Forma Normal de Chomsky (FNC) si toda producción es de la forma A → BC o de la forma A → a, en donde A, B y C son no terminales, y a es un terminal.
		A → BC
		A → a
	Ejemplo:
		S → AB
		A → 0
		B → 1 | SC
		C → 1

## Forma Normal de Greibach (FNG)
		A → α
	Ejemplo:
		S → 0SB
		S → 0B
		B → 1
		

## FIRST FOLLOW
	4.4.2 PRIMERO y SIGUIENTE [pagina 220]
	FIRST
	FOLLOW
		1. Si S es estado inicial agrego $ a FOLLOW(S)
		2. B -> αAβ
			FOLLOW(A) = FIRST(β)
		3. B -> αA  o  B -> αAβ y β *=> ε
			FOLLOW(A) = FOLLOW(B)
			

## Armar tabla LL(1)
	Sea una producción A → α
		Si FIRST(α) = {a}:
			M[A, a] = A → α
		Si ε ∊ FIRST(α), busco FOLLOW(A) = {b}:
			M[A, b] = A → α
		Si en algún momento intentas poner dos producciones distintas en la misma celda M[A, t], tienes conflicto → la gramática no es LL(1).


## Bottom-Up

## LR(0)

## Construcción de la tabla ACTION/GOTO

## Intérpretes (store passing y evaluación)

## Generación de Código Intermedio

## Tipos e Inferencia (Algoritmo , unificación)

## Análisis de Flujo de Datos (CFG y Reaching Definitions)
