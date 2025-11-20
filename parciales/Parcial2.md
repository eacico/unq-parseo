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
S -> S ; S | Stmt | ε
Stmt -> ID := E | if E then Stmt
E -> E + T | T
T -> ID | NUM
```

a) ¿Qué puede decir acerca de la gramática presentada? Realice un análisis desde su perspectiva.  
b) Construya la versión **LR(0)** para la gramática presentada.  
c) Construya el autómata LR(0) de items.  
d) Justifique y realice un analisis de su perspectiva para las siguientes preguntas  
- ¿Cuales son las limitaciones del analizador LR(0)?
- ¿Cómo se puede mejorar un analizador LR(0)?

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

a) Construya el código intermedio (instrucciones)  
b) Genere código de **tres direcciones**  
c) Identifique los **líderes** y forme los bloques básicos completos.  
d) Construya el **grado de flujo de control** (CFG). ¿Qué puede decir de él?  
e) ¿Qué tipo de interpretación propondría para este fragmento de programa? Justifique su elección con un análisis de ventajas y desventajas asociadas a cada tipo de intérprete para el código dado.  

---

## Ejercicio 3

Dadas las siguientes expresiones:

```
if x=y then x=0 else x=Succ(0)
if x=y then y=f(x) else x=g(0)
if f x then Succ(x) else f(0)
```

a) Aplicar el algoritmo de inferencia de tipos sobre los siguientes términos, obteniendo así el juicio de tipoado más general posible que les asigna un tipo.  
b) En un lenguaje con tipos simples, ¿qué restricciones impone la operación de igualdad?  

Nota: `Succ` es una función del tipo `N->N`.

---

## Ejercicio 4:

1. Definir un intérprete:

```text
eval :: Expr -> [Definition] -> Env Addr -> Memory Int -> (Int, Memory Int)
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

2. Realice un análisis sobre la elección del tipo de intérprete utilizado. Explique en qué situaciones o contextos considera que su elección resulta más adecuada, justificando en función de las características del lenguaje, la presencia de efectos, el modelo de evaluación y las necesidades del entorno o del entorno de ejecución.

---

## Ejercicio repacheje (OPCIONAL)

Sea el siguiente código de un lenguaje tipo Eiffel:

```text
if cond then stmt  
if cond then stmt else stmt  
if cond then if cond then stmt else stmt  
```

1. Definir una gramática que reconozca las expresiones anteriores.
2. ¿La gramática generada es LL(1)?
3. Calcule los conjuntos FIRST y FOLLOW de cada no terminal.
4. Muestre la tabla LL(1) y señale las celdas con conflictos.
5. Explique por qué ninguna gramática ambigua puede ser LL(1).
6. Proponga una gramatica no ambigua equivalente