# Ejercicios Práctica 2B
# PRÁCTICO INTEGRAL – PARSEO DE CÓDIGO Y COMPILADORES

## BLOQUE 1 — Análisis Sintáctico Bottom-Up (LR(0))

Ejercicios

Construir la **colección de items LR(0)** y la tabla ACTION/GOTO para:

```
S → aSbb | ab
```

<font color="orange">**Revisar-Falta**</font>
1. Analizar la cadena `aaabbbb` y mostrar el contenido de la pila paso a paso.

   Coleccion de items LR(0)

   ><font color="#6564b3">**Solucion**</font>
   >
   >Uso la gramatica aumentada
   >
   >```
   >S' → S$
   >S  → aSbb | ab
   >```
   >
   >I<sub>0</sub> = `{ S' → •S$ , S → •aSbb , S → •ab }`\
   >I<sub>1</sub> = `{ S' → S•$ }`\
   >I<sub>2</sub> = `{ S → a•Sbb , S → a•b , S → •aSbb , S → •ab }`\
   >I<sub>3</sub> = `{ S → aS•bb }`\
   >I<sub>4</sub> = `{ S → aSb•b }`\
   >I<sub>5</sub> = `{ S → aSbb• }`\
   >I<sub>6</sub> = `{ S → ab• }`
   >
   >![LR(0)-FDA](./assets/p2b-b1-e1.drawio.svg)
   >
   >tabla ACTION/GOTO
   >
   >|   | GOTO | ACTION                       |||
   >|:--|:----:|:--------:|:--------:|:--------:|
   >|   | S    | a        | b        | $        |
   >| 0 | 1    | S2       |          |          |
   >| 1 |      |          |          | Acc      |
   >| 2 | 4    | S2       | S6       |          |
   >| 3 |      |          | S4       |          |
   >| 4 |      |          | S5       |          |
   >| 5 |      | S → aSbb | S → aSbb | S → aSbb |
   >| 6 |      | S → ab   | S → ab   | S → ab   |
   >
   >Pila
   >
   >
   >| Pila | Entrada | Accion |
   >| :-------- | ------------: | :---- |
   >| 0                                                        | `aaabbbb` | Shift 2 |
   >| 02<sup>a</sup>                                           | `aabbbb`  | Shift 2 |
   >| 02<sup>a</sup>2<sup>a</sup>                              | `abbbb`   | Shift 2 |
   >| 02<sup>a</sup>2<sup>a</sup>2<sup>a</sup>                 | `bbbb`    | Shift 6 |
   >| 02<sup>a</sup>2<sup>a</sup>2<sup>a</sup>6<sup>b</sup>    | `bbb`     |  |
   >| 02<sup>a</sup>2<sup>a</sup>4<sup>S</sup>                 | `bbb`     | Shift 5 |
   >| 02<sup>a</sup>2<sup>a</sup>4<sup>S</sup>5<sup>b</sup>    | `bb`      |  |
   >| 02<sup>a</sup>2<sup>a</sup>4<sup>S</sup>5<sup>bb</sup>   | `b`       |  |
   >| 02<sup>a</sup>4<sup>S</sup>                              | `b`       | Shift 5 |
   >| 02<sup>a</sup>4<sup>S</sup>5<sup>b</sup>                 | `$`       | Shift 5 |
   >
   ><font color="red">**FALTA**</font>


Dada la gramática:

```
E → E + E | E * E | (E) | id
```

<font color="red">**Falta**</font>
2. a. Construir el autómata LR(0).  
   b. Mostrar qué conflictos aparecen y por qué.

Para la gramática:

```
S → SS+ | SS* | a
```

<font color="red">**Falta**</font>
3. Mostrar que **no es LR(0)**. Identificar los estados con conflictos y justificarlos.

Considerar la gramática:

```
Stmt → if Expr then Stmt | if Expr then Stmt else Stmt | assign
Expr → id | const
```

<font color="red">**Falta**</font>
4. a. Construir los items LR(0).  
   b. ¿Es ambiguo? Justifique.

Construir el **autómata LR(0)** y tabla de análisis para:

```
S → (L) | a
L → L, S | S
```

<font color="red">**Falta**</font>
5. Verificar si es LR(0).  
   Analizar la cadena `(a,a,a)` usando la tabla del ejercicio anterior.

Gramática extendida:

```
P → D S
D → D ; D | id : T
T → int | real
S → id := E
E → E + T | T
```

<font color="red">**Falta**</font>
6. Construir los estados LR(0) y mostrar si es o no LR(0). Indicar tipo de conflicto.

Para la gramática:

```
S → A a | b A c | d c | b d a
A → d
```

<font color="red">**Falta**</font>
7. Construir autómata LR(0) y tabla completa. Compárela con el diseño del autómata y observe si quedan iguales.

Diseñar un parser bottom-up manual (con pila) y simular el análisis de:

```
E → E + E | E * E | id
```

con la entrada `id + id * id`.

