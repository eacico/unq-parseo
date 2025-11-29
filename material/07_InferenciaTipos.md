# Inferencia de Tipos

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
