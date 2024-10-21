## Descripción del Proyecto

Este proyecto tiene como objetivo analizar el costo de envíos de SMS y proporcionar insights sobre la facturación de los usuarios. Se utiliza un entorno de procesamiento con Docker y Jupyter Notebook para facilitar el análisis de datos.

## Instrucciones de Ejecución

Asegúrate de tener Docker y Docker Compose instalados en tu máquina. Puedes verificar la instalación ejecutando:

```bash
docker --version
docker-compose --version
```

Para ejecutar el proyecto, sigue estos pasos:

1. Clona este repositorio:
```bash
git clone https://github.com/jcrisarh/test_grandata.git
```
2. Navega al directorio del proyecto:
```bash
cd test_grandata
```
3. Levanta los contenedores utilizando Docker Compose:
```bash
docker-compose up
```
  
## EJERCICIO 1: Resultados Obtenidos

### Monto Total por Envío de SMS

El monto total que facturará el proveedor por envíos de SMS es: **$ 1696022.5**.

### Dataset de Usuarios con Mayor Facturación

El dataset de usuarios con mayor facturación se encuentra en: `results/top_users.parquet`.

### Histograma de Llamadas

El histograma de llamadas generado se encuentra en: `results/calls_histogram.png`.

## EJERCICIO 2: Preguntas generales

## PREGUNTA 1

1. La empresa cuenta con un cluster on premise de Hadoop en el cual se ejecuta, tanto el
data pipeline principal de los datos, como los análisis exploratorios de los equipos de
Data Science y Data Engineering. Teniendo en cuenta que cada proceso compite por un
número específico de recursos del cluster:
- ¿Cómo priorizaría los procesos productivos sobre los procesos de análisis
exploratorios?
- Debido a que los procesos productivos del pipeline poseen un uso intensivo
tanto de CPU como de memoria, ¿qué estrategia utilizaría para administrar su
ejecución durante el día? ¿qué herramientas de scheduling conoce para tal fin?

## Priorización de Procesos

Se deben clasificar los procesos en función de su impacto en el negocio. Los procesos productivos deben tener la máxima prioridad, mientras que los análisis exploratorios pueden ser considerados secundarios. Esto se puede llevar a cabo con el uso de colas en Hadoop con el uso del capacity scheduler en el archivo de configuración YARN donde los trabajos productivos tengan su propia cola con recursos asignados y los trabajos exploratorios se envíen a una cola de menor prioridad. Los recursos se pueden limitar por queue.

La memoria de los contenedores yarn se pueden limitar en el archivo de configuración yarn-site.

## Estrategias de Ejecución

Los procesos exploratorios deben ser ejecutados durante los horarios de baja carga, con esto se asegura que los procesos productivos tengan prioridad en la asignación de recursos.

## Herramientas de Scheduling

Apache Oozie, Apache Airflow, YARN Capacity Scheduler

## PREGUNTA 2

2. Existe una tabla del Data Lake con alta transaccionalidad, que es actualizada
diariamente con un gran volumen de datos. Consultas que cruzan información con esta
tabla ven afectada su performance en tiempos de respuesta.
Según su criterio, ¿cuáles serían las posibles causas de este problema? Dada la
respuesta anterior, qué sugeriría para solucionarlo.

## Posibles Causas

Las posibles causas pueden ser:
- Una alta concurrencia de lecturas y/o escrituras, es decir, muchas transacciones realizadas sobre la misma tabla simultáneamente.
- Falta de indexación o indexación inadecuada para los datos utilizados en la consulta.
- Falta de particionamiento de la la tabla.
- Falta de recursos.

## Sugerencias para solucionarlo

- **Implementar particionamiento**: Dividir la tabla en particiones para mejorar el rendimiento.
- **Optimizar índices**: Crear índices adecuados en columnas de consulta.
- **Uso de materialized views**: Crear materialized views para consultas frecuentes, almacenando resultados precomputados.
- **Ajuste de recursos**: Asegurar que la infraestructura de hardware (CPU, RAM, disco) sea suficiente para la carga de trabajo.
- **Monitoreo y tuning**: Implementar herramientas de monitoreo para identificar cuellos de botella y ajustar la configuración según sea necesario.