<font color="red">**Falta**</font>
8. Crear una **gramática ambigua** que genere las cadenas con el mismo número de `a` y `b` y demostrar por qué ningún analizador LR(0) puede procesarla correctamente.

<font color="red">**Falta**</font>
9. Dada la siguiente **gramática**:

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
12. <font color="red">**Falta**</font>
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

<font color="red">**Falta**</font>
1. Implementar un intérprete single store passing para el lenguaje:

```
x := 2
y := x + 3
print(y)
```

   ><font color="#6564b3">**Solucion**</font>
   >

   
<font color="red">**Falta**</font>
2. Mostrar el paso a paso del store passing continuous para la siguiente secuencia:

```
x := 1
y := x + 1
z := y * 2
```

<font color="red">**Falta**</font>
3. Reescribir el intérprete anterior en **forma directa**, explicando diferencias de entorno y memoria.

<font color="red">**Falta**</font>
4. Evaluar y mostrar el entorno, memoria y llamadas recursivas paso a paso:

```
f(n) = if n == 0 then 1 else n * f(n - 1)
f(4)
```

<font color="red">**Falta**</font>
5. Diseñar un interprete continuo que soporte expresiones anidadas (`(e1; e2; e3)`).  
   Implementar `ExprIfZero e1 e2 e3` y simular `if==0 n then 0 else n - 1`.  
   Implementar el tipo `Definition` y `Expr` (como en el ejemplo) y definir la función:

```haskell
eval :: Expr -> [Definition] -> Env -> Memory -> (Value, Memory)
```

<font color="red">**Falta**</font>
6. Ejecutar manualmente `f(3)` donde:

```
define f(n) = if==0 n then 0 else ((n := n + -1); f(n)) + n
```

<font color="red">**Falta**</font>
7. Extender el intérprete con la operación `while e do body`.




























---

## BLOQUE 3 — Generación de Código Intermedio

<font color="yellow">**Revisar**</font>
1. Generar código intermedio para:

```
c := a + b * 2
```

   ><font color="#6564b3">**Solucion**</font>
   >
   >  AST
   >
   >  ![ej](./assets/p2b-b3-e1.drawio.svg)
   >
   >  TAC
   >
   >  ```
   >  t1 := b * 2
   >  t2 := a + t1
   >  ```
   >  
   >  Cuádruplos
   >  
   >  | op | arg<sub>1</sub> | arg<sub>2</sub> | result |
   >  |:--:|:--:|:--:|:--:|
   >  | * | b | 2 | t1 |
   >  | + | a | t1 | t2 |

<font color="red">**Falta**</font>
2. Generar TAC para:

```
x := (a + b) * (c + d)
```

<font color="yellow">**Revisar**</font>
3. Para el siguiente código Eiffel, generar código intermedio con etiquetas y saltos.

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

   ><font color="#6564b3">**Solucion**</font>
   >
   >  TAC
   >
   >  ```
   >     t1 := 0
   >  L1:
   >     t2 := t1 = 3
   >     if t2 goto L2
   >     param t1
   >     call print
   >     t1 := t1 + 1
   >     goto L1
   >  L2:
   >  ```

<font color="red">**Falta**</font>
4. Generar código intermedio con optimización de temporales para:

```
a := b * c + d * e
```

<font color="yellow">**Revisar**</font>
5. Dar una **gramática de atributos** que genere notación posfija (postfijo).  
   Transformar el árbol:\
   `x := (a + b) * (c + d)` en cuádruplas y mostrar cómo se evaluaría.


   ><font color="#6564b3">**Solucion**</font>
   >
   >  ```
   >  E → E1 + T
   >    | T
   >  T → T1 * F
   >    | F
   >  F → (E)
   >    | id
   >  S → id := E
   >  ```
   >  
   >  Reglas
   >  
   >  ```
   >  E → E1 + T
   >      E.post = E1.post || T.post || '+'
   >  E → T
   >      E.post = T.post
   >  
   >  T → T1 * F
   >      T.post = T1.post || F.post || '*'
   >  T → F
   >      T.post = F.post
   >  
   >  F → (E)
   >      F.post = E.post
   >  
   >  F → id
   >      F.post = id.lexeme
   >  
   >  S → id := E
   >      S.post = id.lexeme || E.post || ':='
   >  ```
   >  
   >  ![ej](./assets/p2b-b3-e5.drawio.svg)
   >  
   >  Evaluacion:
   >  
   >  1. 
   >  2. 
   >  3. 
   >  4. `a b +`
   >  5. 
   >  6. 
   >  7. 
   >  8. `c d +`
   >  9. 
   >  10. `a b + c d + *`
   >  11. `x a b + c d + * :=`


<font color="red">**Falta**</font>
6. Implementar una función `emit()` que recorra el AST y genere TAC.  
   Extender el generador para `if-else`:

```
if x < y then z := x else z := y
```

