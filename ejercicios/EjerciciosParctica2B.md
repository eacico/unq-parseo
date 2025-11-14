# Ejercicios Práctica 2B
# PRÁCTICO INTEGRAL – PARSEO DE CÓDIGO Y COMPILADORES

## BLOQUE 1 — Análisis Sintáctico Bottom-Up (LR(0))

Ejercicios

Construir la **colección de items LR(0)** y la tabla ACTION/GOTO para:

```
S → aSbb | ab
```

1. <font color="orange">**Falta**</font>Analizar la cadena `aaabbbb` y mostrar el contenido de la pila paso a paso.

Dada la gramática:

```
E → E + E | E * E | (E) | id
```

2. a. Construir el autómata LR(0).  
   b. Mostrar qué conflictos aparecen y por qué.

<font color="orange">**Falta**</font>
Para la gramática:

```
S → SS+ | SS* | a
```

3. <font color="orange">**Falta**</font>Mostrar que **no es LR(0)**. Identificar los estados con conflictos y justificarlos.

Considerar la gramática:

```
Stmt → if Expr then Stmt | if Expr then Stmt else Stmt | assign
Expr → id | const
```

4. a. Construir los items LR(0).  
   b. ¿Es ambiguo? Justifique.

<font color="orange">**Falta**</font>
Construir el **autómata LR(0)** y tabla de análisis para:

```
S → (L) | a
L → L, S | S
```

5. <font color="orange">**Falta**</font>Verificar si es LR(0).  
   Analizar la cadena `(a,a,a)` usando la tabla del ejercicio anterior.

Gramática extendida:

```
P → D S
D → D ; D | id : T
T → int | real
S → id := E
E → E + T | T
```

6. <font color="orange">**Falta**</font>Construir los estados LR(0) y mostrar si es o no LR(0). Indicar tipo de conflicto.

Para la gramática:

```
S → A a | b A c | d c | b d a
A → d
```

7. <font color="orange">**Falta**</font>Construir autómata LR(0) y tabla completa. Compárela con el diseño del autómata y observe si quedan iguales.

Diseñar un parser bottom-up manual (con pila) y simular el análisis de:

```
E → E + E | E * E | id
```

con la entrada `id + id * id`.

8. <font color="orange">**Falta**</font>Crear una **gramática ambigua** que genere las cadenas con el mismo número de `a` y `b` y demostrar por qué ningún analizador LR(0) puede procesarla correctamente.

9. <font color="orange">**Falta**</font>Dada la siguiente **gramática**:

```
S → class IDENT InheritBlock FeatureBlock end
InheritBlock → ε | inherit IDENT
FeatureBlock → feature DeclList | DeclList
DeclList → Decl DeclList | ε
Decl → IDENT : TYPE ; | IDENT ( ParamList ) : TYPE ; | IDENT : TYPE := Expr ;
ParamList → Param , ParamList | Param | ε
Param → IDENT : TYPE
TYPE → INTEGER | REAL | STRING | IDENT
Expr → NUMBER | STRING_CONST | IDENT | Expr + Expr | Expr * Expr
```

1. Construir la colección de items LR(0) (I₀, I₁, …).  
2. Mostrar la tabla ACTION/GOTO completa.  
3. Indicar si hay conflictos shift/reduce o reduce/reduce y justificar.  
4. Explicar por qué esta gramática no es estrictamente LR(0).  
5. Analizar la cadena de entrada paso a paso (mostrar pila, entrada y acción en cada paso):

	```
	class Point feature x : INTEGER ; end
	```

---
12. <font color="orange">**Falta**</font>
```
S → class IDENT InheritBlock FeatureBlock end
InheritBlock → ε | inherit IDENT
FeatureBlock → feature DeclList | DeclList
DeclList → Decl DeclList | ε
Decl → IDENT : TYPE ;  
     | IDENT ( ParamList ) : TYPE DoBlock
ParamList → Param , ParamList | Param | ε
Param → IDENT : TYPE
TYPE → INTEGER | REAL | STRING | BOOLEAN | IDENT
DoBlock → do StmtList end
StmtList → Stmt StmtList | ε
Stmt → IDENT := Expr ; | if Expr then StmtList end ;
Expr → NUMBER | IDENT | Expr + Expr | Expr < Expr
```

1. Construir la colección completa de items LR(0).  
2. Identificar los estados con conflictos. ¿Qué tipo de conflicto ocurre (shift/reduce o reduce/reduce)?  
3. Explicar por qué StmtList → Stmt StmtList | ε suele inducir ambigüedad si no se controla la recursión.  
4. Mostrar la tabla ACTION/GOTO con al menos 6 estados clave.  
5. Analizar la siguiente entrada (indicar si es aceptada y qué producción aplica en cada paso):

```eiffel
class Test feature
    f (x : INTEGER) : INTEGER do
        x := x + 1 ;
    end
end .
```

---

## BLOQUE 2 — Intérpretes (store passing y evaluación)

1. <font color="orange">**Falta**</font>Implementar un intérprete single store passing para el lenguaje:

```
x := 2
y := x + 3
print(y)
```

