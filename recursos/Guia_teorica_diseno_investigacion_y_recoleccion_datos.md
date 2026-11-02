# Guía teórica: diseños de investigación y recolección de datos en computación

**Organización:** dos unidades, correspondientes a los contenidos de diseño de investigación y de técnicas y herramientas de recolección de datos.  
**Referencia principal:** Raul Sidnei Wazlawick, *Metodologia de pesquisa para Ciência da Computação*, 3.ª edición, LTC, ejemplar con ficha de 3.ª reimpresión de 2026.

## Presentación

Investigar en computación exige decidir qué necesitamos conocer y cómo obtendremos evidencia para responderlo. Construir un sistema, entrenar una red neuronal o instalar una base de datos puede formar parte del trabajo, pero esas actividades no explican por sí mismas qué conocimiento se producirá.

Wazlawick distingue la aplicación práctica del conocimiento de la contribución científica y señala que los artefactos pueden incorporar ideas que deben estudiarse mediante evidencia. El interés investigativo se encuentra en lo que aprendemos sobre esas ideas, sus resultados y sus condiciones de funcionamiento (Wazlawick, 2026, sec. 4.4).

Esta guía utiliza esa orientación y las explicaciones del autor sobre procedimientos, objetivos, definiciones operacionales y variables. Los ejemplos, tablas, protocolos, métricas y actividades son elaboraciones didácticas complementarias: no deben atribuirse literalmente al libro. Las citas remiten a secciones porque se consultó la versión textual del ejemplar, sin paginación editorial verificable.

**Todos los datos numéricos de los ejemplos son ficticios.** Sirven para practicar decisiones y cálculos; no constituyen resultados de investigaciones realizadas ni tamaños de muestra recomendados.

## Resultados de aprendizaje

Al finalizar, podrás:

1. Diferenciar método, diseño, procedimiento, técnica, instrumento y herramienta.
2. Justificar un diseño en función de una pregunta de investigación.
3. Definir unidades de análisis, criterios de selección y estrategia muestral.
4. Operacionalizar variables o establecer categorías de análisis.
5. Diseñar la recolección y el análisis de datos procedentes de servidores, bases de datos, imágenes, voz y participantes.
6. Reconocer límites de la evidencia y planificar materiales, ética, cronograma y presupuesto.

# Unidad I. Diseños de investigación

## 1. ¿Qué es el diseño de investigación?

El **diseño de investigación** es el plan que establece cómo se obtendrá y analizará la evidencia necesaria para responder una pregunta. Relaciona el objetivo con las unidades que se estudiarán, las condiciones de observación o intervención, las mediciones, las comparaciones y el análisis.

Un diseño debe permitir comprender qué se hará y por qué ese procedimiento puede producir una respuesta defendible. Wazlawick explica que el procedimiento metodológico se define a partir del objetivo y debe precisar cómo se organizarán y compararán los datos. También advierte que expresiones como «desarrollar y evaluar un prototipo» requieren explicar en qué consistirá la evaluación (2026, sec. 6.2).

### 1.1. Conceptos relacionados

Para esta guía se adoptan las siguientes distinciones operativas. Los términos pueden tener usos diferentes en otras fuentes; en tu proyecto debes definirlos y emplearlos de manera consistente.

| Concepto | Significado | Ejemplo |
|---|---|---|
| Método o estrategia general | Forma organizada de abordar el problema y obtener evidencia. | Experimentación para comparar dos algoritmos. |
| Diseño | Configuración concreta del estudio: unidades, condiciones, comparaciones, selección y análisis. | Comparar ambos algoritmos sobre las mismas cargas, con orden aleatorio y repeticiones definidas. |
| Procedimiento | Secuencia detallada de acciones para ejecutar el diseño. | Preparar datos, configurar el entorno, ejecutar, registrar, verificar y analizar. |
| Técnica | Procedimiento específico para obtener o analizar datos. | Medición automatizada de tiempos. |
| Instrumento | Estructura o mecanismo que define y registra lo observado. | Ficha de ejecución y esquema de campos del registro. |
| Herramienta | Recurso que permite aplicar una técnica o implementar un instrumento. | Script de medición y analizador de registros. |

**Ejemplo:** «Usaremos Python» identifica una herramienta o entorno de implementación. No explica el diseño. «Compararemos dos métodos de detección sobre los mismos periodos de logs, manteniendo separado un periodo final de prueba» expresa decisiones de diseño.

### 1.2. La coherencia del diseño

La cadena fundamental es:

**Pregunta → objetivo → evidencia necesaria → diseño → recolección → análisis → respuesta y límites.**

Ejemplo: si deseas conocer la frecuencia de errores HTTP, necesitas registros y criterios de conteo. Si deseas saber por qué se producen, esos conteos pueden resultar insuficientes: necesitarás contexto, hipótesis o evidencia adicional. Si deseas atribuir una reducción de errores a una nueva configuración, tendrás que considerar comparaciones y explicaciones alternativas.

## 2. Método de investigación

El método indica el camino general que se seguirá para producir conocimiento. Debe elegirse por su correspondencia con la pregunta y los objetivos, y por la posibilidad real de obtener evidencia pertinente.

Wazlawick presenta procedimientos bibliográficos, documentales, experimentales, de levantamiento, investigación acción, etnografía y estudio de caso, entre otros. También contempla su combinación (2026, sec. 4.3). No existe obligación de que todo proyecto utilice encuestas o experimentos.

### 2.1. Investigación experimental

El investigador modifica deliberadamente uno o más factores y observa sus resultados bajo condiciones planificadas. La comparación busca distinguir el efecto de lo modificado de otras influencias.

