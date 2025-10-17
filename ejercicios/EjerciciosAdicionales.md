# Ejercicios Adicionales - Parseo de código

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