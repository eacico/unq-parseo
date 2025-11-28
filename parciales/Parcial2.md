# Parsea de código
## Segundo Parcial
Licenciatura en Informática  
Universidad Nacional de Quilmes  
19 de Noviembre de 2025  

---

### Instrucciones:
1. No se permite el uso de material.
2. Todos los ejercicios deben estar justificados rigurosamente.
3. Se valorará la prolijidad, formalidad y profundidad de la solución propuesta.

---

## Ejercicio 1
Dada la gramática de un mini-lenguaje de expresiones con if y asignaciones:
```
S    → S ; S | Stmt | ε
Stmt → ID := E | if E then Stmt
E    → E + T | T
T    → ID | NUM
```

a) <font color="red">**Falta**</font> ¿Qué puede decir acerca de la gramática presentada? Realice un análisis desde su perspectiva.  
b) Construya la versión **LR(0)** para la gramática presentada.  
c) Construya el autómata LR(0) de items.  
d) <font color="red">**Falta**</font> Justifique y realice un analisis de su perspectiva para las siguientes preguntas  
- ¿Cuales son las limitaciones del analizador LR(0)?
- ¿Cómo se puede mejorar un analizador LR(0)?

><font color="#6564b3">**Solucion**</font>
>
>b) Primero simplifico la gramatica
>
> <table>
> <tr><td style="vertical-align: top;">
> 
> ```
> S    → S ; S 
>      | Stmt 
>      | ε
> Stmt → ID := E 
>      | if E then Stmt
> E    → E + T 
>      | T
> T    → ID 
>      | NUM
> ```
> 
> </td><td style="vertical-align: top;">
> 
> Elimino producciones **ε**
> ```
> S    → S ; S 
>      | Stmt 
>      | ; S 
>      | S ;
>      | ; 
> Stmt → ID := E 
>      | if E then Stmt
> E    → E + T 
>      | T
> T    → ID 
>      | NUM
> ```
> 
> </td><td style="vertical-align: top;">
> 
> Elimino producciones **Unitarias**
> ```
> S    → S ; S 
>      | ; S 
>      | S ;
>      | ; 
>      | ID := E
>      | if E then Stmt
> Stmt → ID := E 
>      | if E then Stmt
> E    → E + T 
>      | ID
>      | NUM
> T    → ID 
>      | NUM
> ```
> 
> </td><td style="vertical-align: top;">
> 
> Elimino producciones **No Positivas**  
> No hay  
> Elimino producciones **Inalcanzables**  
> No hay  
> 
> </td></tr>
> </table>
> 
> Aumento la gramatica resultante para agregar el caracter de finalizacion:
> ```
> S'   → S $
> S    → S ; S 
>      | ; S 
>      | S ;
>      | ; 
>      | ID := E
>      | if E then Stmt
> Stmt → ID := E 
>      | if E then Stmt
> E    → E + T 
>      | ID
>      | NUM
> T    → ID 
>      | NUM
> ```
>
> c)  
> Ahora genero la lista de Items clausurando cada una:  
> *I<sub>0</sub>* = `{ S' → •S $, S → •S ; S, S → •; S, S → •S ;, S → •;, S → •ID := E, S → •if E then Stmt }`  
> &emsp; [ `S`→*I<sub>1</sub>*, `;`→*I<sub>5</sub>*, `ID`→*I<sub>7</sub>*, `if`→*I<sub>14</sub>* ]  
> *I<sub>1</sub>* = `{ S' → S •$, S → S •; S, S → S •; }`  
> &emsp; [ `$`→*I<sub>2</sub>*, `;`→*I<sub>3</sub>* ]  
> *I<sub>2</sub>* = `{ S' → S $• }`  
> &emsp; [ ACCEPT ]  
> *I<sub>3</sub>* = `{ S → S ; •S, S → S ;•, S → •S ; S, S → •; S, S → •S ;, S → •;, S → •ID := E, S → •if E then Stmt }`  
> &emsp; [ `S`→*I<sub>4</sub>*, `;`→*I<sub>5</sub>*, `ID`→*I<sub>7</sub>*, `if`→*I<sub>14</sub>* ]  
> *I<sub>4</sub>* = `{ S → S ; S•, S → S •; S, S → S •; }`  
> &emsp; [ `;`→*I<sub>3</sub>* ]  
> *I<sub>5</sub>* = `{ S → ; •S, S → ;•, S → •S ; S, S → •; S, S → •S ;, S → •;, S → •ID := E, S → •if E then Stmt }`  
> &emsp; [ `S`→*I<sub>6</sub>*, `;`→*I<sub>5</sub>*, `ID`→*I<sub>7</sub>*, `if`→*I<sub>14</sub>* ]  
> *I<sub>6</sub>* = `{ S → ; S•, S → S •; S, S → S •; }`  
> &emsp; [ `;`→*I<sub>3</sub>* ]  
> *I<sub>7</sub>* = `{ S → ID •:= E }`  
> &emsp; [ `:=`→*I<sub>8</sub>* ]  
> *I<sub>8</sub>* = `{ S → ID := •E, E → •E + T, E → •ID, E → •NUM }`  
> &emsp; [ `E`→*I<sub>9</sub>*, `ID`→*I<sub>12</sub>* , `NUM`→*I<sub>13</sub>* ]  
> *I<sub>9</sub>* = `{ S → ID := E•, E → E •+ T }`  
> &emsp; [ `+`→*I<sub>10</sub>* ]  
> *I<sub>10</sub>* = `{ E → E + •T, T → •ID, T → •NUM }`  
> &emsp; [ `T`→*I<sub>11</sub>*, `ID`→*I<sub>12</sub>* , `NUM`→*I<sub>13</sub>* ]  
> *I<sub>11</sub>* = `{ E → E + T• }`  
> &emsp; []  
> *I<sub>12</sub>* = `{ T → ID• }`  
> &emsp; []  
> *I<sub>13</sub>* = `{ T → NUM• }`  
> &emsp; []  
> *I<sub>14</sub>* = `{ S → if •E then Stmt, E → •E + T, E → •ID, E → •NUM }`  
> &emsp; [ `E`→*I<sub>15</sub>*, `ID`→*I<sub>12</sub>* , `NUM`→*I<sub>13</sub>* ]  
> *I<sub>15</sub>* = `{ S → if E •then Stmt, E → E •+ T }`  
> &emsp; [ `then`→*I<sub>16</sub>*, `+`→*I<sub>10</sub>* ]  
> *I<sub>16</sub>* = `{ S → if E then •Stmt, Stmt → •ID := E → •if E then Stmt }`  
> &emsp; [ `Stmt`→*I<sub>17</sub>*, `ID`→*I<sub>7</sub>*, `if`→*I<sub>14</sub>* ]  
> *I<sub>17</sub>* = `{ S → if E then Stmt• }`  
> &emsp; []  
> 
> M=(Q,Σ,δ,I<sub>0</sub>​,F)  
>  &emsp; Q={I<sub>0</sub>, ... , I<sub>17</sub>​}  
>  &emsp; Σ={0,1}  
>  &emsp; F={I<sub>2</sub>​}  
>  &emsp; δ = {  
>  &emsp; &emsp; δ(*I<sub>0</sub>*, `S`)→*I<sub>1</sub>*, δ(*I<sub>0</sub>*, `;`)→*I<sub>5</sub>*, δ(*I<sub>0</sub>*, `ID`)→*I<sub>7</sub>*, δ(*I<sub>0</sub>*, `if`)→*I<sub>14</sub>*,  
>  &emsp; &emsp; δ(*I<sub>1</sub>*, `$`)→*I<sub>2</sub>*, δ(*I<sub>1</sub>*, `;`)→*I<sub>3</sub>*,  
>  &emsp; &emsp; δ(*I<sub>3</sub>*, `S`)→*I<sub>4</sub>*, δ(*I<sub>3</sub>*, `;`)→*I<sub>5</sub>*, δ(*I<sub>3</sub>*, `ID`)→*I<sub>7</sub>*, δ(*I<sub>3</sub>*, `if`)→*I<sub>14</sub>*,  
>  &emsp; &emsp; δ(*I<sub>4</sub>*, `;`)→*I<sub>3</sub>*,  
>  &emsp; &emsp; δ(*I<sub>5</sub>*, `S`)→*I<sub>6</sub>*, δ(*I<sub>5</sub>*, `;`)→*I<sub>5</sub>*, δ(*I<sub>5</sub>*, `ID`)→*I<sub>7</sub>*, δ(*I<sub>5</sub>*, `if`)→*I<sub>14</sub>*,  
>  &emsp; &emsp; δ(*I<sub>6</sub>*, `;`)→*I<sub>3</sub>*,  
>  &emsp; &emsp; δ(*I<sub>7</sub>*, `:=`)→*I<sub>8</sub>*,  
>  &emsp; &emsp; δ(*I<sub>8</sub>*, `E`)→*I<sub>9</sub>*, δ(*I<sub>8</sub>*, `ID`)→*I<sub>12</sub>* , δ(*I<sub>8</sub>*, `NUM`)→*I<sub>13</sub>*,  
>  &emsp; &emsp; δ(*I<sub>9</sub>*, `+`)→*I<sub>10</sub>*,  
>  &emsp; &emsp; δ(*I<sub>10</sub>*, `T`)→*I<sub>11</sub>*, δ(*I<sub>10</sub>*, `ID`)→*I<sub>12</sub>* , δ(*I<sub>10</sub>*, `NUM`)→*I<sub>13</sub>*,  
>  &emsp; &emsp; δ(*I<sub>14</sub>*, `E`)→*I<sub>15</sub>*, δ(*I<sub>14</sub>*, `ID`)→*I<sub>12</sub>* , δ(*I<sub>14</sub>*, `NUM`)→*I<sub>13</sub>*,  
>  &emsp; &emsp; δ(*I<sub>15</sub>*, `then`)→*I<sub>16</sub>*, δ(*I<sub>15</sub>*, `+`)→*I<sub>10</sub>*,  
>  &emsp; &emsp; δ(*I<sub>16</sub>*, `Stmt`)→*I<sub>17</sub>*, δ(*I<sub>16</sub>*, `ID`)→*I<sub>7</sub>*, δ(*I<sub>16</sub>*, `if`)→*I<sub>14</sub>*​  
>  &emsp; }  
> 
> <font color="red">**Falta terminar**</font>  
> ![ej](./assets/p2-e1c.drawio.svg)
> 
> |   | GOTO             |||| ACTION                              ||||||||   |
> |:--|:--:|:----:|:--:|:--:|:--:|:---:|:---:|:----:|:--:|:--:|:---:|:--:|:--|
> |   | S  | Stmt | E  | T  | ;  | :=  | if  | then | +  | ID | NUM | $  ||
> | 0 | 1  |      |    |    | S5 |     | S14 |      |    | S7 |     |    ||
> | 1 |    |      |    |    | S3 |     |     |      |    |    |     | ACC||
> | 3 | 4  |      |    |    | S5 |     | S14 |      |    | S7 |     |    ||
> | 4 |    |      |    |    | S3 |     |     |      |    |    |     |    ||
> | 5 | 6  |      |    |    | S5 |     | S14 |      |    | S7 |     |    ||
> | 6 |    |      |    |    | S3 |     |     |      |    |    |     |    ||
> | 7 |    |      |    |    |    | S8  |     |      |    |    |     |    ||
> | 8 |    |      | 9  |    |    |     |     |      |    | S12| S13 |    ||
> | 9 |    |      |    |    |    |     |     |      | S10|    |     |    ||
> | 10|    |      |    | 11 |    |     |     |      |    | S12| S13 |    ||
> | 11|    |      |    |    |    |     |     |      |    |    |     |    |E → E + T|
> | 12|    |      |    |    |    |     |     |      |    |    |     |    |T → ID|
> | 13|    |      |    |    |    |     |     |      |    |    |     |    |T → NUM|
> | 14|    |      | 15 |    |    |     |     |      |    | S12| S13 |    ||
> | 15|    |      |    |    |    |     |     | S16  | S10|    |     |    ||
> | 16|    | 17   |    |    |    |     | S14 |      |    | S7 |     |    ||
> | 17|    |      |    |    |    |     |     |      |    |    |     |    |S → if E then Stmt|
> 
> <font color="red">**Creo que hay error porque hay estados con el cursor al final en items que tambientienen items no finalizados (items 3,4,5,6,9).**</font>

