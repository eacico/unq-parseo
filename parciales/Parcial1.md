# Parcial 1 - Parseo y Generacion de Código

## Ejercicio 1

```
S           → class IDENT Compr Feature end
Compr       → ɛ | id Feature
Feature     → feature DeclList | DeclList
DeclList    → Decl DeclList | ɛ
Decl        → IDENT_LIST : TYPE ; | IDENT : TYPE ;
IDENT_LIST  → IDENT , IDENT_LIST | IDENT
TYPE        → INTEGER | REAL | STRING
```
	
1. Verificar si la gramatica propuesta puede ser simplificada. Justificar paso a paso
2. Si la respuesta del punto anterior es positiva, simplificar la gramatica. Justificar
3. Calcular los conjuntos FIRST y FOLLOW para todos los no terminales.
4. Construye la tabla LL(1) completa (presentarla como matriz o lista de entradas). Marca explicitamente si aparecen entradas vacias (ɛ).
5. Usando la tabla, muestra el analisis predictivo paso a paso para la cadena (tokens): `class POINT is feature x,y: INTEGER; end`
6. indica la pila, la entrada restante y la produccion aplicada en cada paso. Muestra el arbol sintactico final

> <font color="#6564b3">**Solucion**</font>
>
> 1. La gramatica puede ser simplificada, ya que en principio se observa una produccion ɛ.
> 2. 
>>
>>1. Eliminacion producciones ε
>>
>>**DeclList → ɛ**
>>
>>```
>>S           → class IDENT Compr Feature end
>>Compr       → ɛ | id Feature | id
>>Feature     → feature DeclList | Decl | feature
>>DeclList    → Decl DeclList | Decl
>>Decl        → IDENT_LIST : TYPE ; | IDENT : TYPE ;
>>IDENT_LIST  → IDENT , IDENT_LIST | IDENT
>>TYPE        → INTEGER | REAL | STRING
>>```
>>
>>**Compr → ɛ**
>>
>>```
>>S           → class IDENT Compr Feature end | class IDENT Feature end
>>Compr       → id Feature | id
>>Feature     → feature DeclList | Decl | feature
>>DeclList    → Decl DeclList | Decl
>>Decl        → IDENT_LIST : TYPE ; | IDENT : TYPE ;
>>IDENT_LIST  → IDENT , IDENT_LIST | IDENT
>>TYPE        → INTEGER | REAL | STRING
>>```
>>
>>2. Elim. prod. Unitarias**  
>>Las producciones unitarias que habia se quitaron en el paso anterior con la eliminacion de las producciones ɛ.
>>
>>3. Elim. var. no Positivas**  
>>No hay  
>>4. Elim. var. no Alcanzables**  
>>No hay
>>
> 3. 
> 4. 
> 5. 
> 6. 

## Ejercicio 2

Dados los siguintes 2 fragmentos de Eiffel y la siguiente gramatica:

	S 			→ StmtList
	StmtList 	→ StmtList Stmt | Stmt
	Stmt 		→ IDENT := Expr ;
	Expr 		→ Expr + Term | Term
	Term 		→ Term * Factor | Factor
	Factor 		→ ( Factor ) | IDENT | INT

Fragmento A:

	local
		a,b : INTEGER
	do
		a := 1 + 2 * 3;
		b := (a + 4) * 2
	end

Fragmento B:

	if a > b then
		a := a - 1;
	else
		b := b + 1
	end
	secuencia: a := id + id * id;

Para cada fragmento

1. Indicar la secuencia de tokens producida por el lexerque usa las reglas de la gramatica propuesta.
2. Indicar si la sintaxis con la gramatica acepta la secuencia; si no, explica por que y que transformacion/produccion se necesitaria.
3. Si la cadena es aceptada, muestra el arbol de parseo para cualquier `Expr`.
4. Construir la tabla LL(1) con todo lo que conlleva desde cero.

> **_Nota:_** El lenguaje de ejemplo del ejercicio no incluye comparaciones (`>`), ni `if` por defecto;en la respuesta debe indicar como extenderian la gramatica para aceptar`if` (si deciden hacerlo) y como afecta a la tabla LL1.

><font color="#6564b3">**Solucion**</font>
>

## Ejercicio 3

Dada la siguiente gramatica clasica para expresiones

	E → E + E | E * E | ( E ) | id | INT

1. Realizar una transformacion que produzca una gramatica sin ambiguedad que respete: `*` tiene mayor precedencia que `+`, y ambas son asociativas a izquierda. Escribe las producciones.
2. Convertir las producciones resultantes a forma normalde Chomsky (CNF). Justifique paso a paso.

><font color="#6564b3">**Solucion**</font>
>

## Ejercicio 4

Considere el siguiente fragmento de un lenguaje de control de flujo tipo Eiffel

	if <Cond> then <Stmt> else <Stmt>

o bien

	if <Cond> then if <Cond> then <Stmt> else <Stmt>

sabemos que ese tipo de construcciones presentan ambiguedad

1. Definir una gramatica ambigua minima para que defina el fragmento propuesto
2. Contruir ambos arboles de derivacion para la cadena
	```
		if <Cond> then if <Cond> then <Stmt> else <Stmt>
	```
	Explicar paso a paso las producciones aplicadas que llevan a interpretaciones distintas

><font color="#6564b3">**Solucion**</font>
>
>1. Definir una gramatica ambigua minima para que defina el fragmento propuesto
>	```
>		instr → if <expr> then <instr>
>				| if <expr> then <instr> else <instr>
>				| <otra> 
>		expr → ...
>	```
>
>
>2. Contruir ambos arboles de derivacion para la cadena
>
>	![Ejercicio 4.2](./assets/e4-2.drawio.svg)
>
>- Derivacion 1:  
>	**instr** ⇒ if expr then **instr** ⇒ if expr then **instr** ⇒ if expr then if expr then instr else instr
>
>- Derivacion 2:  
>	**instr** ⇒ if expr then **instr** else instr ⇒ if expr then **instr** else instr ⇒ if expr then if expr then instr else Stmt