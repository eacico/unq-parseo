# Ejercicios Práctica 2

## Sección 1: Técnica Bottom-Up (LR, SLR, LALR, LR(1))

1. <font color="red">**[FALTA]**</font> Construir la colección completa de items LR(0) para la gramática: S → E; E → E + T | T; T → T * F | F; F → (E) | id. Determinar si LR(0) admite la gramática.

2. <font color="red">**[FALTA]**</font> Diseñar la tabla SLR(1) para la gramática anterior, calcular FIRST/FOLLOW y justificar cada entrada.

3. <font color="red">**[FALTA]**</font> Mostrar paso a paso (pila, entrada, acción) el parseo shift–reduce de `id + id * id` usando la tabla SLR construida.

4. <font color="red">**[FALTA]**</font> Construir la colección canónica LR(1) (items con lookahead) para la gramática de expresiones y comparar número de estados con LR(0).

5. <font color="red">**[FALTA]**</font> Dar un ejemplo de gramática que sea LALR(1) pero no LR(0); construir la tabla LALR(1) y explicar la diferencia.

6. <font color="red">**[FALTA]**</font> Dado un autómata LR(0) con un conflicto shift/reduce, aplicar SLR(1) y explicar si el conflicto se resuelve (calcular FOLLOW).

7. <font color="red">**[FALTA]**</font> Transformar la gramática `S → A a | b A c | d c | b d a` a una forma adecuada para análisis LR y construir la tabla ACTION/GOTO.

8. <font color="red">**[FALTA]**</font> Diseñar una gramática para declaraciones `if-then-else` y demostrar cómo el parseo bottom-up resuelve el dangling else; construir tabla SLR o LALR.

9. <font color="red">**[FALTA]**</font> Implementar en pseudocódigo el algoritmo de construcción de closure/goto para items LR(0) y probarlo en la gramática de expresiones.

10. <font color="red">**[FALTA]**</font> Dada una gramática con left-recursion indirecta, explicar y aplicar una transformación que permita su análisis bottom-up sin cambiar el lenguaje.

11. <font color="red">**[FALTA]**</font> Para la gramática `E → E ^ E | E * E | E + E | id`, proponer una refactorización que determine precedencias y que sea LR(1).

12. <font color="red">**[FALTA]**</font> Analizar la complejidad (número de estados) al pasar de LR(0) a LR(1) para una gramática con muchas producciones similares.

13. <font color="red">**[FALTA]**</font> Construir un ejemplo donde LALR(1) cause errores si se fusionan estados LR(1) indiscriminadamente; explicar la causa.

14. <font color="red">**[FALTA]**</font> Diseñar ejercicios de test (con cadenas) que validen exhaustivamente una tabla SLR(1) pequeña; explicar criterios de cobertura.

15. <font color="red">**[FALTA]**</font> Implementar un verificador automático que valide si una tabla ACTION/GOTO generada es consistente con la gramática dada.

16. <font color="red">**[FALTA]**</font> Mostrar cómo factorizar la gramática `S→if E then S else S | if E then S | stmt` para facilitar el análisis bottom-up y construir la tabla.

17. <font color="red">**[FALTA]**</font> Generar la Máquina de estados LR(0) para la gramática `S→L=R | R; R→L | *R | id` (lista de declaraciones) y explicar cada transición.

18. <font color="red">**[FALTA]**</font> Analizar la afectación de la ambigüedad en la construcción de items LR(0): muestra un ejemplo ambigua y su impacto en ACTION.

19. <font color="red">**[FALTA]**</font> Diseñar una gramática que acepte expresiones con operadores binarios y unario y construir la tabla SLR(1) indicando cómo tratar el operador unario.

20. <font color="red">**[FALTA]**</font> Dado un parser bottom-up, explicar cómo integrarle manejo de errores de forma elegante (p. ej. inserción/sincronización) y dar ejemplos.

21. <font color="red">**[FALTA]**</font> Analizar el impacto de left-factoring en la reducción de conflictos SLR y en el número de estados LR(0).

22. <font color="red">**[FALTA]**</font> Dado un conjunto de items, identificar estados que pueden ser fusionados para LALR y justificar la fusión.

23. <font color="red">**[FALTA]**</font> Diseñar una gramática para arrays y accesos `a[i]` y construir la tabla LALR(1) mínima que la acepte.

24. <font color="red">**[FALTA]**</font> Construir un ejemplo donde SLR(1) falla pero LR(1) tiene éxito; explicar el porqué en términos de FOLLOW y lookahead.

