# Lenguajes Regulares


## Gramatica ambigüa
>**Fuente**: 2.2.4 Ambigüedad ... 47

Para mostrar que una gramática es ambigua, todo lo que debemos hacer es buscar una cadena de terminales que sea la derivación de más de un árbol de análisis sintáctico.

Ejemplo 2.5:  
`cadena → cadena + cadena | cadena − cadena | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9`

<table>
<tr>
<td>

```
          cadena
        /     |  \
    cadena    + cadena
    /  |  \        |
cadena - cadena    2
    |        |
    9        5
```

</td>
<td>

```
    cadena
    /   |  \
cadena  -  cadena
    |     /  |  \
    9 cadena + cadena
        |        |
        5        2
```

</td>
</tr>
</table>

>**Fuente**: 4.2.5 Ambigüedad ... 203

Una gramática ambigua es aquella que produce más de una derivación por la izquierda, o más de una derivación por la derecha para el mismo enunciado.
	
>**Fuente**: 4.3.2 Eliminación de la ambigüedad ... 210

G(V,L,T,S) si existe algun w(arbol de derivacion) ∊ L(G) con al menos una de los siguientes escenarios:
- 2 derivaciones mas a la izquierda distintas
- 2 derivaciones mas a la derecha distintas
- 2 arboles de derivacion distintos


## Definiciones

<table><tr><td style="vertical-align: top;">

**Variables Positiva**  
&emsp; A \*⇒ w &emsp; A ∊ V &emsp; w ∊ T\*

**Variables Alcanzable**  
&emsp; S \*⇒ αAβ &emsp; A ∊ V &emsp; α,β ∊ (V ∪ T)\*

**Variables Util**  
&emsp; S \*⇒ αAβ \*⇒ w &emsp; A ∊ V &emsp; w ∊ T\* &emsp; α,β ∊ (V ∪ T)\*

>Nota: Util ⟾ Positiva y Alcanzable &emsp; (Pero no al revez)

</td><td></td><td style="vertical-align: top;">

**Producciones Unitarias**  
&emsp; A → B &emsp; A, B ∊ V 

**Producciones Epsilon**  
&emsp; A → ɛ &emsp; A ∊ V 

**Variables Nullables**  
&emsp; A \*⇒ ɛ &emsp; A ∊ V

</td></tr></table>

## Gramatica Simplificada
	es una gramatica G=(V,T,P,S) donde:
		- todas sus variables son Utiles
			S *=> αAβ *=> w    A ∊ V    w ∊ T*    α,β ∊ (V ∪ T*)
		- no tiene producciones Unitarias
			A -> B
		- no tiene producciones epsilon
			A -> ε

### Simplificar
1) **Eliminacion de producciones epsilon**  
  >>**Producciones Epsilon**: &emsp; A → ɛ &emsp; A ∊ V  
  >
  >>X<sub>*i*</sub> → ɛ ∊ P  
  >>A → X<sub>*1*</sub>, X<sub>*2*</sub>, ... , X<sub>*i-1*</sub>, X<sub>*i*</sub>, X<sub>*i+1*</sub>, ... , X<sub>*n-1*</sub>, X<sub>*n*</sub> ∊ P  
  >>P ← P ∪ { A → X<sub>*1*</sub>, X<sub>*2*</sub>, ... , X<sub>*i-1*</sub>, X<sub>*i+1*</sub>, ... , X<sub>*n-1*</sub>, X<sub>*n*</sub> }  
  >>P ← P - { X<sub>*i*</sub> → ɛ }  
  >
  >Ejemplo:
  ><table><tr><td style="vertical-align: top;">
  >
  >X → αYβ  
  >Y → ɛ
  >
  >X → αβ
  >
  ></td><td></td><td style="vertical-align: top;">
  >
  >X → αY  
  >Y → Yβ | ɛ
  >
  >X → αY | α  
  >Y → Yβ | β
  >
  ></td><td></td><td style="vertical-align: top;">
  >
  >E → aEb | a**F**  
  >F → a**F**b | **ɛ**  
  >
  >E → aEb | aF | **a**  
  >F → aFb | **ab**  
  >
  ></td></tr></table>

2) **Eliminacion de producciones Unitarias**  
  >>**Producciones Unitarias**: &emsp; A → B &emsp; A, B ∊ V
  >
  >Ejemplo:
  ><table><tr><td style="vertical-align: top;">
  >
  >X → αZβ | **Y**  
  >Y → αZ  
  >
  >X → αZβ | **αZ**
  >
  ></td><td></td><td style="vertical-align: top;">
  >
  >S → aaA | aS | **E** | bA | BD  
  >A → aaA | **D**  
  >D → Db | aA  
  >E → aEb | aF | a  
  >
  >S → aaA | aS | **aEb | aF | a** | bA | BD  
  >A → aaA | **Db | aA**  
  >
  ></td></tr></table>