**Ejemplo con bases de datos:** comparar una consulta con y sin un índice. La condición manipulada es la presencia del índice; el resultado medido es la duración de la consulta. Deben considerarse volumen de datos, selectividad, caché, concurrencia y configuración. Si se modifica al mismo tiempo el hardware, no será sencillo atribuir la diferencia al índice.

La asignación aleatoria de condiciones y el orden aleatorio de ejecución pueden ayudar a reducir ciertos sesgos, pero no reemplazan una justificación del entorno, las unidades y el análisis.

### 2.2. Investigación observacional y documental

Se examinan fenómenos o datos existentes sin asignar deliberadamente la exposición principal. En computación pueden analizarse logs históricos, repositorios, tablas, incidencias o reportes.

**Ejemplo con servidores:** analizar durante qué horarios se concentran los errores HTTP 500. El investigador no provoca fallos ni cambia el servidor: estudia los registros disponibles. Puede encontrar asociaciones temporales, pero no debe atribuir automáticamente los fallos a una causa específica.

El almacenamiento no define el método: una tabla de base de datos puede contener observaciones históricas o resultados de un experimento. Debe explicarse cómo se originaron los datos.

### 2.3. Estudio de caso

Examina un fenómeno de manera profunda dentro de un contexto delimitado. Puede integrar entrevistas, observación, documentos y mediciones.

**Ejemplo:** estudiar cómo una empresa diagnostica incidentes en un sistema distribuido. Los logs muestran eventos; las entrevistas ayudan a comprender decisiones; los reportes permiten reconstruir el proceso.

El caso se delimita por organización, servicio, equipo, periodo y problema. Un sistema probado una vez no se convierte automáticamente en un estudio de caso completo. Wazlawick advierte que un caso favorable no demuestra validez general (2026, sec. 4.3).

### 2.4. Levantamiento mediante encuesta

Recoge respuestas de una población definida para describir prácticas, experiencias o percepciones.

**Ejemplo:** conocer qué dificultades reportan administradores al interpretar alertas. Un cuestionario puede aportar información sobre experiencias, pero no demostrar directamente que una herramienta detecta más fallos. Para ello hacen falta mediciones de detección y una referencia adecuada.

La selección y la no respuesta pueden sesgar los resultados; Wazlawick discute estos problemas en las secciones 4.3 y 6.2.1.

### 2.5. Investigación acción

Combina participación, intervención y reflexión sobre un problema contextual. El investigador trabaja con los involucrados y documenta lo aprendido durante los ciclos de cambio.

**Ejemplo:** colaborar con un equipo de operaciones para mejorar la gestión de incidentes. Cada ciclo registra diagnóstico, cambio aplicado, evidencia y reflexión. La contribución exige analizar lo aprendido y las condiciones que explican los resultados; instalar un panel de monitoreo, por sí solo, no basta (Wazlawick, 2026, sec. 4.3).

### 2.6. Investigación bibliográfica y síntesis de evidencia

Utiliza estudios publicados para responder preguntas. La revisión sistemática y el mapeo requieren protocolos de búsqueda, selección, extracción y síntesis.

**Ejemplo:** revisar qué estrategias se utilizan para evaluar modelos de reconocimiento de voz en ambientes ruidosos. Aquí la fuente son estudios y sus resultados, no grabaciones recogidas directamente por el estudiante (Wazlawick, 2026, secs. 4.1 y 7.4).

### 2.7. Investigación orientada al diseño

Busca conocimiento sobre cómo podrían ser las soluciones. Puede desarrollar un artefacto e investigar sus principios, decisiones, resultados y limitaciones.

**Ejemplo:** proponer una estrategia de selección de imágenes para reducir anotación y evaluar en qué condiciones conserva el desempeño de clasificación. La contribución debe explicar algo sobre la estrategia; presentar la aplicación terminada no responde por sí solo a esa pregunta. Wazlawick reconoce la investigación de diseño entre los objetivos de investigación (2026, sec. 4.2).

Estas estrategias pueden combinarse. La clasificación anterior no constituye una lista de categorías mutuamente excluyentes.

## 3. Intervención tecnológica y proceso de desarrollo

Una **intervención tecnológica** introduce o modifica una tecnología, configuración, procedimiento o artefacto en un contexto. Puede constituir una parte del estudio.

Conviene distinguir:

- **Desarrollo:** construye o configura la solución.
- **Intervención:** introduce el cambio bajo condiciones definidas.
- **Evaluación investigativa:** recoge y analiza evidencia para responder una pregunta sobre el cambio.

**Ejemplo:** programar un detector de anomalías es una actividad de desarrollo. Integrarlo en un servicio es una intervención. Comparar su capacidad de detección y sus falsas alertas bajo un protocolo es una evaluación.

Scrum, un tablero de tareas o el ciclo de desarrollo ayudan a organizar el trabajo técnico. Su uso no especifica por sí mismo cómo se producirán las conclusiones científicas. Esta distinción permite abordar la intervención tecnológica prevista en el sílabo dentro del tema general «Método de investigación», sin tratarla como un método universal.

## 4. Determinación de etapas y actividades de ejecución

Una **etapa** agrupa actividades con un propósito común. Una **actividad** es una acción concreta que produce un resultado verificable. El **objetivo de investigación** expresa qué conocimiento se pretende obtener.

Wazlawick advierte que los objetivos específicos no deben confundirse con actividades como revisar literatura, desarrollar un prototipo o ejecutar un experimento (2026, sec. 6.1).

