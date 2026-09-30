# Proyecto de Ciencia de Datos

## Dataset elegido

Trabajaremos con el dataset **Reporte de Hurto por Modalidades de la Policía Nacional**

`Reporte_Hurto_por_Modalidades_Policía_Nacional_20260916.csv`

## Pregunta de negocio inicial

¿Es posible predecir la cantidad de hurtos de motocicletas que se presentarán en un municipio durante el siguiente mes, utilizando el comportamiento histórico de los hurtos y las variables disponibles en el dataset?

## Exploración inicial (Clase 1)

La primera lectura del archivo se encuentra en [exploracion_inicial.ipynb](exploracion_inicial.ipynb) (o en [entrega/exploracion_inicial.ipynb](entrega/exploracion_inicial.ipynb)). El dataset contiene 656.635 registros y 9 variables.

## Fase A: Diseño Dimensional (Clase 2)

El diseño del modelo dimensional en estrella y su justificación se encuentran documentados en [fase_a_diseño_borrador.pdf](fase_a_diseño_borrador.pdf) (o en [entrega/fase_a_diseño_borrador.pdf](entrega/fase_a_diseño_borrador.pdf)).
- **Tabla de hechos:** `FACT_HURTOS` (granularidad: reporte individual de hurto de vehículo).
- **Dimensiones:** `DIM_FECHA`, `DIM_MUNICIPIO`, `DIM_TIPO_HURTO`, `DIM_ARMA_MEDIO`, `DIM_VICTIMA`.

## Fase B: Pipeline ETL y Carga a Data Warehouse (Clase 3)

La implementación completa del ETL, validaciones de integridad y persistencia en SQLite se encuentra en [fase_b_etl.ipynb](fase_b_etl.ipynb) (o en [entrega/fase_b_etl.ipynb](entrega/fase_b_etl.ipynb)):
- **Extracción:** Carga de los 656.635 registros del CSV original.
- **Transformación:** Parseo de fechas, estandarización de texto, imputación de nulos categóricos a `'NO REPORTADO'`.
- **Surrogate Keys:** Generación de claves subrogadas para las 5 dimensiones.
- **Construcción de Hechos:** Asignación de FKs hacia las dimensiones y surrogate key `hurto_id`.
- **Validación:** Se verifica estrictamente `len(hecho) == len(fuente)` (656.635 filas, 0 nulos en FKs).
- **Carga:** Exportación del modelo a base de datos SQLite relacional (`hurto_dw.db`) con índices analíticos.
- **Reflexión:** Documentación detallada de estrategia de carga incremental (CDC, marcas de agua, SCD, tablas staging e idempotencia).


**Integrantes**
BOLAÑOS ISIQUITA DIEGO ANDRES - 202379918 
GOMEZ PUENTES DIEGO ALEJANDRO - 202411026  
MUJANAJINSOY JAJOY DAVID STIVEN - 202376834  

