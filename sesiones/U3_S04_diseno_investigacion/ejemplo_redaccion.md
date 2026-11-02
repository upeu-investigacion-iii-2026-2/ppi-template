# Ejemplo de redacción — U3 Sesión 4: Diseño de la investigación

> **Aviso.** Este ejemplo es un modelo de **redacción y estructura**. El tema,
> las cifras, las herramientas y las decisiones son **ficticios** y no deben
> copiarse. Cada equipo debe redactar su propio diseño a partir de su problema,
> sus objetivos y su hipótesis. Base conceptual:
> `recursos/Guia_teorica_diseno_investigacion_y_recoleccion_datos.md`.

**Tema del ejemplo:** efecto de una estrategia de caché en la latencia y en la
corrección de las respuestas de un servicio web.

**Pregunta:** ¿cómo cambian la latencia y la proporción de respuestas
incorrectas al activar la estrategia de caché, bajo cargas definidas?

**Hipótesis (H1):** bajo las cargas evaluadas, la estrategia reduce la latencia
mediana respecto de la configuración de referencia sin aumentar la proporción
de respuestas incorrectas.

---

## 3. Procedimiento metodológico (ejemplo de redacción)

### 3.1. Enfoque, alcance y tipo de investigación

La investigación adopta un enfoque cuantitativo, pues responde a la pregunta
mediante mediciones de latencia y de corrección de respuestas. Su alcance es
explicativo-comparativo: se busca estimar la diferencia entre dos
configuraciones y no solo describir el comportamiento del servicio. Es una
investigación aplicada, de fuente primaria, con intervención planificada:
la estrategia de caché es el factor que el investigador activa o desactiva de
forma deliberada.

### 3.2. Diseño de la investigación

Se empleará un diseño experimental con comparación controlada por bloques. Cada
bloque corresponde a un nivel de carga (baja, media y alta) y dentro de cada
uno se ejecutan ambas condiciones: configuración de referencia (`baseline`) y
configuración con la estrategia (`proposal`). El orden de las condiciones se
asignará aleatoriamente dentro de cada bloque para reducir sesgos debidos a
efectos de calentamiento o a variaciones del entorno. Este diseño permite
atribuir las diferencias observadas a la estrategia, y no a otros factores,
porque el hardware, la versión del software y los datos permanecen constantes.

La Tabla 1 muestra la correspondencia entre los objetivos específicos y el
diseño.

**Tabla 1.** Coherencia entre objetivos y diseño

| Objetivo específico | Actividad que lo responde | Resultado esperado |
|---|---|---|
| OE1. Estimar el efecto de la estrategia sobre la latencia | Ejecución de ambos tratamientos en tres bloques de carga | Diferencia de latencia mediana por carga |
| OE2. Determinar su efecto sobre la corrección de las respuestas | Verificación de cada respuesta contra un resultado de referencia | Diferencia en proporción de respuestas incorrectas |
| OE3. Identificar bajo qué cargas el efecto es relevante | Comparación entre bloques | Condiciones donde la mejora es práctica |

### 3.3. Unidades de análisis, población y muestra

La unidad experimental es la **ejecución**: una corrida completa de una
condición, iniciada desde un estado controlado (caché vacía y datos
restaurados). Las solicitudes son observaciones dentro de cada ejecución y no
se tratarán como independientes. La población de interés son los servicios web
de lectura intensiva con perfil de uso similar al evaluado; la población
accesible es el servicio de prueba desplegado en el laboratorio. Por tanto, las
conclusiones se limitan a ese contexto.

Se realizarán 30 ejecuciones por condición y bloque, número determinado por
la variabilidad observada en el piloto y por los recursos disponibles. Las
operaciones se seleccionaron de manera deliberada a partir del uso previsto:
80 % de lecturas y 20 % de escrituras.

### 3.4. Variables y operacionalización

**Tabla 2.** Operacionalización de variables