| Etapa | Actividades posibles | Producto verificable |
|---|---|---|
| Delimitación | Precisar problema, pregunta, alcance y antecedentes. | Pregunta y objetivo sustentados. |
| Diseño | Definir unidades, condiciones, selección, variables y análisis. | Protocolo del estudio. |
| Preparación | Gestionar acceso, preparar entorno y elaborar instrumentos. | Datos autorizados e instrumentos versionados. |
| Pilotaje | Probar extracción, medición, anotación o preguntas. | Registro de problemas y ajustes. |
| Ejecución | Aplicar el protocolo y registrar incidencias. | Datos originales y bitácora. |
| Procesamiento y análisis | Revisar calidad, transformar y analizar. | Datos derivados, resultados y scripts. |
| Interpretación y comunicación | Responder la pregunta, discutir límites y documentar. | Informe y materiales que puedan compartirse. |

**Ejemplo con voz:** antes de grabar todo el corpus, el pilotaje puede revelar saturación del micrófono o identificadores duplicados. Detectarlo después de la grabación completa puede volver inutilizable parte del material.

Las etapas pueden iterar, pero los cambios deben registrarse. Modificar una hipótesis después de observar resultados es distinto de haberla planteado antes; debe comunicarse con transparencia.

## 5. Tipo y diseño de investigación

### 5.1. Dimensiones de clasificación

El tipo caracteriza el estudio desde una dimensión; el diseño describe cómo se ejecutará. No conviene reunir todas las etiquetas en una sola clasificación.

| Dimensión | Posibilidades | Pregunta orientadora |
|---|---|---|
| Fuente de evidencia | Primaria, secundaria o terciaria. | ¿Producimos evidencia original, sintetizamos estudios o sintetizamos revisiones? |
| Objetivo | Exploratorio, descriptivo, explicativo o de diseño. | ¿Qué clase de conocimiento buscamos? |
| Enfoque de evidencia | Cuantitativo, cualitativo o mixto. | ¿Trabajamos con mediciones, significados o una integración de ambos? |
| Intervención | Observacional o con intervención planificada. | ¿Modificamos deliberadamente las condiciones? |
| Tiempo | Corte temporal definido o seguimiento longitudinal. | ¿Estudiamos un periodo puntual o cambios en el tiempo? |

Las dos primeras dimensiones corresponden a las secciones 4.1 y 4.2 de Wazlawick. Las demás se incluyen como organización didáctica complementaria. Un estudio no se vuelve mixto solo por presentar números y comentarios: debe integrar ambos tipos de evidencia para responder la pregunta.

### 5.2. Diseños y decisiones concretas

**Experimento con comparación controlada.** Se planifican condiciones, asignación, mediciones y análisis para comparar alternativas. Ejemplo: ejecutar los algoritmos A y B sobre las mismas cargas, alternando aleatoriamente su orden dentro de bloques definidos por carga. Debe distinguirse variación entre cargas de variación entre repeticiones.

**Cuasiexperimento.** Evalúa una intervención con limitaciones relevantes para asignar condiciones de manera aleatoria o establecer comparabilidad. Ejemplo: comparar la evolución de un servicio intervenido con otro servicio semejante durante periodos comunes. La elección del diseño debe explicarse, no deducirse únicamente del nombre de la muestra.

**Antes–después de un único grupo.** Registra una situación previa y otra posterior en el mismo contexto. Por sí solo ofrece capacidad limitada para atribuir causalidad: pueden influir cambios de carga, aprendizaje, estacionalidad o actualizaciones. No debe presentarse como experimento controlado solo porque contiene dos mediciones.

**Observacional longitudinal.** Sigue un fenómeno en el tiempo sin asignar la intervención. Ejemplo: estudiar la relación entre despliegues y errores durante varios meses. La coincidencia temporal requiere examinar explicaciones alternativas.

**Estudio de caso único o múltiple.** Delimita uno o varios contextos y establece un protocolo común de evidencia. La selección de casos debe tener una razón analítica; aumentar casos no garantiza representatividad estadística.

### 5.3. Variables y definiciones operacionales

Una variable representa una propiedad que puede tomar distintos valores. En un experimento, una variable manipulada corresponde a un factor que el investigador cambia; una variable medida corresponde a un resultado observado. Wazlawick desarrolla esta distinción en la sección 6.2.3.

Una **definición conceptual** explica el significado de una propiedad. Una **definición operacional** precisa cómo se observará o medirá en el estudio (Wazlawick, 2026, sec. 6.2.2).

| Propiedad | Definición operacional para un estudio concreto | Límite |
|---|---|---|
| Rapidez | Tiempo entre envío y recepción completa de una solicitud desde un cliente de prueba. | Incluye componentes distintos del tiempo interno del servidor. |
| Capacidad de detección | Proporción de incidentes de referencia identificados según una ventana y regla de coincidencia definidas. | Depende de la calidad de la referencia. |
| Calidad de clasificación | Precision y recall por clase sobre un conjunto de prueba separado. | No describe automáticamente desempeño en otros dominios. |
| Calidad de transcripción | Tasa de error de palabras tras una normalización documentada. | No representa por sí sola utilidad o comprensión. |

No existe una única operacionalización válida para todo estudio. Debe justificarse por qué la medida representa la propiedad relevante. Un tiempo menor no significa mejor solución si se incrementan errores o se produce un resultado incorrecto.

## 6. Diseño muestral

El **diseño muestral** establece qué unidades se seleccionarán, de dónde procederán, cómo se elegirán y qué alcance tendrán las conclusiones.

### 6.1. Conceptos básicos

- **Población de interés:** conjunto al que se desea referir las conclusiones.
- **Población accesible:** parte a la que realmente se puede acceder.
- **Marco muestral:** listado o mecanismo que identifica las unidades seleccionables.
- **Muestra:** subconjunto que se estudiará.
- **Unidad de análisis:** entidad sobre la que se formularán conclusiones.
- **Unidad de observación:** entidad o evento del que se obtiene un registro.
- **Unidad experimental:** entidad a la que se asigna una condición experimental.