2. <font color="orange">**Falta**</font>Mostrar el paso a paso del store passing continuous para la siguiente secuencia:

```
x := 1
y := x + 1
z := y * 2
```

3. <font color="orange">**Falta**</font>Reescribir el intérprete anterior en **forma directa**, explicando diferencias de entorno y memoria.

4. <font color="orange">**Falta**</font>Evaluar y mostrar el entorno, memoria y llamadas recursivas paso a paso:

```
f(n) = if n == 0 then 1 else n * f(n - 1)
f(4)
```

5. <font color="orange">**Falta**</font>Diseñar un interprete continuo que soporte expresiones anidadas (`(e1; e2; e3)`).  
   Implementar `ExprIfZero e1 e2 e3` y simular `if==0 n then 0 else n - 1`.  
   Implementar el tipo `Definition` y `Expr` (como en el ejemplo) y definir la función:

```haskell
eval :: Expr -> [Definition] -> Env -> Memory -> (Value, Memory)
```

6. <font color="orange">**Falta**</font>Ejecutar manualmente `f(3)` donde:

```
define f(n) = if==0 n then 0 else ((n := n + -1); f(n)) + n
```

7. <font color="orange">**Falta**</font>Extender el intérprete con la operación `while e do body`.

---

## BLOQUE 3 — Generación de Código Intermedio

1. <font color="orange">**Falta**</font>Generar código intermedio para:

```
c := a + b * 2
```

2. <font color="orange">**Falta**</font>Generar TAC para:

```
x := (a + b) * (c + d)
```

3. <font color="orange">**Falta**</font>Para el siguiente código Eiffel, generar código intermedio con etiquetas y saltos.

```eiffel
from
    i := 0
until
    i = 3
loop
    print(i)
    i := i + 1
end
```

4. <font color="orange">**Falta**</font>Generar código intermedio con optimización de temporales para:

```
a := b * c + d * e
```

5. <font color="orange">**Falta**</font>Dar una **gramática de atributos** que genere notación posfija (postfijo).  
   Transformar el árbol:

```
x := (a + b) * (c + d)
```

en cuádruplas y mostrar cómo se evaluaría.

6. <font color="orange">**Falta**</font>Implementar una función `emit()` que recorra el AST y genere TAC.  
   Extender el generador para `if-else`:

```
if x < y then z := x else z := y
```

7. <font color="orange">**Falta**</font>Diseñar la generación de código intermedio para while y for.  
   Implementar una mini–máquina de tres direcciones que ejecute el TAC generado.

---

## BLOQUE 4 — Tipos e Inferencia (Algoritmo , unificación)

1. <font color="orange">**Falta**</font>Aplicar el **Algoritmo de inferencia** sobre:

```
if f(f 0) then True else False
```

2. <font color="orange">**Falta**</font>Deducir el tipo más general de:

```
λx. λy. x y
```

3. <font color="orange">**Falta**</font>Resolver las siguientes unificaciones:

```
● α → β = Int → Bool
● α = β → γ
● α → α = β → γ
● α = α → β
```

4. <font color="orange">**Falta**</font>Inferir tipo de:

```
f(x, y) = if x then y else 0
```

5. <font color="orange">**Falta**</font>Inferir tipos en:

```
λf. λx. f(f(x))
```

6. <font color="orange">**Falta**</font>Inferir tipo  if xy then x0 else xSucc(0) aplicando el algoritmo de inferencia de tipos.

7. <font color="orange">**Falta**</font>Dado:

```
Γ = { f : α → β, x : α }
```

inferir tipo de f x.

---

## BLOQUE 5 — Análisis de Flujo de Datos (CFG y Reaching Definitions)

0. <font color="orange">**Falta**</font>Traducir el siguiente programa a **código de tres direcciones**:

```
x := 1
y := 0
while x < n {
   if y > x {
      y := x
      x := x + y
   } else {
      x := x + y
      y := x
   }
}
```

1. <font color="orange">**Falta**</font>Identificar **bloques básicos** y construir el **grafo de flujo**.  
2. <font color="orange">**Falta**</font>Calcular **definiciones alcanzables** (Reaching Definitions **RD**) en cada bloque.  
3. <font color="orange">**Falta**</font>Calcular **variables vivas  (Live Variables)** en el mismo programa.  
4. <font color="orange">**Falta**</font>Aplicar **propagación de constantes** y volver a calcular RD.  
5. <font color="orange">**Falta**</font>Diseñar el **formato de conjunto IN/OUT** para un análisis de flujo hacia adelante.  
6. <font color="orange">**Falta**</font>Implementar el algoritmo iterativo de flujo de datos hasta convergencia.  
7. <font color="orange">**Falta**</font>Definir el análisis inverso (hacia atrás) para detectar variables muertas.  
8. <font color="orange">**Falta**</font>Analizar el siguiente TAC y optimizarlo eliminando instrucciones muertas:

```
t1 := a + b
t2 := t1 * c
t3 := a + b
print(t2)
```

Discutir cómo se integraría este análisis en una fase de optimización global de un compilador Eiffel.
