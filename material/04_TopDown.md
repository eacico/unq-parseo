# Top Down
Empieza de la raiz del arbol de analisis sintactico (`S`) y una cadena de entrada, y se busca armar el arbol de deribacion de arriba hacia abajo.  
Para aplicar las derivaciones suponemos tener un Oraculo que nos proporciona la derivacion correcta.

Ejemplo de **analisis sintactico descendente predictivo**

```
T → U
  | U ⇒ T
U → a
  | (T)
```

| Entrada | Pila | |
| :-------- | ------------: | :---- |
| `(a⇒a)⇒a` | T | Expandir |
| `(a⇒a)⇒a` | U ⇒ T | Expandir |
| `(a⇒a)⇒a` | (T) ⇒ T | Consumir |
|  |
| `a⇒a)⇒a` | T) ⇒ T | Expandir |
| `a⇒a)⇒a` | U ⇒ T) ⇒ T | Expandir |
| `a⇒a)⇒a` | a ⇒ T) ⇒ T | Consumir |
|  |
| `⇒a)⇒a` | ⇒ T) ⇒ T | Consumir |
|  |
| `a)⇒a` | T) ⇒ T | Expandir |
| `a)⇒a` | U) ⇒ T | Expandir |
| `a)⇒a` | a) ⇒ T | Consumir |
|  |
| `)⇒a` | ) ⇒ T | Consumir |
|  |
| `⇒a` | ⇒ T | Consumir |
|  |
| `a` | T | Expandir |
| `a` | U | Expandir |
| `a` | a | Consumir |
|  |
| ε | ε | |

La cadena es aceptada porque tanto la pila como la cadena a procesar redujeron a ε.  
Falla en el caso que la entrada o la pila quede vacia pero la otra no.

## Backtracking

Si utilizo un algoritmo sin oraculo para decidir si una cadena es aceptada por la gramatica, el backtracking es la tecnica de analizar una rama del arbol de derivacion y si falla (la produccion no acepta la cadena) volver al ultimo punto que la cadena era aceptada y continuar verificando por otra produccion (otra rama).  
Usando backtracking el parser se puede colgar con gramaticas que tengan recursion a izquierda. Ej: `S → a | S + a`

## FIRST / FOLLOW
>Fuente: 4.4.2 PRIMERO y SIGUIENTE [pagina 220]  

**FIRST** (terminal y no terminal)  
- Si `x` es terminal `FIRST(x) = {x}`
- Si `X` es no terminal   
1. B → αAβ  
   FIRST(B) = FIRST(α)  
2. B → Aβ  
   FIRST(B) = FIRST(A) - {ε}  
   - Si &emsp; ε ∊ FIRST(A)  
     FIRST(B) += FIRST(β) 

**FOLLOW** (no terminal)  
1. Si S es estado inicial agrego $ a FOLLOW(S)  
   FOLLOW(A) += { \$ }
2. B → αAβ  
   FOLLOW(A) = FIRST(β) - {ε}  
   - B → αA &emsp; o &emsp; B → αAβ y β *⇒ ε &emsp; o &emsp; ε ∊ FIRST(β)  
   FOLLOW(A) += FOLLOW(B)

Ejemplo  

**No Terminales**:  
`{ id, int, bool, ⇒, ;, (, ) }`

<table>
<tr><th></th><th>FIRST</th><th></th></tr>

<tr><td style="vertical-align: top;">

```
S  → VS  
   | ε  
V  → D id;  
D  → T  
   | ε  
T  → UT'  
T' → ⇒ UT'  
   | ε  
U  → int  
   | bool  
   | (T)
```

</td><td style="vertical-align: top;">

```
FIRST(V) + { ε }

{ id } + FIRST(D) - {ε}
FIRST(T) + {ε}

FIRST(U)
{ ⇒, ε }

{ int, bool, ( }


```

</td><td style="vertical-align: top;">

```
S: { id, int, bool, (, ε }

V: { id, int, bool, ( }
D: { int, bool, (, ε }

T: { int, bool, ( }
T': { ⇒, ε }

U: { int, bool, ( }


```

</td></tr></table>


<table>
<tr><th></th><th>FIRST</th><th>FOLLOW</th><th></th></tr>

<tr><td style="vertical-align: top;">

```
S  → VS  
   | ε  
V  → D id;  
D  → T  
   | ε  
T  → UT'  
T' → ⇒ UT'  
   | ε  
U  → int  
   | bool  
   | (T)
```