## Sección 2: Intérpretes (AST, ejecución, diseño)

25. <font color="red">**[FALTA]**</font> Diseñar un intérprete recursivo en pseudocódigo para expresiones aritméticas con variables y asignaciones; incluir manejo de entorno.

26. <font color="red">**[FALTA]**</font> Dado un AST para `if (a>b) then x:=x+1 else x:=x-1`, escribir la función eval que ejecute correctamente la sentencia.

27. <font color="red">**[FALTA]**</font> Extender un intérprete para soportar funciones con ámbito léxico y closures; demostrar con ejemplo de función anidada.

28. <font color="red">**[FALTA]**</font> Implementar manejo de excepciones (raise/catch) en un intérprete; explicar la semántica y el paso de control.

29. <font color="red">**[FALTA]**</font> Diseñar un intérprete que haga evaluación perezosa (lazy) para expresiones; mostrar diferencias con evaluación estricta.

30. <font color="red">**[FALTA]**</font> Construir un intérprete que ejecute sentencias concurrentes (threads ligeros); explicar sincronización de entorno.

31. <font color="red">**[FALTA]**</font> Añadir profiling al intérprete para contar tiempo de ejecución de funciones; proponer cómo minimizar overhead.

32. <font color="red">**[FALTA]**</font> Implementar optimización en el intérprete: memoización de funciones puras y demostrar con ejemplos.

33. <font color="red">**[FALTA]**</font> Diseñar una representación del AST en Eiffel y escribir el pseudocódigo del método `eval` para nodos binarios.

34. <font color="red">**[FALTA]**</font> Dado una especificación de paso por referencia vs valor, diseñar el comportamiento del intérprete y mostrar diferencias.

35. <font color="red">**[FALTA]**</font> Diseñar un intérprete que soporte continuaciones (call/cc estilo Scheme); explicar su implementación y casos de uso.

36. <font color="red">**[FALTA]**</font> Añadir trazado y depuración interactiva al intérprete (breakpoints, inspección de variables) y justificar diseño.

37. <font color="red">**[FALTA]**</font> Implementar recolección de basura simple en el intérprete y mostrar cómo integrar la liberación de memoria con el AST.

38. <font color="red">**[FALTA]**</font> Diseñar un intérprete que soporte macros de tiempo de compilación y explique cómo se integran con parseo.

39. <font color="red">**[FALTA]**</font> Crear un mini-lenguaje con tipos dinámicos y diseñar su intérprete, mostrando chequeo dinámico de tipos.

40. <font color="red">**[FALTA]**</font> Implementar un intérprete para expresiones booleanas con cortocircuito y demostrar su evaluación en ejemplos complejos.

41. <font color="red">**[FALTA]**</font> Diseñar la semántica de un lenguaje con operadores sobrecargados y escribir el manejador en el intérprete.

42. <font color="red">**[FALTA]**</font> Extender un intérprete para soportar genéricos (templates) y discutir cómo afecta al tiempo de ejecución.

43. <font color="red">**[FALTA]**</font> Crear un intérprete que genere traza de ejecución en formato JSON para integrarse con herramientas externas.

44. <font color="red">**[FALTA]**</font> Diseñar un intérprete seguro (sandbox) para ejecutar código de usuario; identificar vectores de ataque y mitigaciones.

45. <font color="red">**[FALTA]**</font> Implementar un intérprete que realice optimizaciones JIT sencillas (e.g., inlining de funciones pequeñas) y analizar su beneficio.

46. <font color="red">**[FALTA]**</font> Diseñar un esquema de despliegue para un intérprete embebido en una aplicación y explicar restricciones de memoria.

47. <font color="red">**[FALTA]**</font> Proponer cómo instrumentar un intérprete para análisis de cobertura de código y diseñar casos de prueba.

48. <font color="red">**[FALTA]**</font> Diseñar un intérprete que soporte programación por contratos (pre/postconditions) e implementar checks en tiempo de ejecución.

## Sección 3: Inferencia de tipos (Hindley-Milner, unificación, polimorfismo)

49. <font color="red">**[FALTA]**</font> Aplicar el algoritmo de unificación para inferir tipos en la expresión `let f = \x -> x in f 3` (Hindley–Milner).

50. <font color="red">**[FALTA]**</font> Diseñar reglas de tipado para let-polymorphism e inferir tipos en `let id = \x -> x in (id, id 3)`.