<font color="red">**Falta**</font>
7. Diseñar la generación de código intermedio para while y for.  
   Implementar una mini–máquina de tres direcciones que ejecute el TAC generado.






























---

## BLOQUE 4 — Tipos e Inferencia (Algoritmo , unificación)

<font color="yellow">**Revisar**</font>
1. Aplicar el **Algoritmo de inferencia** sobre:

```
if f(f 0) then True else False
```

   ><font color="#6564b3">**Solucion**</font>
   >
   >Armo el AST y lo enumero en post-order
   >
   >  ![](./assets/p2b-b4-e1.drawio.svg)
   >
   >1. f ⇝ f:?1 ⊢ f:?1
   >2. f ⇝ f:?2 ⊢ f:?2
   >3. 0 ⇝ ∅ ⊢ 0:Int
   >4. 𝕊<sub>4</sub> mgu{?2 ≐ Int → ?3}\
   >     = { ?2 ↦ (Int → ?3) }\
   >     f0 ⇝ f:(Int → ?3), 0:Int ⊢ f0: ?3
   >5. 𝕊<sub>5</sub> mgu{?1 ≐ ?3 → ?4 , ?1 ≐ Int → ?3}\
   >     [Decompose]→ { ?1 ≐ ?1 , ?3 → ?4 ≐ Int → ?3 }\
   >     [Delete,Decompose]→ { ?3 ≐ Int , ?4 ≐ ?3 }\
   >     [Elim]→ { ?3 ↦ Int , ?4 ↦ Int }\
   >     = { ?1 ↦ (Int → Int)}\
   >     f(f0) ⇝ f:(Int → Int), 0:Int ⊢ f(f0): Int
   >6. True ⇝ ∅ ⊢ True:Bool
   >7. False ⇝ ∅ ⊢ False:Bool
   >8. 𝕊<sub>8</sub> mgu{ Int ≐ Bool , Bool ≐ Bool}\
   >     [Clash]→ { Int ≠ Bool }\
   >     **FALLA**

<font color="yellow">**Revisar**</font>
2. Deducir el tipo más general de:

```
λx. λy. x y
```

   ><font color="#6564b3">**Solucion**</font>
   >
   >Armo el AST y lo enumero en post-order
   >
   >  ![](./assets/p2b-b4-e2.drawio.svg)
   >
   >1. x ⇝ x:?1 ⊢ x:?1
   >2. y ⇝ y:?2 ⊢ y:?2
   >3. 𝕊<sub>3</sub> mgu{?1 ≐ ?2 → ?3}\
   >  = { ?1 ↦ (?2 → ?3) }\
   >  xy ⇝ x:(?2 → ?3), y:?2 ⊢ xy: ?3
   >4. λy. xy ⇝ x:(?2 → ?3) ⊢ λy:?2. yx:(?2 → ?3) → ?3
   >5. λx. λy. xy ⇝ ⊢ λx:(?2 → ?3).λy:?2.yx:?2 → ((?2 → ?3) → ?3)

3. <font color="red">**Falta**</font>Resolver las siguientes unificaciones:

```
● α → β = Int → Bool
● α = β → γ
● α → α = β → γ
● α = α → β
```

4. <font color="red">**Falta**</font>Inferir tipo de:

```
f(x, y) = if x then y else 0
```

5. <font color="red">**Falta**</font>Inferir tipos en:

```
λf. λx. f(f(x))
```

6. <font color="red">**Falta**</font>Inferir tipo `if xy then x0 else xSucc(0)` aplicando el algoritmo de inferencia de tipos.

7. <font color="red">**Falta**</font>Dado:

```
Γ = { f : α → β, x : α }
```

inferir tipo de `f x`.





























---

## BLOQUE 5 — Análisis de Flujo de Datos (CFG y Reaching Definitions)

0. <font color="red">**Falta**</font>Traducir el siguiente programa a **código de tres direcciones**:

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

1. <font color="red">**Falta**</font>Identificar **bloques básicos** y construir el **grafo de flujo**.  
2. <font color="red">**Falta**</font>Calcular **definiciones alcanzables** (Reaching Definitions **RD**) en cada bloque.  
3. <font color="red">**Falta**</font>Calcular **variables vivas  (Live Variables)** en el mismo programa.  
4. <font color="red">**Falta**</font>Aplicar **propagación de constantes** y volver a calcular RD.  
5. <font color="red">**Falta**</font>Diseñar el **formato de conjunto IN/OUT** para un análisis de flujo hacia adelante.  
6. <font color="red">**Falta**</font>Implementar el algoritmo iterativo de flujo de datos hasta convergencia.  
7. <font color="red">**Falta**</font>Definir el análisis inverso (hacia atrás) para detectar variables muertas.  
8. <font color="red">**Falta**</font>Analizar el siguiente TAC y optimizarlo eliminando instrucciones muertas:

```
t1 := a + b
t2 := t1 * c
t3 := a + b
print(t2)
```

Discutir cómo se integraría este análisis en una fase de optimización global de un compilador Eiffel.