| Variable | Tipo | Definición operacional | Escala o unidad | Instrumento |
|---|---|---|---|---|
| Estrategia de caché | Independiente | Presencia (`proposal`) o ausencia (`baseline`) de la estrategia | Categórica | Ficha de ejecución |
| Nivel de carga | Independiente (bloque) | Solicitudes por segundo generadas: 50, 200 y 500 | Solicitudes/s | Script de carga |
| Latencia | Dependiente | Tiempo entre el envío de la solicitud y la recepción completa de la respuesta, medido en el cliente | ms | Registro por solicitud |
| Respuestas incorrectas | Dependiente | Proporción de respuestas que difieren del resultado de referencia, incluidas las obsoletas | % | Registro por solicitud |
| Hardware, versión y datos | Control | Se mantienen constantes en todas las ejecuciones | — | Ficha de entorno |

### 3.5. Procedimiento

1. Preparar una copia controlada de los datos y fijar la configuración del
   entorno.
2. Comprobar el instrumento de medición con un piloto de 5 ejecuciones.
3. Para cada bloque de carga, definir de forma aleatoria el orden de las
   condiciones.
4. Restaurar el estado inicial, ejecutar la condición y registrar cada
   solicitud.
5. Verificar la integridad de los registros y anotar las incidencias.
6. Conservar los datos originales sin modificar y generar los datos derivados
   mediante scripts versionados.

### 3.6. Plan de análisis y contraste de hipótesis

Se formulan H0: la mediana de latencia con la estrategia es igual o mayor que
la de referencia, y H1: es menor. Para cada bloque se compararán las medianas
de las ejecuciones mediante una prueba no paramétrica para muestras
pareadas, con nivel de significancia de 0,05 y verificación previa de la
distribución. Se informarán el tamaño del efecto y el intervalo de confianza, y
no solo el valor p. La proporción de respuestas incorrectas se analizará con
una prueba de diferencia de proporciones. Las latencias extremas no se
eliminarán salvo que se demuestre un error de captura.

### 3.7. Amenazas a la validez y límites

- **Interna:** variaciones del entorno entre ejecuciones; se controlan con
  restauración del estado y orden aleatorio.
- **De constructo:** la latencia medida en el cliente incluye la red; se
  reporta como latencia percibida y no como tiempo interno del servidor.
- **Externa:** los resultados se obtienen en un entorno de laboratorio y con
  tres niveles de carga, por lo que no se generalizan a producción.
- **De conclusión:** las solicitudes de una misma ejecución están agrupadas;
  el análisis se realiza a nivel de ejecución.

### 3.8. Consideraciones éticas y riesgos

El estudio no involucra personas ni datos personales: se utilizan datos
sintéticos. Se declaran las versiones y licencias del software empleado. Como
riesgo principal se identifica la saturación del equipo de pruebas, que se
mitiga con un monitoreo de recursos y la repetición de las ejecuciones
afectadas.

### 3.9. Cronograma

| Actividad | S1 | S2 | S3 | S4 | S5 | S6 |
|---|---|---|---|---|---|---|
| Diseño e instrumentos | X | X | | | | |
| Piloto y ajustes | | X | | | | |
| Recolección definitiva | | | X | X | | |
| Análisis | | | | X | X | |
| Interpretación e informe | | | | | X | X |

---

## Errores frecuentes de redacción

| Redacción débil | Redacción mejorada |
|---|---|
| «Usaremos Python y Docker.» | «Se comparará la configuración de referencia y la propuesta sobre las mismas cargas, ejecutadas en contenedores con configuración fija.» |
| «Desarrollar y evaluar un prototipo.» | «Se evaluará el prototipo comparando su latencia con la configuración de referencia en tres niveles de carga.» |
| «Se tomarán 30 datos porque es lo habitual.» | «Se realizarán 30 ejecuciones por condición según la variabilidad del piloto y los recursos.» |
| «La mejora se debe a la estrategia.» | «En las condiciones evaluadas, la estrategia se asoció con una reducción de la latencia mediana.» |

## Lista de verificación del texto

- [ ] El diseño responde a cada objetivo específico.
- [ ] Se explica por qué el diseño permite contrastar la hipótesis.
- [ ] Cada variable tiene definición operacional, escala e instrumento.
- [ ] Se distingue la unidad experimental de las observaciones.
- [ ] El análisis indica pruebas, supuestos y criterio de decisión.
- [ ] Se declaran límites sin sobregeneralizar.
