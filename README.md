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

Se deben clasificar los procesos en función de su impacto en el negocio. Los procesos productivos deben tener la máxima prioridad, mientras que los análisis exploratorios pueden ser considerados secundarios. Esto se puede llevar a cabo con el uso de colas en Hadoop con el uso de YARN donde los trabajos productivos tengan su propia cola con recursos asignados y los trabajos exploratorios se envíen a una cola de menor prioridad.


### Limitación de Recursos
- Configura límites de recursos (CPU, memoria) para los trabajos de análisis exploratorios, asegurando que no interrumpan los procesos productivos. 
- Esto puede hacerse a través de configuraciones en YARN.

## Estrategias de Ejecución

### Horarios de Ejecución
- Programa los procesos exploratorios durante horarios de baja carga, como la noche o fines de semana, cuando la demanda de recursos es menor.

### Batch Processing
- Agrupa procesos exploratorios en lotes para ejecutarlos en intervalos programados, liberando así recursos durante las horas pico.

### Scaling Vertical y Horizontal
- Considera la posibilidad de escalar tu clúster si es viable, añadiendo más nodos o recursos para manejar mejor la carga de trabajo.

## Herramientas de Scheduling

### Apache Oozie
- Un sistema de coordinación de trabajos para Hadoop que permite programar flujos de trabajo, ideal para ejecutar procesos en función de sus prioridades y dependencias.

### Apache Airflow
- Herramienta de orquestación que permite programar y monitorear flujos de trabajo de manera más visual, facilitando la gestión de procesos exploratorios.

### YARN Capacity Scheduler
- Permite configurar y gestionar la asignación de recursos en el clúster, optimizando el uso de CPU y memoria según las prioridades definidas.

### Chronos o Quartz
- Para programar tareas de forma más flexible y sencilla, estas herramientas pueden ser útiles para gestionar procesos exploratorios en horarios específicos.

## Conclusión
La clave es establecer un balance entre la eficiencia de los procesos productivos y la necesidad de análisis exploratorios. Al implementar una combinación de estrategias de priorización, ejecución y herramientas de scheduling, puedes optimizar el rendimiento de tu clúster de Hadoop.