51. <font color="red">**[FALTA]**</font> Dado un conjunto de ecuaciones de tipo, resolverlas por unificación y justificar el orden de sustituciones.

52. <font color="red">**[FALTA]**</font> Implementar en pseudocódigo el algoritmo W (Hindley–Milner) y aplicar a un ejemplo con funciones recursivas.

53. <font color="red">**[FALTA]**</font> Mostrar cómo detectar errores de tipo en `f x = x + True` y explicar el mensaje de error producido por la unificación.

54. <font color="red">**[FALTA]**</font> Diseñar un sistema de tipos que soporte subtipado simple y demostrar inferencia en presencia de herencia.

55. <font color="red">**[FALTA]**</font> Inferir tipos en una función con múltiples cláusulas por patrón (pattern matching) y explicar el proceso.

56. <font color="red">**[FALTA]**</font> Explicar cómo la inferencia maneja tipos mutables (referencias) y proponer restricciones necesarias.

57. <font color="red">**[FALTA]**</font> Diseñar casos donde la inferencia produce tipos polimórficos y explicar la generalización en let-bindings.

58. <font color="red">**[FALTA]**</font> Aplicar inferencia de tipos a una función que devuelve funciones (`compose f g x = f (g x)`) y mostrar pasos.

59. <font color="red">**[FALTA]**</font> Analizar la complejidad del algoritmo de unificación en términos del tamaño del término de tipo.

60. <font color="red">**[FALTA]**</font> Diseñar una extensión de HM con tipos de rango (rank-2) y dar ejemplos donde HM simple falla.

61. <font color="red">**[FALTA]**</font> Proponer un sistema de inferencia para un lenguaje con tipos algebraicos y deducir tipos en ejemplos.

62. <font color="red">**[FALTA]**</font> Implementar comprobación de tipos para expresiones aritméticas mixtas (Int/Float) con coerciones implícitas.

63. <font color="red">**[FALTA]**</font> Resolver un caso con tipos recursivos (listas homogéneas) y demostrar unificación con occurr-check.

64. <font color="red">**[FALTA]**</font> Diseñar tests que provoquen generalización indebida y explicar cómo evitarlo (value restriction).

65. <font color="red">**[FALTA]**</font> Inferir tipos en una función con parámetros opcionales y sobrecarga, proponiendo reglas de desambiguación.

66. <font color="red">**[FALTA]**</font> Aplicar inferencia en presencia de módulos/namespaces y explicar cómo restringir generalización entre módulos.

67. <font color="red">**[FALTA]**</font> Construir un sistema de tipado para un lenguaje con traits/mixins y mostrar inferencia en un ejemplo complejo.

68. <font color="red">**[FALTA]**</font> Dado un fragmento en pseudo-Eiffel sin anotaciones, inferir tipos locales y justificar decisiones.

69. <font color="red">**[FALTA]**</font> Diseñar un algoritmo para inferir tipos en expresiones lambda con anotaciones parciales del usuario.

70. <font color="red">**[FALTA]**</font> Mostrar cómo integrar inferencia de tipos con el flujo de datos para permitir optimizaciones basadas en tipos.

71. <font color="red">**[FALTA]**</font> Discutir limitaciones de Hindley–Milner ante efectos (IO, estado) y proponer soluciones prácticas.

72. <font color="red">**[FALTA]**</font> Aplicar el algoritmo de unificación para inferir tipos en la expresión `let f = \x -> x in f 3` (Hindley–Milner).

## Sección 4: Generación de código intermedio (3-address code, SDT, temporales)

73. <font color="red">**[FALTA]**</font> Generar código de tres direcciones (quadruples) para la expresión `a = (b + c) * (d - e)` y optimizar temporales.

74. <font color="red">**[FALTA]**</font> Transformar una sentencia `if-then-else` en código intermedio con etiquetas y saltos condicionales.

75. <font color="red">**[FALTA]**</font> Producir código intermedio para un bucle `for` y mostrar la estructura básica de control traducida.

76. <font color="red">**[FALTA]**</font> Diseñar SDT (S-attributed) que genere temporales para expresiones en un parser bottom-up.

77. <font color="red">**[FALTA]**</font> Convertir un AST en forma postorder a código de tres direcciones y proponer esquema de nombrado de temporales.

78. <font color="red">**[FALTA]**</font> Introducir short-circuit para `&&`/`||` en la generación de código intermedio y mostrar ejemplo.

79. <font color="red">**[FALTA]**</font> Diseñar la representación en memoria de estructuras (records) y generar acceso a campos en código intermedio.

