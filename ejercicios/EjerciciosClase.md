# Ejercicios Clase

## ejercicio-clase-01-10

	class CALCULATOR
	feature
		x: INTEGER
		y: INTEGER
		do
			x := 5
			y := x
		end
	end
	
1. Definir Tokens

		token_class 	→ class
		token_feature 	→ feature
		token_do 		→ do
		token_end 		→ end
		ID 				→ [a-z,A-Z,_]*[a-z,A-Z,0-9,_]
		TYPE 			→ INTEGER | STRING | DOUBLE | BOOL
		token_assign 	→ :=
		token_colon 	→ :
		NUM 			→ [0-9]+
		
2. Proponer una Gramática Libre de Contexto (GLC)

	Tomando los tokens definidos en el punto anterior como base, agrego las reglas de deriacion para los no terminales.
		
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