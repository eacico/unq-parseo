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

![LR(0)-AFD](./assets/LR(0)-AFD.drawio.svg)

### tabla ACTION/GOTO

|   | GOTO       ||| ACTION             |||||
|:--|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|   | E' | E | T | n         | +  | (  | )  | $  |
| 1 |    | 2 | 9 | S6        | | S5 |  |  |
| 2 |    |   |   |           | S3 |  |  | ACCEPT |
| 3 |    |   | 4 | S6        |  | S5 |  |  |
| 4 |    |   |   | E → E + T | E → E + T | E → E + T | E → E + T | E → E + T |
| 5 |    | 7 |   | S6        | S9 | S5 |  |  |
| 6 |    |   |   | T → n     | T → n | T → n | T → n | T → n |
| 7 |    |   |   |           |  |  | S8 |  |
| 8 |    |   |   | T → (E)   | T → (E) | T → (E) | T → (E) | T → (E) |
| 9 |    |   |   | E → T     | E → T | E → T | E → T | E → T |

Es LR(0) porque no hay conflictos (mas de una produccion por celda)

Conflicto Reduce/Reduce

![LR(0)-conflicto-reduce-reduce](./assets/LR(0)-conflicto-reduce-reduce.png)

Conflicto Shift/Reduce

![LR(0)-conflicto-reduce-reduce](./assets/LR(0)-conflicto-shift-reduce.png)

Uso de la tabla para armar la pila

![LR(0)-conflicto-reduce-reduce](./assets/LR(0)-uso-tabla.png)
