# Parcial 1 - Parseo y Generacion de Código

## Ejercicio 1

```
S           → class IDENT Compr Feature end
Compr       → ɛ | is Feature
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
>>Compr       → ɛ | is Feature | is
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
>>Compr       → is Feature | is
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
> 3. <font color="red">**Falto eliminar recursion por izquierda y factorizar para eliminar la ambiguedad de la gramatica**</font>
><table>
><tr><th></th><th>FIRST</th><th></th></tr>
>
><tr><td style="vertical-align: top;">
>
>```
>S           → class IDENT Compr Feature end
>Compr       → ɛ | is Feature | id
>Feature     → feature DeclList | Decl | feature
>DeclList    → Decl DeclList | Decl
>Decl        → IDENT_LIST : TYPE ; | IDENT : TYPE ;
>IDENT_LIST  → IDENT , IDENT_LIST | IDENT
>TYPE        → INTEGER | REAL | STRING
>```
>
></td><td style="vertical-align: top;">
>
>```
>{ class }
>{ ɛ, is }
>{ feature } + FIRST(Decl)
>FIRST(Decl)
>{ IDENT } + FIRST(IDENT_LIST)
>{ IDENT }
>{ INTEGER, REAL, STRING }
>```
>
></td><td style="vertical-align: top;">
>
>```
>S: { class }
>Compr: { ɛ, is }
>Feature: { feature, IDENT }
>DeclList: { IDENT }
>Decl: { IDENT }
>IDENT_LIST: { IDENT }
>TYPE: { INTEGER, REAL, STRING }
>```
>
></td></tr></table>
>
>
><table>
><tr><th></th><th>FIRST</th><th>FOLLOW</th><th></th></tr>
>
><tr><td style="vertical-align: top;">
>
>```
>S           → class IDENT Compr Feature end
>Compr       → ɛ | is Feature | id
>Feature     → feature DeclList | Decl | feature
>DeclList    → Decl DeclList | Decl
>Decl        → IDENT_LIST : TYPE ; | IDENT : TYPE ;
>IDENT_LIST  → IDENT , IDENT_LIST | IDENT
>TYPE        → INTEGER | REAL | STRING
>```
>
></td><td style="vertical-align: top;">
>
>```
>S: { class }
>Compr: { ɛ, is }
>Feature: { feature, IDENT }
>DeclList: { IDENT }
>Decl: { IDENT }
>IDENT_LIST: { IDENT }
>TYPE: { INTEGER, REAL, STRING }
>```
>
></td><td style="vertical-align: top;">
>
>```
>S: { $ }
>Compr: FIRST(Feature)
>Feature: { end }+FOLLOW(Compr)
>DeclList: FOLLOW(Feature)
>Decl: FOLLOW(Feature)+FOLLOW(DeclList)
>IDENT_LIST: { : }
>TYPE: { ; }
>```
>
></td><td style="vertical-align: top;">
>
>```
>S: { $ }
>Compr: { feature, IDENT }
>Feature: { end, feature, IDENT }
>DeclList: { end, feature, IDENT }
>Decl: { end, feature, IDENT }
>IDENT_LIST: { : }
>TYPE: { ; }
>```
>
></td></tr></table>
>
> 4. <font color="red">**Falta**</font>  
>
>||FIRST|FOLLOW|
>|:--|:--|:--|
>|S | class | $ |
>|Compr | ɛ is | feature IDENT |
>|Feature | feature, IDENT | end feature IDENT |
>|DeclList | IDENT | end, feature IDENT |
>|Decl | IDENT | end feature IDENT |
>|IDENT_LIST | IDENT | : |
>|TYPE | INTEGER REAL STRING | ; |
>
>
>Terminales: `class, IDENT, end, id, feature, ',', INTEGER, REAL, STRING`  
>No Terminales: `S, Compr, Feature, DeclList, Decl, IDENT_LIST, TYPE`
>
>Enumero producciones para reducir tamaño de la tabla
>
>```
>01) S          → class IDENT Compr Feature end
>02) Compr      → ɛ 
>03)            | is Feature 
>04)            | is
>05) Feature    → feature DeclList 
>06)            | Decl 
>07)            | feature
>08) DeclList   → Decl DeclList 
>09)            | Decl
>10) Decl       → IDENT_LIST : TYPE ; 
>11)            | IDENT : TYPE ;
>12) IDENT_LIST → IDENT , IDENT_LIST 
>13)            | IDENT
>14) TYPE       → INTEGER 
>15)            | REAL 
>16)            | STRING
>```
>
>|             | class | IDENT | end | is | feature | ,  | INTEGER | REAL | STRING | $  |
>| :--         | --    | --    | --  | -- | --      | -- | --      | --   | --     | -- |
>| S           | 1     |       |     |    |         |    |         |      |        |    |
>| Compr       |       | 2     |     | 3 4| 2       |    |         |      |        |    |
>| Feature     |       | 6     |     |    | 5 7     |    |         |      |        |    |
>| DeclList    |       | 8 9   |     |    |         |    |         |      |        |    |
>| Decl        |       | 10 11 |     |    |         |    |         |      |        |    |
>| IDENT_LIST  |       | 12 13 |     |    |         |    |         |      |        |    |
>| TYPE        |       |       |     |    |         |    | 14      | 15   | 16     |    |
>
><font color="red">**Conficto**</font>: La gramatica tiene conflicto en la celda [Compr, id] con mas de una produccion, por lo que la gramatica no es LL(1)  
> 5. Armo la primera parte de de la pila usando las producciones de la tabla hasta el primer conflicto.  
>
>cadena: `class POINT is feature x,y: INTEGER; end`
>
>| Entrada | Pila | |
>| :-------- | ------------: | :---- |
>| `class POINT is feature x,y: INTEGER; end` | S | M[S,class] = S → VS |
>| `class POINT is feature x,y: INTEGER; end` | class IDENT Compr Feature end|  |
>| `POINT is feature x,y: INTEGER; end` | IDENT Compr Feature end|  |
>| `is feature x,y: INTEGER; end` | Compr Feature end| M[Compr,is] = `is Feature` `is` |
>
> 6. <font color="red">**Falta**</font>  

## Ejercicio 2

Dados los siguintes 2 fragmentos de Eiffel y la siguiente gramatica:
>```
>S 			→ StmtList
>StmtList 	→ StmtList Stmt | Stmt
>Stmt 		→ IDENT := Expr ;
>Expr 		→ Expr + Term | Term
>Term 		→ Term * Factor | Factor
>Factor 		→ ( Factor ) | IDENT | INT
>```

Fragmento A:
>```
>local
>	a,b : INTEGER
>do
>	a := 1 + 2 * 3;
>	b := (a + 4) * 2
>end
>```

Fragmento B:
>```
>if a > b then
>  a := a - 1;
>else
>  b := b + 1
>end
>secuencia: a := id + id * id;
>```

Para cada fragmento

1. Indicar la secuencia de tokens producida por el lexer que usa las reglas de la gramatica propuesta.
2. <font color="red">**Falta**</font> Indicar si la sintaxis con la gramatica acepta la secuencia; si no, explica por que y que transformacion/produccion se necesitaria.
3. <font color="red">**Falta**</font> Si la cadena es aceptada, muestra el arbol de parseo para cualquier `Expr`.
4. <font color="red">**Falta**</font> Construir la tabla LL(1) con todo lo que conlleva desde cero.

> **_Nota:_** El lenguaje de ejemplo del ejercicio no incluye comparaciones (`>`), ni `if` por defecto;en la respuesta debe indicar como extenderian la gramatica para aceptar`if` (si deciden hacerlo) y como afecta a la tabla LL1.

><font color="#6564b3">**Solucion**</font>
>
> 1. La gramática sólo reconoce identificadores (`IDENT`), enteros (`INT`), y los símbolos `:=`, `+`, `*`, `(`, `)`, `;`.  
> Pero no reconoce palabras clave como `local`, `if`, `then`, `else`, `end`, `do`, ni operadores relacionales como `>`, ni `-`.  
><table>
><tr><th>Fragmento A</th><th>Fragmento B</th></tr>
><tr><td style="vertical-align: top;">
>
> ```
>IDENT(local)
>IDENT(a)
>,
>IDENT(b)
>:
>IDENT(INTEGER)
>IDENT(do)
>IDENT(a)
>:=
>INT(1)
>+
>INT(2)
>*
>INT(3)
>;
>IDENT(b)
>:=
>(
>IDENT(a)
>+
>INT(4)
>)
>*
>INT(2)
>IDENT(end)
>```
>
></td><td style="vertical-align: top;">
>
> ```
>IDENT(if)
>IDENT(a)
>UNKNOWN(>)   -- no pertenece a la gramática
>IDENT(b)
>IDENT(then)
>IDENT(a)
>:=
>IDENT(a)
>UNKNOWN(-)   -- no pertenece a la gramática
>INT(1)
>;
>IDENT(else)
>IDENT(b)
>:=
>IDENT(b)
>+
>INT(1)
>IDENT(end)
>```
>
></td></tr></table>
>
>2. 
>

## Ejercicio 3

Dada la siguiente gramatica clasica para expresiones

	E → E + E | E * E | ( E ) | id | INT

1. Realizar una transformacion que produzca una gramatica sin ambiguedad que respete: `*` tiene mayor precedencia que `+`, y ambas son asociativas a izquierda. Escribe las producciones.
2. Convertir las producciones resultantes a forma normal de Chomsky (CNF). Justifique paso a paso.

><font color="#6564b3">**Solucion**</font>
>
>1. Primero separo las producciones de cada operador en reglas nuevas.
>```
>E → E + T | T
>T → T * F | F
>F → (E) | id | INT
>```
>Quito la recursion por izquierda:  
>Primero ordeno las variables (E,T,F) y elimino la producciones que comienzan con algun simbolo anterior. Ninguna empieza con una variable anterior.  
>Ahora debo eliminar la recursion directa. Para eso dejo en la produccion original solo las reglas terminales y a la derecha agrego la nueva regla prima. Luego creo la regla prima que va a tener las producciones originalmente recursivas a izquierda sin la variable a la izquierda y con la variable prima a la derecha. Ademas a las variables primas le agrego la produccion epsilon.
>```
>E  → T E'
>E' → ε | + T E'
>T  → F T'
>T' → ε | * F T'
>F  → (E) | id | INT
>```
>2. Primero necesito simplificar la gramatica.  
>
>Elimino producciones ε:  
>```
>E  → T E' | T
>E' → + T | + T E'
>T  → F T' | F
>T' → * F | * F T'
>F  → (E) | id | INT
>```
>Elimino producciones unitarias:  
>```
>E  → T E' | F T' | (E) | id | INT
>E' → + T | + T E'
>T  → F T' | (E) | id | INT
>T' → * F | * F T'
>F  → (E) | id | INT
>```
>Las producciones que quedan son positivas y alcanzables, asi que ya esta simplificado.  
>
>FNC solo permite producciones con terminales, o hasta 2 variables concatenadas, pero no producciones que mezclen variables y terminales.  
>Por esto primero separo las producciones con terminales de las no terminales
>
>Primero defino nuevas reglas que contengan cada terminal y sustituyo en las demas producciones.
>```
>E  → T E' | F T' | X5 E X6 | X1 | x2
>E' → X3 T | X3 T E'
>T  → F T' | X5 E X6 | X1 | x2
>T' → X4 F | X4 F T'
>F  → X5 E X6 | X1 | x2
>X1 → id
>x2 → INT
>X3 → +
>X4 → *
>X5 → (
>X6 → )
>```
>Y por ultimo sustituyo producciones que tengan 3 o mas variables
>```
>E  → T E' | F T' | X5 Y1 | X1 | x2
>Y1 → E X6
>E' → X3 T | X3 Y2
>Y2 → T E'
>T  → F T' | X5 Y1 | X1 | x2
>T' → X4 F | X4 Y3
>Y3 → F T'
>F  → X5 Y1 | X1 | x2
>X1 → id
>x2 → INT
>X3 → +
>X4 → *
>X5 → (
>X6 → )
>```

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
> ```
> instr → if <expr> then <instr>
>       | if <expr> then <instr> else <instr>
>       | <otra> 
> expr → ...
> ```
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