</td><td style="vertical-align: top;">

```
S: { id, int, bool, (, ε }

V: { id, int, bool, ( }
D: { int, bool, (, ε }

T: { int, bool, ( }
T': { ⇒, ε }

U: { int, bool, ( }


```

</td><td style="vertical-align: top;">

```
{ $ }

FIRST(S) + FOLLOW(S)
{ id }

{ ) } + FOLLOW(D)
FOLLOW(T)

FIRST(T')
  + FOLLOW(T)

```

</td><td style="vertical-align: top;">

```
S: { $ }

V: { id, int, bool, (, $ }
D: { id }

T: { ), id }
T': { ), id }

U: { ⇒, ), id }


```

</td></tr></table>

## Tabla LL(1)
	Sea una producción A → α
		Si FIRST(α) = {a}:
			M[A, a] = A → α
		Si ε ∊ FIRST(α), busco FOLLOW(A) = {b}:
			M[A, b] = A → α
		Si en algún momento intentas poner dos producciones distintas en la misma celda M[A, t], tienes conflicto → la gramática no es LL(1).

### Precondiciones
1. **Simplificar**
2. **Eliminar recursión izquierda** (obligatorio)
3. **Factorizar** (obligatorio si hay prefijos comunes)

### Armar Tabla
B → Aβ | ε  
A → α  

Para armar la fila de B
- B → Aβ  
  - En las columnas de **FIRST(A)** usar la produccion **B → Aβ**  
- B → ε  
  - En las columnas de **FOLLOW(B)** usar la produccion **B → ε**  

|    | α | β | $ | 
|:---|:--:|:--:|:--:|
| B  | B → Aβ |  | B → ε |
| A  | A → α |  |  |


Ejemplo:  

|    | id | int | bool | ⇒ | ( | ) | ; | $ | 
|:---|:--:|:--: |:--: |:--:|:--:|:--:|:--:|:--:|
| S  | VS | VS | VS |  | VS |  |  | ε | 
| V  |  | D id; | D id; |  | D id; |  |  |  | 
| D  | ε | T | T |  | T |  |  |  | 
| T  |  | UT' | UT' |  | UT' |  |  |  | 
| T' | ε |  |  | ⇒ UT' |  | ε |  |  | 
| U  |  | int | bool |  | (T) |  |  |  | 

### Usar Tabla

| Entrada | Pila | |
| :-------- | ------------: | :---- |
| `int ⇒ int id;` | S | M[S,int] = S → VS |
| `int ⇒ int id;` | VS | M[V,int] = V → D id;|
| `int ⇒ int id;` | D id;S | M[D,int] = D → T|
| `int ⇒ int id;` | T id;S | M[T,int] = T → UT'|
| `int ⇒ int id;` | UT' id;S | M[U,int] = U → int|
| `int ⇒ int id;` | int T' id;S |  |
| `⇒ int id;` | T' id;S | M[T',⇒] = T' → ⇒ UT'|
| `⇒ int id;` | ⇒ UT' id;S | |
| `int id;` | UT' id;S | M[U,int] = U → int|
| `int id;` | int T' id;S | |
| `id;` | T' id;S | M[T',id] = T' → ε|
| `id;` | id;S ||
| `;` | ;S ||
| ε | S | M[S,ε] = S → ε |
| ε | ε | ACCEPT |

### Validar que una gramatica no es LL(1)
- Armar FIRST de todos los simbolos
- Armar FOLLOW de todos los simbolos
- Armar tabla
- Si en alguna celda de la tabla quedan 2 o mas producciones no es LL(1)

Ejemplo:
```
S → if E then S  
  | if E then S else S  
  | cmd  
E → exp  
```
En este ejemplo se puede ver que para `M[S,if]` van a existir 2 producciones:
- S → if E then S  
- S → if E then S else S

### Hacer gramatica LL(1)
- **Eliminar recursión izquierda**  
Identifica y elimina las reglas de producción recursivas en el lado izquierdo de otras reglas de la gramática. Esto es un paso crucial porque las gramáticas recursivas con recursión izquierda no son LL(1).  
- **Factorización**  
Si un no terminal tiene múltiples producciones que comienzan con el mismo símbolo terminal, se agrupan bajo una nueva producción con un nuevo no terminal. Esto se hace para evitar la ambigüedad.
- **Calcular los conjuntos First y Follow**
- **Construir la tabla LL(1)**
- **Verificar si es LL(1)**