# Resumen

## Intérpretes (store passing y evaluación)

![Interpretes-ej](./assets/Interpretes-ej.png)

### Forma Directa

```python
env = {}

def eval_stmt(stmt):
	if stmt["type"] == "assign":
		env[stmt["var"]] = eval_expr(stmt["expr"])
	elif stmt["type"] == "print":
		print(eval_expr(stmt["expr"]))

def eval_expr(expr):
	if expr["type"] == "num":
		return expr["value"]
	elif expr["type"] == "var":
		return env[expr["name"]]
	elif expr["type"] == "add":
		return eval_expr(expr["left"]) + eval_expr(expr["right"])
```

### Store Passing

```python
class Environment:
	def __init__(self, parent=None):
		self.parent = parent
		self.map = {}

	def lookup(self, name):
		if name in self.map:
			return self.map[name]
		elif self.parent:
			return self.parent.lookup(name)
		else:
			raise RuntimeError(f"Variable '{name}' not defined")

class Store:
	def __init__(self):
		self.memory = {}
		self.next_addr = 0

	def alloc(self, value):
		addr = self.next_addr
		self.memory[addr] = value
		self.next_addr += 1
		return addr

	def update(self, addr, value):
		self.memory[addr] = value

	def read(self, addr):
		return self.memory[addr]
```
```python
def eval_expr(expr, env, store):
    if expr["type"] == "num":
        return expr["value"], store
    elif expr["type"] == "var":
			addr = env.lookup(expr["name"])
			val = store.read(addr)
			return val, store
    elif expr["type"] == "add":
			v1, s1 = eval_expr(expr["left"], env, store)
			v2, s2 = eval_expr(expr["right"], env, s1)
			return v1 + v2, s2

def eval_stmt(stmt, env, store):
    if stmt["type"] == "assign":
			val, s1 = eval_expr(stmt["expr"], env, store)
			addr = env.lookup(stmt["target"])
			s1.update(addr, val)
			return s1
```

### Continuation-Passing Style - CPS

```python
def eval_expr(expr, env, k):
    if expr["type"] == "num":
        return k(expr["value"])
    elif expr["type"] == "add":
			return eval_expr(expr["left"], env, 
				lambda v1: eval_expr(expr["right"], env,
					lambda v2: k(v1 + v2)))

def eval_stmt(stmt, env, k):
    if stmt["type"] == "assign":
			return eval_expr(stmt["expr"], env,
				lambda val: k(env.update({stmt["var"]: val})))
    elif stmt["type"] == "print":
			return eval_expr(stmt["expr"], env,
				lambda val: (print(val), k(env))[1])
```

Ejemplo

```go
x := 5
y := x + 1
print(y)
```
```ini
k0 = λ_. print(y)
k1 = λ_. y := x + 1; k0()
k2 = λ_. x := 5; k1()
```

## Generación de Código Intermedio

Ejemplo de codigo fuente

```
c := a + b * 2
```

**Tres Direcciones** (Three Address Code – TAC) [Libro '6.2 Código de tres direcciones' pagina 389]

Características:

- Cada instrucción usa máximo 3 direcciones:
>`x = y op z`
- Introduce temporales.

Ejemplo:

![inf-tipos unificacion](./assets/tac-ej-ast.drawio.svg)

```
t1 := b
t2 := 2
t2 := t1 * t2
t1 := a
t1 := t1 + t2
c  := t1
```

**Cuádruplas**

```
(op, arg1, arg2, result)

(*,  b, 2,  t1)
(+,  a, t1, t2)
(:=, t2, -,  c)
```


- código intermedio
- código intermedio con etiquetas y saltos
- optimización de temporales
- gramática de atributos
- notación posfija (postfijo)
- mini–máquina de tres direcciones

## Tipos e Inferencia (Algoritmo , unificación)

Reglas de Inferencia

- (Const)
	> Γ ⊢ 5 : INTEGER

- (BinOp)
	```
	Γ ⊢ e1 : INTEGER    Γ ⊢ e2 : REAL
	----------------------------------
	Γ ⊢ e1 + e2 : REAL
	```

![inf-tipos reglas](./assets/inf-tipos-reglas-tipado.png)

![inf-tipos reglas](./assets/inf-tipos-reglas-tipado-ej1.png)

![inf-tipos reglas](./assets/inf-tipos-reglas-tipado-ej2.png)

![inf-tipos reglas](./assets/inf-tipos-reglas-tipado-ej3.png)

inf-tipos unificacion

![inf-tipos unificacion](./assets/inf-tipos-unificacion.png)

![inf-tipos unificacion Ej](./assets/inf-tipos-unificacion-ej.png)

Inferencia de tipos

![inf-tipos](./assets/inf-tipos.png)

![inf-tipos reglas](./assets/inf-tipos-reglas.png)

- Algoritmo de inferencia
- unificaciones
- Inferir tipo

## Análisis de Flujo de Datos (CFG(Control Flow Graph) y Reaching Definitions)

### Líderes y bloques básicos

Regla de líderes:  
Un líder es:
- La primera instrucción del programa
- El destino de un `goto` o `if`
- La instrucción siguiente a cualquier salto condicional o incondicional

Agrupo instrucciones desde un líder hasta el siguiente salto o líder.

### Grafo de Flujo

Reglas:
- Identificar Bloques (Algoritmo de Bloques)
	- Identificar Lideres
		1. Una instruccion es un lider
		2. Las instrucciones inmediatas a un condicional son lider
		3. La instruccion destino de un condicional es lider
	- 
- Sucesores y Predeesores (Precedencia)

Temas:
- bloques básicos
- definiciones alcanzables (Reaching Definitions RD)
- variables vivas  (Live Variables)
- propagación de constantes
- formato de conjunto IN/OUT
- convergencia
- análisis inverso (hacia atrás) para detectar variables muertas
- eliminar instrucciones muertas