80. <font color="red">**[FALTA]**</font> Generar código intermedio para llamada a función con paso de parámetros por pila y retorno por registro.

81. <font color="red">**[FALTA]**</font> Implementar generación de código intermedio para excepciones (try/catch) con tablas de manejo.

82. <font color="red">**[FALTA]**</font> Generar código intermedio en SSA para `a = b + c; d = a * e; a = a + 1` y mostrar conversión a SSA.

83. <font color="red">**[FALTA]**</font> Diseñar un esquema para temporales reutilizables y analizar su impacto en la asignación de registros posterior.

84. <font color="red">**[FALTA]**</font> Generar código intermedio para acceso a arrays con verificación de límites y explicar costo añadido.

85. <font color="red">**[FALTA]**</font> Traducir llamadas recursivas a código intermedio que utilice stack frames y temporales locales.

86. <font color="red">**[FALTA]**</font> Proponer un conjunto de instrucciones intermedias atómicas que simplifiquen la optimización común.

87. <font color="red">**[FALTA]**</font> Diseñar la traducción para expresiones de cadenas y concatenación en código tres-direcciones.

88. <font color="red">**[FALTA]**</font> Crear una SDT que genere código intermedio para sentencias compuestas (begin...end) manteniendo orden.

89. <font color="red">**[FALTA]**</font> Generar código intermedio con manejo de booleanos como enteros (0=false, ≠0=true) y discutir limitaciones.

90. <font color="red">**[FALTA]**</font> Diseñar transformaciones para convertir código intermedio a una forma adecuada para análisis de flujo (basic blocks).

91. <font color="red">**[FALTA]**</font> Generar código intermedio para operaciones de casting entre tipos (Int↔Float) considerando precisión y temporales.

92. <font color="red">**[FALTA]**</font> Implementar un algoritmo que minimice el número de temporales en la generación inicial (heurística local).

93. <font color="red">**[FALTA]**</font> Diseñar la representación intermedia para closures y generar el código que crea y llama a un closure.

94. <font color="red">**[FALTA]**</font> Generar código intermedio para destructores/RAII en presencia de excepciones y retornar limpio.

95. <font color="red">**[FALTA]**</font> Crear ejemplos donde la ordenación de instrucciones en código intermedio afecte la posibilidad de optimización futura.

96. <font color="red">**[FALTA]**</font> Generar código de tres direcciones (quadruples) para la expresión `a = (b + c) * (d - e)` y optimizar temporales.

## Sección 5: Análisis estático y optimización (CFG, dataflow, optimizaciones)

97. <font color="red">**[FALTA]**</font> Construir el grafo de flujo de control (CFG) para una función que contiene if/else y while.

98. <font color="red">**[FALTA]**</font> Calcular reaching definitions para cada bloque básico en un ejemplo dado y mostrar cómo se usan.

99. <font color="red">**[FALTA]**</font> Aplicar análisis de live variables y proponer eliminaciones de código muerto en un fragmento.

100. <font color="red">**[FALTA]**</font> Implementar en papel el algoritmo de dominadores para un CFG y determinar el dominador inmediato.

101. <font color="red">**[FALTA]**</font> Diseñar un algoritmo para detección de bucles naturales usando back-edges y aplica a un CFG.

102. <font color="red">**[FALTA]**</font> Realizar optimización de propagación de constantes en un código intermedio dado y mostrar resultados.

103. <font color="red">**[FALTA]**</font> Detectar y eliminar common subexpression en un bloque de código intermedio con explicaciones.

104. <font color="red">**[FALTA]**</font> Diseñar análisis de aliasing simple y mostrar cómo afecta a optimizaciones de memoria.

105. <font color="red">**[FALTA]**</font> Implementar análisis de puntos de escape de variables para decidir si se pueden colocar en stack.

106. <font color="red">**[FALTA]**</font> Construir SSA para un fragmento de código y explicar cómo facilita ciertas optimizaciones.

107. <font color="red">**[FALTA]**</font> Diseñar un pass para hoisting de invariantes de bucle y demostrar en un ejemplo con nested loops.

108. <font color="red">**[FALTA]**</font> Aplicar strength reduction a una operación de multiplicación por constante en un bucle y mostrar código resultante.

109. <font color="red">**[FALTA]**</font> Establecer un conjunto de transformaciones seguras para interprocedural constant propagation.

