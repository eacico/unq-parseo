# Analisis Estatico

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