Estas unidades pueden coincidir o ser diferentes. Si se estudian políticas aplicadas por servidor y cada servidor genera miles de solicitudes, las solicitudes son observaciones anidadas; no equivalen a miles de servidores independientes.

### 6.2. Selección de unidades

En una selección **probabilística**, las unidades tienen probabilidades de inclusión conocidas. Puede utilizarse selección aleatoria simple, estratificación o conglomerados, según el marco y la pregunta.

En una selección **no probabilística**, se eligen unidades por acceso, criterios deliberados o necesidades analíticas. Puede ser apropiada, pero no autoriza estimaciones representativas de toda una población sin argumentos adicionales.

**Ejemplos:**

- Logs: seleccionar periodos de baja, media y alta carga para cubrir condiciones previstas. Si se sobremuestrean errores, la proporción observada no estima directamente su frecuencia real sin ajustar el diseño.
- Bases de datos: seleccionar consultas de lectura, escritura y agregación; cada categoría responde a comportamientos distintos.
- Imágenes: seleccionar sujetos u objetos antes de distribuir imágenes relacionadas entre conjuntos.
- Voz: seleccionar hablantes, sesiones y condiciones acústicas. Tener muchos fragmentos de pocas personas no garantiza diversidad de hablantes.

### 6.3. Cantidad de datos y dependencia

No existe un tamaño universal como «30 muestras» o «el 10 %». La justificación considera precisión requerida, variabilidad, estructura de dependencia, efecto relevante, recursos y alcance. En estudios cualitativos se considera profundidad, diversidad y suficiencia de la información, explicando el criterio utilizado.

**Ejemplo:** 10 hablantes producen 100 grabaciones cada uno. Existen 1000 audios y 10 hablantes. Para una afirmación sobre desempeño en hablantes nuevos, el número y diversidad de hablantes son fundamentales; los 1000 audios no son 1000 personas independientes.

### 6.4. Muestra y particiones de aprendizaje automático

Seleccionar datos y dividirlos son decisiones distintas:

- **Entrenamiento:** ajustar parámetros del modelo.
- **Validación:** elegir configuraciones, umbrales o variantes.
- **Prueba:** estimar desempeño final con datos que no guiaron esas decisiones.

Las proporciones se justifican según el problema; no constituyen reglas universales. Debe evitarse la **filtración de información**, que ocurre cuando información reservada para la evaluación participa en el aprendizaje o selección.

| Datos | Riesgo | Decisión preventiva |
|---|---|---|
| Logs | Registros del futuro influyen en decisiones para predecir el pasado. | Separación temporal acorde con el uso previsto. |
| Imágenes | Fotografías casi idénticas del mismo objeto aparecen en entrenamiento y prueba. | Separar por objeto, sujeto, sesión o fuente pertinente. |
| Voz | Fragmentos del mismo hablante aparecen en ambos conjuntos aunque se quiere evaluar hablantes nuevos. | Separación por hablante. |
| Datos tabulares | La misma persona aparece en filas de distintos conjuntos. | Separación por entidad cuando corresponda. |

El aumento artificial de imágenes o audio debe aplicarse después de la separación y según el propósito de cada conjunto. Las transformaciones aprendidas de los datos se ajustan utilizando únicamente la información permitida por el protocolo.

# Unidad II. Técnicas y herramientas de recolección de datos

## 7. ¿Qué significa recolectar datos?

Recolectar datos es obtener y registrar evidencia de manera planificada. Incluye definir su origen, formato, identificación, calidad, contexto y condiciones de acceso.

Descargar un dataset o exportar un log es solo una parte. Debe conocerse cómo se produjeron los datos, qué representan, qué falta y qué sesgos pueden contener. Wazlawick enfatiza que recoger datos no sustituye su interpretación ni la producción de conocimiento (2026, sec. 6.2.1).

### 7.1. Técnica, instrumento y herramienta

| Técnica | Instrumento | Herramienta posible | Resultado |
|---|---|---|---|
| Extracción de logs | Esquema de campos y reglas de selección. | Script de lectura y exportación. | Tabla de eventos. |
| Medición de rendimiento | Protocolo y ficha de ejecución. | Generador de carga y temporizador. | Mediciones por ejecución. |
| Extracción de base de datos | Consulta documentada y diccionario de datos. | Cliente SQL. | Tabla de registros seleccionados. |
| Anotación de imágenes | Manual de etiquetas y formato de anotación. | Aplicación de etiquetado. | Imágenes con referencia anotada. |
| Registro de voz | Protocolo de grabación y ficha de sesión. | Micrófono y grabadora. | Audios y metadatos. |
| Entrevista | Guía semiestructurada. | Grabadora o formulario de notas. | Audio, transcripción y notas. |
| Observación | Ficha de tareas y eventos. | Registro de pantalla autorizado. | Conductas, tiempos e incidencias. |

Un cuestionario no es obligatorio en un estudio de rendimiento. Un script puede implementar un instrumento, pero debe documentar sus reglas y comprobar que registra lo previsto.

## 8. Construcción de instrumentos

Un instrumento debe permitir entender qué se registra y cómo se interpreta.

### 8.1. Pasos de elaboración

1. Identificar la pregunta u objetivo al que aportará evidencia.
2. Definir variables, indicadores o categorías.
3. Especificar campos, unidades, valores permitidos y reglas.
4. Asignar identificadores que permitan vincular registros sin exponer datos innecesarios.
5. Establecer instrucciones de aplicación y tratamiento de incidencias.
6. Pilotear con un subconjunto y comprobar la correspondencia con la fuente.
7. Corregir, versionar y conservar el historial de cambios.

### 8.2. Diccionario de datos de ejemplo