110. <font color="red">**[FALTA]**</font> Diseñar un análisis de alias interprocedural para punteros simples y discutir escalabilidad.

111. <font color="red">**[FALTA]**</font> Implementar un algoritmo para detection of unreachable code y removerlo conservativamente.

112. <font color="red">**[FALTA]**</font> Diseñar tests para verificar correctitud de un pass de optimización que reordena instrucciones.

113. <font color="red">**[FALTA]**</font> Analizar cómo la ordenación de instrucciones por dependencias afecta la latencia y rendimiento.

114. <font color="red">**[FALTA]**</font> Proponer métricas para evaluar la calidad de un optimizador (code size, runtime, compile time).

115. <font color="red">**[FALTA]**</font> Comparar efectos de optimizaciones locales vs globales en un ejemplo de función con múltiples bloques.

116. <font color="red">**[FALTA]**</font> Diseñar un análisis para detectar sincronización innecesaria en código concurrente y sugerir optimizaciones.

117. <font color="red">**[FALTA]**</font> Construir el grafo de flujo de control (CFG) para una función que contiene if/else y while.

118. <font color="red">**[FALTA]**</font> Calcular reaching definitions para cada bloque básico en un ejemplo dado y mostrar cómo se usan.

119. <font color="red">**[FALTA]**</font> Aplicar análisis de live variables y proponer eliminaciones de código muerto en un fragmento.

120. <font color="red">**[FALTA]**</font> Implementar en papel el algoritmo de dominadores para un CFG y determinar el dominador inmediato.

## Sección 6: Asignación de registros y manejo automático de memoria (GC, stack, spills)

121. <font color="red">**[FALTA]**</font> Dado un fragmento de código con variables temporales, construir el grafo de interferencia y colorearlo con 3 registros disponibles.

122. <font color="red">**[FALTA]**</font> Explicar y demostrar el proceso de spill y reload cuando no hay suficientes registros; generar código resultante.

123. <font color="red">**[FALTA]**</font> Diseñar el layout de stack frame para una función con parámetros, variables locales y espacio para temporales.

124. <font color="red">**[FALTA]**</font> Comparar asignación de registros por grafo coloring vs heurística linear scan en términos de complejidad y calidad.

125. <font color="red">**[FALTA]**</font> Diseñar un algoritmo para decidir qué variables deben ir al heap vs stack basándose en escape analysis.

126. <font color="red">**[FALTA]**</font> Implementar conteo de referencias y mostrar un ejemplo donde falla por ciclos; proponer solución.

127. <font color="red">**[FALTA]**</font> Diseñar un garbage collector simple (mark-sweep) y trazar su ejecución en un heap pequeño.

128. <font color="red">**[FALTA]**</font> Desarrollar una política de spilling basada en costo/beneficio y aplicar a un bloque ejemplo.

129. <font color="red">**[FALTA]**</font> Diseñar un esquema para generación automática de código de prolog/epilog de funciones para convención de llamadas.

130. <font color="red">**[FALTA]**</font> Analizar trade-offs entre asignación de registros en tiempo de compilación y en tiempo de ejecución (JIT).

131. <font color="red">**[FALTA]**</font> Diseñar un sistema de arenas/regiones para manejo eficiente de memoria temporal y comparar con GC.

132. <font color="red">**[FALTA]**</font> Construir un ejemplo donde escape analysis permite evitar allocations y mostrar el código resultante.

133. <font color="red">**[FALTA]**</font> Diseñar y justificar una estrategia de spill-filling para minimizar movimientos de memoria.

134. <font color="red">**[FALTA]**</font> Analizar cómo el orden de evaluación y side-effects afectan la colocación de variables en registros.

135. <font color="red">**[FALTA]**</font> Diseñar un esquema para manejo automático de memoria en un intérprete embebido con constraints de tiempo real.

136. <font color="red">**[FALTA]**</font> Implementar en pseudocódigo una función que realice stack allocation para closures si no escapan.

137. <font color="red">**[FALTA]**</font> Diseñar un GC incremental para reducir latencia y aplicar traza de ejecución en un ejemplo.

138. <font color="red">**[FALTA]**</font> Proponer cómo integrar escape analysis con un optimizador para mejorar asignación de registros.

139. <font color="red">**[FALTA]**</font> Diseñar pruebas que muestren pérdidas de rendimiento por spilling excesivo y cómo mitigarlas.

140. <font color="red">**[FALTA]**</font> Crear un ejemplo donde reuse de registros entre bloques reduce dramáticamente el número de spills.
