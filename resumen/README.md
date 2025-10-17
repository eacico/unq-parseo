# Resumen


## Gramatica ambigua: 
	G(V,L,T,S) si existe algun w(arbol de derivacion) ∊ L(G) con al menos una de los siguientes escenarios:
		2 derivaciones mas a la izquierda distintas
		2 derivaciones mas a la derecha distintas
		2 arboles de derivacion distintos

## Gramatica Simplificada
	es una gramatica G=(V,T,P,S) donde:
		- todas sus variables son Utiles
			S *=> αAβ *=> w    A \ib V    w ∊ T*    α,β ∊ (V ∪ T*)
		- no tiene producciones Unitarias
			A -> B
		- no tiene producciones epsilon
			A -> ε
	Para simplificar
		(1) Eliminacion de producciones epsilon
		(2) eliminacion de producciones Unitarias
		(3) Obtencion de valiables Positivas
			A *=> w    A \ib V    w ∊ T*
		(4) Obtencion de valiables Alcanzables
			S *=> αAβ    A \ib V    α,β ∊ (V ∪ T*)



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
