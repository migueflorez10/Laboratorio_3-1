### Info de la Materia: Topicos Especiales en Telematica-st0263

### Estudiante:
- Miguel Angel Martinez Florez, mamartinef@eafit.edu.co

### Profesor:  Edwin Nelson Montoya Munera, emontoya@eafit.edu.co  

# Laboratorio 3-1: GESTIÓN DE ARCHIVOS EN HDFS Y S3 PARA BIG DATA

##  Objetivo

## Descripción de la Actividad 

## Guia paso a paso 
- **LAB 3-0: Crear un Cluster AWS EMR en Amazon para trabajar todos los laboratorios.**
- NOTA: Esta guía describe los pasos necesarios para instalar y configurar un clúster EMR (Elastic MapReduce) en AWS (Amazon Web Services). El objetivo es usar herramientas de big data como Hadoop y Spark para análisis de datos.
- Prerrequisitos
  - Antes de iniciar, asegúrate de tener lo siguiente:
    - Una cuenta de AWS.
    - Claves SSH para acceder al clúster.
- Pasos para Crear un Clúster EMR
  - Accede a EC2: Ve al servicio EC2 en la consola de AWS.
  - Generar Claves SSH: Crea un nuevo par de claves SSH (si no tienes uno). Guarda la clave privada en tu máquina local para acceder al máster del clúster.
- Iniciar la Creación del Clúster EMR
  - Acceder a EMR: Desde la consola de AWS, navega a EMR.
  - Crear Clúster: Haz clic en "Create cluster".
  - Opciones Avanzadas: Selecciona "Go to advanced options".
- Configurar el Clúster
  - Versión de EMR: Selecciona la versión 6.3.1.
  - Componentes del Clúster:
    - Hadoop: Framework para el procesamiento distribuido de grandes conjuntos de datos.
    - Hive: Data warehouse que facilita consultas SQL-like sobre grandes conjuntos de datos.
    - Hue: Interfaz de usuario web para gestionar Hadoop.
    - Spark: Framework de procesamiento de datos en tiempo real.
    - Livy: Servicio REST para la interacción con Spark (opcional, no se selecciona en este caso).
    - HBase: Base de datos NoSQL distribuida.
    - JupyterHub: Entorno de notebooks para data science y análisis.
- Configurar Persistencia de Notebooks en S3
  - Configurar S3: Para persistir los notebooks creados en JupyterHub, configura un bucket S3.
    - Crear Bucket: Ve a S3 y crea un nuevo bucket. El nombre debe ser único a nivel global (por ejemplo, notebooks-montoya).
- Configuración de Hardware
  - Tipo de Instancia: Cambia las instancias por m4.xlarge (recomendado para cuentas de AWS Educate).
  - Uso de Instancias Spot: Selecciona instancias Spot para reducir costos.
  - Almacenamiento: Configura 20 GB de almacenamiento para los nodos.
- Configurar Auto Terminación
  - Auto Terminación: Habilita la auto terminación para que el clúster se destruya después de 1 hora de inactividad, ahorrando costos.
- Finalizar Configuración
  - Nombre del Clúster: Asigna un nombre descriptivo, por ejemplo, mi-cluster-montoya-631.
  - Clave SSH: Selecciona la clave SSH creada previamente.
  - Crear Clúster: Haz clic en "Create cluster".
-  Esperar la Creación del Clúster
  - La creación del clúster tomará aproximadamente 20-25 minutos. Una vez que todos los nodos estén en estado "Running" y todo esté en verde, el clúster estará listo para usarse.
- Pasos Posteriores
  - En una segunda parte del proceso, se detallará cómo usar el clúster creado para ejecutar trabajos y análisis con EMR.
- Consideraciones Adicionales
  - Puertos: Asegúrate de abrir los puertos necesarios para acceder a las interfaces de administración del clúster.
  - Persistencia en S3: Configura correctamente el bucket S3 para que los datos de los notebooks sean persistentes.

## Resultados Esperados

## Descripción del Ambiente de Desarrollo y Técnico