| Campo | Tipo y unidad | Regla | Precaución |
|---|---|---|---|
| `run_id` | Texto | Identifica una ejecución. | No confundir con una solicitud. |
| `timestamp` | Fecha y hora con zona definida | Formato uniforme. | Registrar sincronización y desfases. |
| `condition` | Categoría | `baseline` o `proposal`. | No inferirla de nombres ambiguos. |
| `latency_ms` | Numérico, milisegundos | Definir inicio y fin. | No confundir segundos con milisegundos. |
| `status_code` | Entero | Código registrado en la fuente. | Diferenciar error del servicio y fallo de medición. |
| `session_id` | Texto | Vincula datos de una sesión. | Permite reconocer agrupamiento. |
| `quality_flag` | Categoría | Válido, incompleto o error de captura. | Conservar motivo y registro original. |

## 9. Calidad de los datos y de los instrumentos

La **validez de la medición** se refiere al sustento para interpretar los datos como evidencia de la propiedad de interés. La **confiabilidad** se relaciona con la consistencia de la medición en condiciones pertinentes. Una medición consistentemente equivocada puede ser confiable y carecer de validez para el uso previsto.

**Ejemplo:** medir solo el tiempo interno de la base de datos no equivale a medir el tiempo total percibido por el usuario. Ambos pueden ser útiles, pero responden a propiedades distintas.

Las comprobaciones dependen del instrumento:

- Scripts: contrastar una extracción pequeña con la fuente y comprobar unidades, duplicados, pérdidas y errores.
- Cuestionarios: revisar pertinencia y comprensión; examinar propiedades de las escalas cuando corresponda.
- Entrevistas: pilotear formulación, secuencia y preguntas de seguimiento.
- Anotaciones: capacitar, anotar una parte en común, medir acuerdo con un criterio adecuado y resolver discrepancias.
- Grabaciones: revisar saturación, silencios, frecuencia de muestreo, canales y metadatos.

No debe aplicarse automáticamente alfa de Cronbach a cualquier instrumento. Su pertinencia depende del modelo de medición y del uso de una escala; no valida genéricamente logs, scripts, entrevistas o fichas de tiempos.

La ausencia de errores de captura tampoco garantiza un buen diseño: datos correctos pueden proceder de una selección sesgada.

## 10. Caso didáctico A: logs de servidores

### 10.1. Pregunta y diseño

**Pregunta:** ¿cómo varía la frecuencia de errores HTTP 500 entre franjas de carga durante el periodo observado?

**Diseño:** observacional longitudinal de un servicio delimitado. La carga debe operacionalizarse; por ejemplo, solicitudes por minuto. Los límites de cada franja deben justificarse antes del análisis principal.

**Fuente:** logs de acceso y, si corresponde, registros internos vinculados por identificadores. El periodo debe cubrir las condiciones que se desea estudiar.

### 10.2. Datos de ejemplo

| Franja | Total de solicitudes | Respuestas HTTP 500 | Porcentaje |
|---|---:|---:|---:|
| Baja carga | 1000 | 5 | 0,5 % |
| Alta carga | 1000 | 40 | 4,0 % |

**Cálculo:** porcentaje = respuestas HTTP 500 / total de solicitudes × 100.

La diferencia es de **3,5 puntos porcentuales**. En estos datos, la proporción de alta carga es ocho veces la de baja carga. No equivale a una diferencia de 3,5 % ni demuestra que la carga sea la causa de los errores.

### 10.3. Recolección y análisis

Registrar periodo, servidor, ruta normalizada, código, duración si existe y definición de carga. Documentar si los reintentos cuentan como nuevas solicitudes y si los fallos sin respuesta aparecen en otra fuente.

Procesar sin eliminar errores por resultar incómodos. Revisar continuidad temporal, rotación de logs y registros duplicados. Analizar por tiempo, ruta y servidor cuando la pregunta lo requiera. Las solicitudes cercanas pueden estar relacionadas por un mismo incidente.

**Conclusión permitida:** en el servicio y periodo analizados se observó mayor proporción de HTTP 500 en la franja de alta carga.

**Conclusión no sustentada:** la alta carga causó los errores en todos los servidores.

**Pregunta para el estudiante:** ¿cambiaría tu interpretación si todos los errores de alta carga ocurrieran durante un único despliegue?

## 11. Caso didáctico B: consultas a una base de datos

### 11.1. Pregunta y diseño

**Pregunta:** ¿cómo cambia el tiempo de una familia de consultas al incorporar un índice, bajo volúmenes y cargas definidos?

**Diseño:** comparación experimental por bloques. Cada bloque puede corresponder a una combinación de volumen y carga. Se planifica el orden de condiciones y se mantiene una copia controlada de los datos.

**Factor:** índice presente o ausente.  
**Resultados:** tiempo, corrección del resultado y, si resulta pertinente, costo de escritura o almacenamiento.  
**Condiciones registradas:** motor, versión, configuración, datos, consultas, hardware y estado de caché.

### 11.2. Mediciones de ejemplo

| Repetición ilustrativa | Sin índice, ms | Con índice, ms |
|---|---:|---:|
| 1 | 120 | 45 |
| 2 | 118 | 47 |
| 3 | 125 | 44 |
| 4 | 117 | 46 |
| 5 | 120 | 48 |
| Media | 120 | 46 |

Reducción relativa respecto de la condición sin índice: **(120 − 46) / 120 × 100 = 61,7 %**, aproximadamente.

Este cálculo resume cinco mediciones ficticias. No demuestra significación estadística ni determina un tamaño de muestra suficiente.

### 11.3. Instrumento y procedimiento

La ficha registra `run_id`, consulta, condición, bloque, orden, duración, resultado y anomalías. Antes de medir, se define si interesa el comportamiento con caché fría, caliente o ambos. Se verifica que las consultas producen resultados equivalentes.