---

## Ejercicio 2
Considere el siguiente fragmento de un programa:

```text
x := 1  
y := 0  
while x < n do  
		if y > x then  
			y := x
				for i to 30  
					x= y*x + i + x
		else
			x := x + y
				for i to 50
					x= y*x - i + x
    end  
    x := x + 1  
end  
return x
```

a) <font color="yellow">**Revisar IA**</font> Construya el código intermedio (instrucciones)  
b) <font color="yellow">**Revisar IA**</font> Genere código de **tres direcciones**  
c) <font color="yellow">**Revisar IA**</font> Identifique los **líderes** y forme los bloques básicos completos.  
d) <font color="red">**Falta**</font> Construya el **grafo de flujo de control** (CFG). ¿Qué puede decir de él?  
e) <font color="red">**Falta**</font> ¿Qué tipo de interpretación propondría para este fragmento de programa? Justifique su elección con un análisis de ventajas y desventajas asociadas a cada tipo de intérprete para el código dado.  

><font color="#6564b3">**Solucion**</font>
>
> <table>
> <tr><td style="vertical-align: top;">
> 
> a)
> ```
> 1.   x := 1
> 2.   y := 0
> 
> 3.   L1: if x < n goto L2
> 4.       goto LEND
> 
> 5.   L2: if y > x goto THEN
> 6.       goto ELSE
> 
>         THEN:
> 7.         y := x
> 8.         i := 1
> 9.   L3:   if i <= 30 goto L4
> 10.          goto L5
> 11.  L4:   t1 := y * x
> 12.        t2 := t1 + i
> 13.        x  := t2 + x
> 14.        i := i + 1
> 15.        goto L3
> 16.  L5:   goto AFTER_IF
> 
>         ELSE:
> 17.        x := x + y
> 18.        j := 1
> 19.  L6:   if j <= 50 goto L7
> 20.          goto L8
> 21.  L7:   t3 := y * x
> 22.        t4 := t3 - j
> 23.        x  := t4 + x
> 24.        j := j + 1
> 25.        goto L6
> 26.  L8:   goto AFTER_IF
> 
> 27. AFTER_IF:
> 28.      x := x + 1
> 29.      goto L1
> 
> 30. LEND:
> 31. return x
> ```
> 
> </td><td style="vertical-align: top;">
> 
> b)
> ```
> 1   x := 1
> 2   y := 0
> 
> 3 L1:
> 4   t1 := x < n
> 5   if t1 goto L2
> 6   goto LEND
> 
> 7 L2:
> 8   t2 := y > x
> 9   if t2 goto THEN
> 10  goto ELSE
> 
> THEN:
> 11  y := x
> 12  i := 1
> 
> 13 L3:
> 14  t3 := i <= 30
> 15  if t3 goto L4
> 16  goto L5
> 
> 17 L4:
> 18  t4 := y * x
> 19  t5 := t4 + i
> 20  t6 := t5 + x
> 21  x := t6
> 22  t7 := i + 1
> 23  i := t7
> 24  goto L3
> 
> 25 L5:
> 26  goto AFTER_IF
> 
> ELSE:
> 27  t8 := x + y
> 28  x := t8
> 29  j := 1
> 
> 30 L6:
> 31  t9 := j <= 50
> 32  if t9 goto L7
> 33  goto L8
> 
> 34 L7:
> 35  t10 := y * x
> 36  t11 := t10 - j
> 37  t12 := t11 + x
> 38  x := t12
> 39  t13 := j + 1
> 40  j := t13
> 41  goto L6
> 
> 42 L8:
> 43  goto AFTER_IF
> 
> 44 AFTER_IF:
> 45  t14 := x + 1
> 46  x := t14
> 47  goto L1
> 
> 48 LEND:
> 49  return x
> ```
> 
> </td><td style="vertical-align: top;">
> 
> c)  
> Líderes:
> - 1 (primera)
> - L1 (3)
> - L2 (7)
> - THEN (11)
> - L3 (13)
> - L4 (17)
> - L5 (25)
> - ELSE (27)
> - L6 (30)
> - L7 (34)
> - L8 (42)
> - AFTER_IF (44)
> - LEND (48)
> 
> Bloques básicos  
> **BB1**
> ```
> 1  x := 1
> 2  y := 0
> ```
> **BB2 (L1)**
> ```
> 3 L1:
> 4 t1 := x < n
> 5 if t1 goto L2
> 6 goto LEND
> ```
> **BB3 (L2)**
> ```
> 7 L2:
> 8 t2 := y > x
> 9 if t2 goto THEN
> 10 goto ELSE
> ```
> **BB4 (THEN)**
> ```
> 11 y := x
> 12 i := 1
> ```
> **BB5 (L3)**
> ```
> 13 L3:
> 14 t3 := i <= 30
> 15 if t3 goto L4
> 16 goto L5
> ```
> 
> </td><td style="vertical-align: top;">
> 
> **BB6 (L4)**
> ```
> 17 L4:
> 18 t4 := y * x
> 19 t5 := t4 + i
> 20 t6 := t5 + x
> 21 x := t6
> 22 t7 := i + 1
> 23 i := t7
> 24 goto L3
> ```
> **BB7 (L5)**
> ```
> 25 L5:
> 26 goto AFTER_IF
> ```
> **BB8 (ELSE)**
> ```
> 27 t8 := x + y
> 28 x := t8
> 28 j := 1
> ```
> **BB9 (L6)**
> ```
> 30 L6:
> 31 t9 := j <= 50
> 32 if t9 goto L7
> 33 goto L8
> ```
> **BB10 (L7)**
> ```
> 34 L7:
> 35 t10 := y * x
> 36 t11 := t10 - j
> 37 t12 := t11 + x
> 38 x := t12
> 39 t13 := j + 1
> 40 j := t13
> 41 goto L6
> ```
> **BB11 (L8)**
> ```
> 42 L8:
> 43 goto AFTER_IF
> ```
> **BB12 (AFTER_IF)**
> ```
> 44 AFTER_IF:
> 45 t14 := x + 1
> 46 x := t14
> 47 goto L1
> ```
> **BB13 (LEND)**
> ```
> 48 LEND:
> 49 return x
> ```
> 
> </td></tr>
> </table>
> 

