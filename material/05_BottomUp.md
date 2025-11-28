# Bottom Up

## Bottom-Up

  Shift
    Cuando leo un caracter de la entrada
  Reduce
    Cuando transformo la cadena procesada aplicando una produccion que la defina

Ej: Usar el algoritmo para el analisis sintactico ascendente con la gramatica G=({E,T,F},{+,*,n,(,)},P,E):
```
  E → T | E + T
  T → F | T * F
  F → n | (E) 
```
para la entrada `n*n+n`

| Pila | Entrada |  |
| :-------- | ------------: | :---- |
|  | `n*n+n` | Shift |
| `n` | `*n+n` | Reduce |
| `F` | `*n+n` | Reduce |
| `T` | `*n+n` | Shift |
| `T*` | `n+n` | Shift |
| `T*n` | `+n` | Reduce |
| `T*F` | `+n` | Reduce |
| `T` | `+n` | Reduce |
| `E` | `+n` | Shift |
| `E+` | `n` | Shift |
| `E+n` | `$` | Reduce |
| `E+F` | `$` | Reduce |
| `E+T` | `$` | Reduce |
| `E` | `$` | Accept |

## LR(0)

### Precondiciones

1. **Simplificación** (opcional, ayuda a tener tablas más limpias)

NO se debe:
  - eliminar recursión por la izquierda
  - factorizar

### Closure

Ej: 
```
  E' → E$
  E → T | E + T
  T → n | (E) 
```


```
  I 		= { E' → •E$ }
  I' 		= { E' → •E$ , E → •T , E → •E + T}
  I'' 	= { E' → •E$ , E → •T , E → •E + T , T → •n , T → •(E)}
  I''' 	= I''
```

`Clausura (I) = I''`

### AFD para LR(0)

![LR(0)-AFD](./assets/05-LR(0)-AFD.drawio.svg)

### Tabla ACTION/GOTO
Teniendo los Items armados puedo armar la tabla con los siguientes pasos:  
1. Armar estructura de la tabla con:
    - Filas: descripcion de los **Items** definidos
      - Nota: Omitir la fila del estado de aceptacion
    - Columnas: Separarlas en 2 grupos
      - Los **No Terminales** correspondientes al grupo **GOTO**
      - Los **Terminales** (incluyendo `$`) correspondientes al grupo **ACTION**
2. Completar todas las celdas usando las reglas de transicion definidas por el automata. Para las reglas qye reciban un simbolo **terminal** indicar que se hace un **Shift** al nuevo estado.
3. Para los estados que tengan solo una produccion con el cursos al final, escribir en todas las celdas de **ACTION** la produccion a aplicar.

|   | GOTO   || ACTION             |||||
|:--|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|   | E  | T  | n         | +  | (  | )  | $  |
| 1 | 2  | 9  | S6        | | S5 |  |  |
| 2 |    |    |           | S3 |  |  | ACCEPT |
| 3 |    | 4  | S6        |  | S5 |  |  |
| 4 |    |    | E → E + T | E → E + T | E → E + T | E → E + T | E → E + T |
| 5 | 7  |    | S6        | S9 | S5 |  |  |
| 6 |    |    | T → n     | T → n | T → n | T → n | T → n |
| 7 |    |    |           |  |  | S8 |  |
| 8 |    |    | T → (E)   | T → (E) | T → (E) | T → (E) | T → (E) |
| 9 |    |    | E → T     | E → T | E → T | E → T | E → T |

Es LR(0) porque no hay conflictos (mas de una produccion por celda)

Conflicto Reduce/Reduce

![LR(0)-conflicto-reduce-reduce](./assets/05-LR(0)-conflicto-reduce-reduce.png)

Conflicto Shift/Reduce

![LR(0)-conflicto-reduce-reduce](./assets/05-LR(0)-conflicto-shift-reduce.png)

Uso de la tabla para armar la pila

![LR(0)-conflicto-reduce-reduce](./assets/05-LR(0)-uso-tabla.png)