No se descartan automáticamente las primeras ejecuciones: si se establece calentamiento, debe justificarse y aplicarse de forma consistente. Tampoco deben tratarse todas las repeticiones sobre la misma consulta como consultas independientes.

**Conclusión limitada:** el índice redujo el tiempo de las consultas evaluadas bajo estas condiciones; debe estudiarse su efecto en otros volúmenes y en operaciones de escritura.

**Pregunta para el estudiante:** ¿qué pasaría si la condición sin índice se midiera con carga alta y la condición con índice durante un periodo sin usuarios?

## 12. Caso didáctico C: conjunto de imágenes

### 12.1. Pregunta y diseño

**Pregunta:** ¿cómo cambia la detección de defectos con el método propuesto frente a una referencia, en imágenes de objetos no vistos durante el entrenamiento?

**Diseño:** evaluación comparativa sobre un conjunto de prueba separado por objeto físico. Se especifican origen, captura, etiquetas y criterios de inclusión.

Supongamos 100 objetos fotografiados seis veces: existen 600 imágenes, pero 100 objetos. Si fotografías casi idénticas del mismo objeto aparecen en entrenamiento y prueba, el resultado puede reflejar reconocimiento de ese objeto y no generalización a objetos nuevos.

### 12.2. Referencia y anotación

El manual de anotación define qué cuenta como defecto, clases, regiones y tratamiento de casos dudosos. Se conserva el identificador del objeto y de la sesión. La referencia debe provenir de un procedimiento independiente del modelo evaluado; sus errores también deben considerarse.

### 12.3. Matriz de resultados ficticia

Se considera «defecto» como clase positiva.

| Referencia | Predice defecto | Predice sin defecto |
|---|---:|---:|
| Defecto | 18 | 2 |
| Sin defecto | 8 | 72 |

- Exactitud global: (18 + 72) / 100 = **90 %**.
- Precision de la clase defecto: 18 / (18 + 8) = **69,2 %**.
- Recall o sensibilidad: 18 / (18 + 2) = **90 %**.

Los indicadores responden a preguntas diferentes. Una exactitud global de 90 % no informa por sí sola cuántas alertas son incorrectas. Debe considerarse el costo de omitir defectos y el de generar falsas alertas.

### 12.4. Recolección y evaluación

Conservar imágenes originales, etiquetas, procedencia, permisos y reglas de transformación. Comparar los métodos sobre las mismas unidades de prueba cuando corresponda. Si se ajusta el umbral tras mirar la prueba, esta deja de ser una evaluación final independiente de esa decisión.

**Pregunta para el estudiante:** si todas las imágenes de prueba se capturaron con iluminación uniforme, ¿puedes concluir que el método funciona igual con iluminación variable?

## 13. Caso didáctico D: grabaciones de voz

### 13.1. Pregunta y diseño

**Pregunta:** ¿cómo cambia el error de transcripción de dos modelos al procesar voz con diferentes condiciones de ruido, en hablantes no vistos?

**Diseño:** comparación sobre audios de los mismos hablantes de prueba, separados de entrenamiento y validación. Si se añade ruido artificialmente, deben documentarse el procedimiento y los niveles; ello no representa automáticamente todo ambiente real.

### 13.2. Instrumentos y metadatos

El protocolo define consignas, micrófono, distancia, entorno, formato y procedimiento de transcripción de referencia. La ficha incluye hablante seudonimizado, sesión, frase, condición, duración y calidad.

La transcripción de referencia requiere revisión. Su normalización —mayúsculas, signos, números, abreviaturas— se establece antes de calcular la métrica.

### 13.3. Ejemplo de tasa de error de palabras

La tasa de error de palabras, **WER**, se calcula como:

**WER = (sustituciones + eliminaciones + inserciones) / palabras de referencia.**

Para una referencia de 20 palabras, con 2 sustituciones, 1 eliminación y 1 inserción:

**WER = (2 + 1 + 1) / 20 = 0,20 = 20 %.**

WER no es una medida directa de comprensión y puede superar 100 % cuando hay muchas inserciones. El protocolo debe especificar si se suman errores sobre todo el corpus o se promedian tasas por audio o hablante; esas agregaciones no son equivalentes.

### 13.4. Interpretación

Comparar condiciones con información sobre distribución entre hablantes y sesiones. Si pocos hablantes producen muchos audios, debe reconocerse ese agrupamiento. Las conclusiones sobre acentos o ambientes no evaluados requieren evidencia adicional.

**Pregunta para el estudiante:** ¿sería válido afirmar desempeño para hablantes nuevos si la prueba contiene fragmentos distintos de los mismos hablantes usados para entrenar?

## 14. Técnicas para el procesamiento y análisis de la información

El **procesamiento** prepara y organiza los datos; el **análisis** los utiliza para responder la pregunta. El plan de análisis debe orientar la recolección desde el inicio.

### 14.1. Flujo de procesamiento

1. Conservar una copia original protegida contra modificaciones accidentales.
2. Comprobar integridad, formatos y correspondencia con la fuente.
3. Documentar faltantes, duplicados, exclusiones y transformaciones.
4. Generar datos derivados mediante procedimientos reproducibles.
5. Vincular cada resultado con la versión de datos, instrumento y código utilizados.

Los datos atípicos no se eliminan solo por ser extremos: pueden representar fallos reales o condiciones relevantes. Debe distinguirse un error de captura de un comportamiento raro pero válido.

### 14.2. Análisis cuantitativo

Utiliza resúmenes y comparaciones apropiados: frecuencias, proporciones, distribuciones, medianas, percentiles, diferencias e incertidumbre. La media puede ocultar colas largas en tiempos de respuesta.

