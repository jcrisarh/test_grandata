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
  
  
  




## Resultados Obtenidos

### Monto Total por Envío de SMS

El monto total que facturará el proveedor por envíos de SMS es: **$[TOTAL_SMS_COST]**.

### Dataset de Usuarios con Mayor Facturación

El dataset de usuarios con mayor facturación se encuentra en: `results/top_users.parquet`.

### Histograma de Llamadas

El histograma de llamadas generado se encuentra en: `results/calls_histogram.png`.

## Conclusiones

Este ejercicio proporciona una visión general sobre cómo manejar datos en un entorno de procesamiento distribuido como Spark y la importancia de optimizar recursos en un clúster Hadoop.
