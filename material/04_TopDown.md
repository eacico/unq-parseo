# Top Down

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