Las pruebas estadísticas se eligen según la pregunta, escala, dependencia y supuestos. No se selecciona una prueba únicamente porque el tamaño sea mayor o menor que 30. Un valor p no mide la magnitud ni la importancia práctica del efecto. La ausencia de significación tampoco demuestra equivalencia.

Para un percentil debe indicarse la población de mediciones y el procedimiento usado. El percentil 95 de latencia describe un punto de la distribución: aproximadamente 95 % de las observaciones quedan en él o por debajo, según la convención de cálculo. No es un intervalo de confianza del 95 %.

### 14.3. Análisis cualitativo

Organiza e interpreta significados y experiencias mediante un procedimiento explícito. Puede incluir lectura, codificación, construcción de categorías, contraste de casos y revisión de interpretaciones.

**Ejemplo:** ante comentarios como «las alertas llegan duplicadas» y «dejamos de revisarlas por exceso de ruido», se pueden construir categorías sobre redundancia y fatiga de alertas. Deben conservarse los fragmentos y el contexto que sustentan la interpretación. Contar palabras no sustituye este análisis.

### 14.4. Integración de fuentes

Combinar logs, entrevistas y documentos puede ayudar a contrastar explicaciones. Si el equipo afirma que los incidentes se resuelven rápido pero los registros muestran cierres administrativos tardíos, corresponde examinar qué significa «resolver» en cada fuente. La discrepancia aporta información; no debe ocultarse.

## 15. Amenazas a la validez y límites

Las siguientes categorías son una organización didáctica complementaria para revisar el estudio:

| Dimensión | Pregunta | Ejemplo | Acción posible |
|---|---|---|---|
| Medición o constructo | ¿El indicador representa lo que afirmo estudiar? | Usar exactitud global para una clase rara. | Añadir métricas pertinentes y revisar la referencia. |
| Interna | ¿Existen explicaciones alternativas del cambio? | Cambiar índice y hardware simultáneamente. | Separar factores o limitar la interpretación. |
| Externa | ¿A qué contextos se aplica la evidencia? | Voz grabada solo en silencio. | Delimitar alcance y evaluar otros ambientes si el objetivo lo requiere. |
| Conclusión | ¿El análisis respeta la estructura y variabilidad? | Contar fotogramas de un objeto como objetos independientes. | Reconocer grupos y seleccionar un análisis compatible. |

Un piloto comprueba factibilidad y problemas del procedimiento; no reemplaza toda la evaluación. Una demostración funcional tampoco prueba superioridad frente a alternativas.

## 16. Materiales y aspectos éticos

### 16.1. Materiales y recursos

Especifica función, cantidad y disponibilidad: servidores, almacenamiento, motor de base de datos, cámaras, micrófonos, capacidad de cómputo, instrumentos y software con sus versiones. Explica cómo la configuración afecta las mediciones.

### 16.2. Tratamiento responsable de los datos

Planifica medidas acordes con el contenido y los requisitos institucionales aplicables:

- Logs: revisar credenciales, tokens, direcciones, rutas y cuerpos de solicitud antes de compartir.
- Bases de datos: utilizar datos autorizados y extraer solo campos necesarios.
- Imágenes: considerar identificabilidad, derechos de uso y exposición de personas.
- Voz: considerar que el audio puede identificar al hablante y revelar información personal.
- Participantes: explicar propósito, uso de datos y condiciones de participación cuando corresponda.

La seudonimización sustituye identificadores y mantiene una posible vinculación; no garantiza anonimato. Separar acceso para investigación y permiso para publicar: disponer de datos no implica autorización para difundirlos.

Documenta almacenamiento, acceso, conservación y eliminación. No declares una aprobación ética o cumplimiento institucional que no hayas obtenido o verificado. Estas orientaciones son prácticas generales y no reproducen legislación del libro.

## 17. Cronograma de actividades

El cronograma ubica actividades en el tiempo y señala dependencias. No reemplaza el diseño.

| Actividad ilustrativa | Semana 1 | Semana 2 | Semana 3 | Semana 4 | Semana 5 | Semana 6 |
|---|---|---|---|---|---|---|
| Pregunta, antecedentes y diseño | X | X | | | | |
| Acceso a datos e instrumentos | X | X | | | | |
| Pilotaje y ajustes | | X | | | | |
| Recolección definitiva | | | X | X | | |
| Procesamiento y análisis | | | | X | X | |
| Interpretación e informe | | | | | X | X |

Es un ejemplo, no una duración prescrita. La recolección definitiva depende de contar con acceso y de resolver los problemas detectados en el piloto. Si hay aprendizaje automático, deben presupuestarse también preparación, entrenamiento y evaluación.

## 18. Presupuesto

El presupuesto relaciona recursos con actividades. Debe mostrar cantidad, unidad, precio y justificación, diferenciando recursos disponibles y desembolsos previstos.

| Recurso ficticio | Cantidad | Costo unitario, S/ | Subtotal, S/ | Uso |
|---|---:|---:|---:|---|
| Cómputo | 20 horas | 3 | 60 | Ejecuciones de evaluación. |
| Almacenamiento | 2 meses | 15 | 30 | Conservación y respaldo. |
| Material de grabación | 1 unidad | 40 | 40 | Preparación de sesiones. |
| Total | | | 130 | |

Los precios son ficticios. Un equipo disponible puede no requerir compra, pero debe declararse como recurso utilizado. El presupuesto debe considerar licencias, anotación y acceso a datos si efectivamente se requieren.

# Aplicación y autoevaluación

## 19. Ejemplo de integración metodológica

**Tema:** evaluación de una estrategia de caché en un servicio web.

**Pregunta:** ¿cómo cambia la latencia y la proporción de respuestas incorrectas al activar la estrategia, bajo cargas definidas?