---

## Ejercicio 3

Dadas las siguientes expresiones:

```
if x=y then x=0 else x=Succ(0)
if x=y then y=f(x) else x=g(0)
if f x then Succ(x) else f(0)
```

a) <font color="red">**Falta**</font> Aplicar el algoritmo de inferencia de tipos sobre los siguientes términos, obteniendo así el juicio de tipoado más general posible que les asigna un tipo.  
b) <font color="red">**Falta**</font> En un lenguaje con tipos simples, ¿qué restricciones impone la operación de igualdad?  

Nota: `Succ` es una función del tipo `N→N`.

><font color="#6564b3">**Solucion**</font>
>

---

## Ejercicio 4:

1. <font color="red">**Falta**</font> Definir un intérprete:

```text
eval :: Expr → [Definition] → Env Addr → Memory Int → (Int, Memory Int)
```

para el lenguaje:

```text
Expr ::= Var x  
        | Const n  
        | Add Expr Expr  
        | Assign x Expr  
        | Seq Expr Expr  
        | Call f [Expr]  
        | IfZero Expr Expr Expr  
```

Las definiciones de funciones son:

```text
Define f (params) = body
```

**Programa a evaluar**

Dadas las definiciones:

```text
define dec(x) = if ==0 x then 0 else (x := x + -1; dec(x))
define h(a, b) = if ==0 a then b else (b := b + 1; h(a + -1, b))
```

