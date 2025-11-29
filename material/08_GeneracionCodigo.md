# Generación de Código

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