3) **Eliminar valiables NO Positivas**  
  >>**Variables Positivas**: &emsp; A \*⇒ w &emsp; A ∊ V &emsp; w ∊ T\*
  >
  >POS ← { A / A → w ∊P &emsp; w ∊T\*}  
  >A ∉ POS ∧ A → α ∊ P ∧ α ∊ (POS ∪ T)\*  
  >&emsp; POS ← POS ∪ { A }
  >
  >Ejemplo:
  ><table><tr><td style="vertical-align: top;">
  >
  >S → **aaA** | aS | **bA** | **BD** | aEb | aF | a  
  >**A → aaA | Db | aA**  
  >B → Bbb | bb  
  >C → bC | b  
  >**D → Db | aA**  
  >E → aEb | aF | a  
  >F → aFb | ab  
  >
  >POS = {F,E,C,B,S}
  >
  ></td><td></td><td style="vertical-align: top;">
  >
  >S → aS | aEb | aF | a  
  >B → Bbb | bb  
  >C → bC | b  
  >E → aEb | aF | a  
  >F → aFb | ab  
  >
  ></td></tr></table>

4) **Eliminar valiables NO Alcanzables**  
  >>**Variables Alcanzable**: &emsp; S \*⇒ αAβ &emsp; A ∊ V &emsp; α,β ∊ (V ∪ T)\*  
  >
  >Ejemplo:
  ><table><tr><td style="vertical-align: top;">
  >
  >S → aS | aEb | aF | a  
  >**B → Bbb | bb**  
  >**C → bC | b**  
  >E → aEb | aF | a  
  >F → aFb | ab  
  >
  >ALC= {S, E, F}
  >
  ></td><td></td><td style="vertical-align: top;">
  >
  >S → aS | aEb | aF | a  
  >E → aEb | aF | a  
  >F → aFb | ab  
  >
  ></td></tr></table>

## Eliminar Recurcion a Izquierda

Ejemplo  
Lenguaje: `cb*`  
A → Ab | c

A → cA'  
A' → ɛ | bA'

Ejemplo  
S → Ab | c  
A → d | Sf | Ag

- Ordenar simbolos no terminales  
  S,A
1. Eliminar las producciones de `S` que comienzan con un simbolo anterior a `S`  
No hay
2. Eliminar las producciones de `A` que comienzan con un simbolo anterior a `A`  
S → Ab | c  
A → d | Abf | cf | Ag  
- Eliminar recursion directa.  
Primero dejo las producciones sin recursion directa y les agrego al final la variable prima de la regla.  
Luego a las producciones con recursion las paso como producciones de la variable prima quitandole la variable original y poniendo la variable prima al final.  
Por ultimo agrego la produccion ε a la variable prima.  
S → Ab | c  
A → Abf | Ag | d | cf  
⇒  
S → Ab | c  
A → dA' | cfA'  
A' → ε | bfA' | gA'

## Eliminar Ambigüedad
- **Eliminar recursión izquierda**  
- **Factorización por la izquierda**  
Si un no terminal tiene múltiples producciones que comienzan con el mismo símbolo terminal, se agrupan bajo una nueva producción con un nuevo no terminal. Esto se hace para evitar la ambigüedad.  
S → **if E then S** | **if E then S** else S | a  
E → b  
⇒  
S  → **if E then S** S' | a  
S' → else S | ε  
E  → b  

## Teorema General de Simplificacion


## Forma Normal de Chomsky (FNC)
Se dice que una gramática está en Forma Normal de Chomsky (FNC) si toda producción es de la forma A → BC o de la forma A → a, en donde A, B y C son no terminales, y a es un terminal.  
La producción S → ε está permitida solo para el símbolo de inicio S, y solo si la cadena vacía ε es parte del lenguaje que la gramática genera.  
No se permiten producciones que mezclen símbolos terminales y no terminales en el lado derecho, como A → aB.
No se permiten producciones de 3 o mas simbolos del lado derecho.  
```
A → BC
A → a
```
Ejemplo:
```
S → AB
A → 0
B → 1 | SC
C → 1
```

### Pasos
1. Simplificar  
    - eliminar prod ε
    - Eliminar prod unitarias
    - Eliminar prod inutiles
2. Pasar a FNC  
    - Sustituir terminales
    - Sustituir producciones >= 3

## Forma Normal de Greibach (FNG)
		A → α
	Ejemplo:
		S → 0SB
		S → 0B
		B → 1