Evaluar: `Seq( Assign("y", Const 3), Call "h" [ Const 2, Var "y" ] )`


El intérprete debe:

- Evaluar argumentos estrictamente de izquierda a derecha
- Crear entornos para cada llamada
- Actualizar memoria en Assign
- Devolver el valor final y la memoria final.

**Resultado esperado**: 5

2. <font color="red">**Falta**</font> Realice un análisis sobre la elección del tipo de intérprete utilizado. Explique en qué situaciones o contextos considera que su elección resulta más adecuada, justificando en función de las características del lenguaje, la presencia de efectos, el modelo de evaluación y las necesidades del entorno o del entorno de ejecución.

><font color="#6564b3">**Solucion**</font>
>

---

## Ejercicio repacheje (OPCIONAL)

Sea el siguiente código de un lenguaje tipo Eiffel:

```text
if cond then stmt  
if cond then stmt else stmt  
if cond then if cond then stmt else stmt  
```

1. <font color="red">**Falta**</font> Definir una gramática que reconozca las expresiones anteriores.
2. <font color="red">**Falta**</font> ¿La gramática generada es LL(1)?
3. <font color="red">**Falta**</font> Calcule los conjuntos FIRST y FOLLOW de cada no terminal.
4. <font color="red">**Falta**</font> Muestre la tabla LL(1) y señale las celdas con conflictos.
5. <font color="red">**Falta**</font> Explique por qué ninguna gramática ambigua puede ser LL(1).
6. <font color="red">**Falta**</font> Proponga una gramatica no ambigua equivalente

><font color="#6564b3">**Solucion**</font>
>
