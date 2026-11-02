# Ejemplo de redacción — U3 Sesión 5: Recolección de datos

> **Aviso.** Este ejemplo es un modelo de **redacción y estructura**. El tema,
> las cifras, los campos y las decisiones son **ficticios** y no deben
> copiarse. Cada equipo debe adaptarlo a su diseño y a sus variables. Base
> conceptual: `recursos/Guia_teorica_diseno_investigacion_y_recoleccion_datos.md`.

**Tema del ejemplo:** efecto de una estrategia de caché en la latencia y en la
corrección de las respuestas de un servicio web (continuación del ejemplo de la
Sesión 4).

---

## 4. Técnicas e instrumentos de recolección de datos (ejemplo de redacción)

### 4.1. Fuentes y técnicas

Los datos son de fuente primaria y se obtienen durante los experimentos. La
técnica principal es la **medición automatizada de latencia** mediante un
generador de carga que registra cada solicitud. La corrección de las respuestas
se obtiene por **verificación automática** contra un resultado de referencia
calculado a partir de la copia controlada de los datos. Complementariamente, se
registran las condiciones del entorno mediante una ficha de ejecución.

**Tabla 1.** Matriz indicador–técnica–instrumento–herramienta

| Variable | Indicador | Técnica | Instrumento | Herramienta | Resultado |
|---|---|---|---|---|---|
| Latencia | Tiempo de respuesta (ms) | Medición automatizada | Esquema de registro por solicitud | Script generador de carga | Tabla de solicitudes |
| Respuestas incorrectas | Proporción que difiere de la referencia | Verificación automática | Reglas de comparación documentadas | Script validador | Indicador por solicitud |
| Condiciones del entorno | Versiones, configuración, estado | Registro estructurado | Ficha de ejecución | Plantilla en YAML | Ficha por ejecución |

### 4.2. Instrumentos

El **registro por solicitud** almacena un evento por cada petición con los
campos descritos en el diccionario de datos. La **ficha de ejecución** describe
cada corrida: condición, bloque, orden, estado inicial, versión del software y
anomalías. Los instrumentos se encuentran en `instrumentos/` y se versionan
mediante Git; todo cambio posterior al piloto se documenta con un commit
descriptivo.

### 4.3. Diccionario de datos

**Tabla 2.** Diccionario de datos del registro por solicitud

| Campo | Tipo y unidad | Regla de registro | Precaución |
|---|---|---|---|
| `run_id` | Texto | Identifica una ejecución | No confundir con la solicitud |
| `request_id` | Texto | Identifica la solicitud dentro de la ejecución | Único por ejecución |
| `timestamp` | Fecha y hora UTC | Formato ISO 8601 | Reloj sincronizado |
| `condition` | Categoría | `baseline` o `proposal` | No inferir desde nombres de archivo |
| `block` | Categoría | `50`, `200` o `500` solicitudes/s | Corresponde a la carga objetivo |
| `latency_ms` | Numérico, ms | Desde el envío hasta la recepción completa | No confundir con segundos |
| `status_code` | Entero | Código HTTP recibido | Diferenciar error del servicio de fallo de medición |
| `is_correct` | Booleano | Compara con la referencia | Una respuesta obsoleta se marca `false` |
| `quality_flag` | Categoría | `valid`, `incomplete` o `capture_error` | Conservar el motivo |

### 4.4. Validación y prueba piloto

La validez de la medición se comprobó contrastando una muestra de 100
solicitudes con los tiempos que registra un analizador de paquetes
independiente; las diferencias se encontraron dentro de ±2 ms y se documentó que
el indicador mide latencia percibida por el cliente. Dado que el instrumento es
un script y no una escala, no se aplicó alfa de Cronbach; en su lugar se
verificaron unidades, duplicados, pérdidas de registros y correspondencia con
la fuente.

El piloto consistió en 5 ejecuciones por condición con el bloque de menor
carga. Se detectó que la primera ejecución se veía afectada por el calentamiento
del entorno y que el campo `latency_ms` mezclaba unidades. Como resultado, se
incorporó una fase de calentamiento definida y aplicada de manera uniforme y se
corrigió el esquema. Las cifras del piloto no determinan el tamaño de la
muestra final.

### 4.5. Protocolo de recolección

1. Restaurar la copia controlada de los datos y vaciar la caché.
2. Registrar la ficha de ejecución con el orden asignado aleatoriamente.
3. Ejecutar la fase de calentamiento y luego la fase de medición.
4. Guardar los registros originales en modo solo lectura.
5. Verificar integridad (conteo de solicitudes, duplicados, formato).
6. Anotar incidencias y repetir las ejecuciones afectadas por fallos de captura.

La recolección definitiva se realizará en las semanas 3 y 4 del cronograma.

### 4.6. Almacenamiento, limpieza y control de calidad

Los datos originales se guardan en `experimentos/datos_originales/` en formato
CSV, sin modificaciones. Los datos derivados se generan con scripts versionados
que registran las transformaciones. Los registros incompletos se marcan con
`quality_flag` y se conservan; únicamente se excluyen del análisis cuando se
demuestra un error de captura, indicando el motivo. Los valores extremos no se
eliminan por su magnitud, pues pueden representar comportamiento real.

### 4.7. Aspectos éticos, privacidad y licencias

El estudio emplea datos sintéticos generados por el equipo; no contiene
información personal ni credenciales. Se registran las versiones y licencias de
las herramientas utilizadas y se revisaron los archivos antes de subirlos al
repositorio para evitar claves o rutas sensibles.

---

## Variante para estudios con personas (fragmento)

> La recolección se realizó mediante un cuestionario de 12 ítems en escala
> Likert, aplicado a 40 estudiantes seleccionados por conveniencia. Antes de su
> aplicación, tres expertos evaluaron la pertinencia y claridad de los ítems y
> se realizó un piloto con 8 estudiantes ajenos a la muestra, a partir del cual
> se reformularon dos ítems ambiguos. Los participantes dieron su consentimiento
> informado y las respuestas se almacenaron con un código en lugar del nombre.
> En el repositorio solo se conserva la versión anonimizada de los datos.

## Errores frecuentes de redacción

| Redacción débil | Redacción mejorada |
|---|---|
| «Se recolectarán los datos con un script.» | «La latencia se medirá con un script que registra, por solicitud, el tiempo entre el envío y la recepción completa.» |
| «El instrumento fue validado.» | «Se contrastaron 100 solicitudes con una herramienta independiente y se verificaron unidades y duplicados.» |
| «Se eliminaron los datos extraños.» | «Se excluyeron únicamente los registros marcados como error de captura, indicando el motivo.» |
| «Los datos están en el repositorio.» | «Los datos originales están en `experimentos/datos_originales/` en CSV, descritos por el diccionario de datos.» |

## Lista de verificación del texto

- [ ] Cada indicador tiene técnica, instrumento y herramienta.
- [ ] Se describe cómo se validó el instrumento y qué cambió tras el piloto.
- [ ] El protocolo permite que otra persona repita la recolección.
- [ ] El diccionario define tipo, unidad y regla de cada campo.
- [ ] Se explican limpieza y exclusiones.
- [ ] No hay datos personales en el repositorio.