**Objetivo:** estimar las diferencias entre la estrategia y la configuración de referencia en las condiciones evaluadas.

**Diseño:** experimento con comparación por bloques de carga; asignación planificada de condiciones y orden aleatorio dentro de bloques.

**Unidades:** ejecuciones independientes definidas por el protocolo; las solicitudes son mediciones dentro de cada ejecución. La independencia debe justificarse mediante preparación y control del estado.

**Variables:** estrategia, carga, latencia y corrección de respuesta. Registrar fallos y respuestas obsoletas; no analizar únicamente las solicitudes exitosas sin explicarlo.

**Instrumentos:** protocolo, script de carga, registro por solicitud y ficha por ejecución.

**Selección:** cargas y operaciones justificadas por el uso de interés. Las repeticiones se determinan mediante variabilidad y precisión requerida, dentro de recursos disponibles.

**Procedimiento:** preparar copia de datos, comprobar instrumento, pilotear, fijar configuración, ejecutar bloques, conservar logs y analizar diferencias e incertidumbre.

**Límites:** un entorno de laboratorio y cargas seleccionadas no representan automáticamente toda condición productiva.

Este esquema concreta la recomendación de Wazlawick de conectar objetivo, procedimiento, comparación y evaluación de resultados (2026, sec. 6.2).

## 20. Actividades para estudiantes

### Actividad 1. Convertir una actividad técnica en una propuesta de investigación

Elige uno de estos enunciados: «crear un panel de logs», «implementar un índice», «entrenar un clasificador de imágenes» o «construir un transcriptor de voz».

Plantea una pregunta que requiera evidencia, define el conocimiento buscado y explica qué parte corresponde al desarrollo. Evita declarar novedad o superioridad sin revisar antecedentes.

### Actividad 2. Justificar el diseño

Completa la matriz y comprueba que ningún objetivo quede sin evidencia:

| Pregunta | Objetivo | Diseño y razón | Unidades y selección | Datos requeridos | Análisis | Límites |
|---|---|---|---|---|---|---|
| Completar | Completar | Completar | Completar | Completar | Completar | Completar |

### Actividad 3. Elaborar y pilotear un instrumento

Construye una ficha o esquema de extracción con al menos identificador, procedencia, variable o categoría, unidad, regla de registro y calidad. Aplícalo a un pequeño conjunto de prueba y registra qué problemas encontraste. El número usado en el piloto no determina automáticamente el tamaño de la muestra final.

### Actividad 4. Detectar errores de interpretación

Explica el problema y propone una corrección:

1. «Tenemos un millón de líneas de un servidor; por tanto, representamos todos los servidores de la institución».
2. «El modelo alcanzó 95 % de exactitud; por tanto, funciona bien para cualquier clase».
3. «El sistema mejoró después de instalar la herramienta; la herramienta causó toda la mejora».
4. «Dividimos aleatoriamente fragmentos de los mismos hablantes y evaluamos hablantes nuevos».
5. «La encuesta fue validada porque calculamos un coeficiente, sin revisar qué medían los ítems».
6. «El método será revisar, programar y evaluar; no hace falta explicar la evaluación».

## 21. Producto final y criterios de revisión

Entrega un protocolo que incluya:

1. Problema, pregunta, objetivo y alcance.
2. Método y diseño justificados.
3. Etapas y actividades con productos verificables.
4. Unidades, población accesible, selección y justificación de cantidad.
5. Variables y definiciones operacionales o categorías.
6. Técnicas, instrumentos, herramientas y diccionario de datos.
7. Pilotaje y comprobaciones de calidad.
8. Procedimiento de recolección, procesamiento y análisis.
9. Amenazas a la validez y límites.
10. Materiales, tratamiento de datos, cronograma y presupuesto.

Antes de entregar, pregúntate: ¿otra persona podría comprender y ejecutar el procedimiento?, ¿cada conclusión prevista tendrá evidencia?, ¿estoy confundiendo observaciones con unidades independientes?, ¿el análisis responde a la pregunta?, ¿he definido qué haré si la propuesta no supera a la referencia?

# Referencia y orientación de lectura

Wazlawick, R. S. (2026). *Metodologia de pesquisa para Ciência da Computação* (3.ª ed., 3.ª reimp.). LTC.

Se utiliza el año de la ficha del ejemplar consultado, que identifica la reimpresión de 2026; no se presenta como una edición metodológica nueva de ese año. El archivo indica cierre editorial en 2020 y copyright de la edición en 2021.

| Contenido de la guía | Lectura del libro |
|---|---|
| Fuentes y objetivos de investigación | Secciones 4.1 y 4.2. |
| Procedimientos de investigación | Sección 4.3. |
| Ciencia, tecnología y contribución | Sección 4.4. |
| Objetivos frente a actividades | Sección 6.1. |
| Coherencia y detalle del procedimiento | Sección 6.2. |
| Datos e interpretación | Sección 6.2.1. |
| Definiciones operacionales | Sección 6.2.2. |
| Variables medidas y manipuladas | Sección 6.2.3. |
| Revisiones y mapeos | Sección 7.4. |
| Formulación de preguntas | Capítulo 8. |

**Alcance de atribución:** Wazlawick fundamenta la lógica de investigación empleada. La organización en unidades, las distinciones terminológicas operativas, los protocolos específicos, el desarrollo del muestreo, las particiones de aprendizaje automático, las métricas, las tablas, los ejercicios y las recomendaciones de reproducibilidad son complementos didácticos de esta guía. No se presentan como transcripciones o desarrollos exhaustivos del autor. Esta guía no sustituye una referencia especializada en estadística, muestreo o validación de instrumentos cuando el estudio requiera esos desarrollos.
