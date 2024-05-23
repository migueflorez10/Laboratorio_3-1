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
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/7e002b7c-a2f9-473f-8e1a-f7fdab81360a)
  - Crear Clúster: Haz clic en "Create cluster".
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/baef0681-6fd2-454c-bfcb-fa5e2edf0188)
  - Opciones Avanzadas: Selecciona "Go to advanced options".
- Configurar el Clúster
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/4c758e28-f865-41c0-afc6-70df2435c562)
  - Versión de EMR: Selecciona la versión 6.3.1.
  - Componentes del Clúster:
    - Hadoop: Framework para el procesamiento distribuido de grandes conjuntos de datos.
    - Hive: Data warehouse que facilita consultas SQL-like sobre grandes conjuntos de datos.
    - Hue: Interfaz de usuario web para gestionar Hadoop.
    - Spark: Framework de procesamiento de datos en tiempo real.
    - Livy: Servicio REST para la interacción con Spark (opcional, no se selecciona en este caso).
    - HBase: Base de datos NoSQL distribuida.
    - JupyterHub: Entorno de notebooks para data science y análisis.
- Configuración del Catálogo de datos de AWS Glue
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/0948597d-f9d1-4403-b171-8d662d2992b5)
- Configurar Persistencia de Notebooks en S3
  - Configurar S3: Para persistir los notebooks creados en JupyterHub, configura un bucket S3.
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/03c2b6aa-8ea9-494c-971f-47171381e6f6)
    ```
          [
            {
                "Classification": "jupyter-s3-conf",
                "Properties": {
                    "s3.persistence.enabled": "true",
                    "s3.persistence.bucket": "MyJupyterBackups"
                }
            }
        ]
    ```
    - Crear Bucket: Ve a S3 y crea un nuevo bucket. El nombre debe ser único a nivel global (por ejemplo, notebooks-miguel).
- Configuración de Hardware
  - Tipo de Instancia: Cambia las instancias por m4.xlarge (recomendado para cuentas de AWS Educate).
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/1e5cd945-ecb1-44ff-949d-92a22af9d989)
  - Uso de Instancias Spot: Selecciona instancias Spot para reducir costos.
  - Almacenamiento: Configura 20 GB de almacenamiento para los nodos.
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/cc75b0ff-f487-4a9f-b41a-cbbe24e3af23)
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/38727512-277c-4f0e-8e8a-661ea989d43a)
- Configurar Auto Terminación
  - Auto Terminación: Habilita la auto terminación para que el clúster se destruya después de 1 hora de inactividad, ahorrando costos.
- Finalizar Configuración
  - Nombre del Clúster: Asigna un nombre descriptivo, por ejemplo, mi-cluster.
  - Clave SSH: Selecciona la clave SSH creada previamente.
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/4b0bbe09-563f-4585-acab-b251ba60f2eb)
  - Rol de servicio de Amazon EMR
    - Escoger la opcion "ERM_DefaultRole"
  - Perfil de instancia de EC2 para Amazon EMR
    - Escoger la opcion "ERM_EC2_DefaultRole"
  - Rol de escalamiento automático personalizado - opcional
    - Escoger la opcion "ERM_AutoScaling_DefaultRole"
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/c204f52b-fb45-4e3d-8398-aada4a1834f2)
  - Crear Clúster: Haz clic en "Create cluster".
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/3d4654e1-f87d-412c-b12b-4c4379878c46)
-  Esperar la Creación del Clúster
  - La creación del clúster tomará aproximadamente 20-25 minutos. Una vez que todos los nodos estén en estado "Running" y todo esté en verde, el clúster estará listo para usarse.
- Consideraciones Adicionales
  - Puertos: Asegúrate de abrir los puertos necesarios para acceder a las interfaces de administración del clúster.
  - Persistencia en S3: Configura correctamente el bucket S3 para que los datos de los notebooks sean persistentes.

### Pasos posteriores despues de haber creado el cluster 
Esta guía detalla el proceso de configuración y uso de un clúster en Amazon EMR, incluyendo la creación de buckets en S3, conexión SSH al nodo master, apertura de puertos, y uso de aplicaciones como JupyterHub y Zeppelin. Se presentan los pasos necesarios y aspectos importantes a considerar para una correcta implementación y manejo de los recursos.

- Creación del Clúster
  - Verificación del Clúster
    - Después de aproximadamente 25 minutos, el clúster debería estar creado.
    - Un círculo en verde indica que el clúster está operativo.
  - Almacenamiento en S3
    - Los notebooks deben ser almacenados en S3.
    - Crear un bucket en S3 llamado notebooks.
  - Configuración del Bucket
    - Asegurarse de que el bucket está listo para almacenar los Jupyter Notebooks.
- Conexión al Clúster
  - Filtrar Clúster Activos
    - En la interfaz de administración, filtrar para mostrar solo los clústeres activos.
    - Conectar al nodo master vía SSH.
  - Instrucciones SSH
    - Seguir las instrucciones proporcionadas para conectarse al nodo master.
    - Descargar las claves necesarias y usar ssh para acceder al nodo master.
  - Uso de HDFS
    - Una vez conectado al nodo master, utilizar HDFS para manejar el sistema de archivos distribuido.
- Apertura de Puertos
  - Puertos Necesarios
    - Los puertos que deben estar abiertos son:
      - JupyterHub: 8888
      - Zeppelin: 8890
      - Otros: 9443
  - Configuración de Puertos en el Clúster
    - En la sección de Security Groups, editar las políticas para agregar los puertos necesarios.
    - Verificar que el puerto 22 para SSH esté abierto.
  - Verificación de Puertos
    - Asegurarse de que los puertos estén configurados correctamente tanto en el Security Group del nodo master como en la red WiFi.
- Uso de JupyterHub y Zeppelin
  - Acceso a JupyterHub
    - Conectar a JupyterHub usando la URL y el puerto configurado (9443).
    - Crear un usuario y contraseña la primera vez que se ingrese.
  - Creación y Almacenamiento de Notebooks
    - Crear notebooks en JupyterHub.
    - Asegurarse de que los notebooks se almacenan en S3 para evitar la pérdida de datos.
  - Configuración de Spark en JupyterHub
    - Verificar las variables spark y SparkContext para confirmar que Spark está configurado correctamente.
  - Uso de Zeppelin
    - Conectar a Zeppelin usando el puerto 8890.
    - Zeppelin soporta múltiples lenguajes, incluyendo Spark y SQL.
- Administración y Otros Servicios
  - Interfaz de Administración de EMR
    - Usar la interfaz de administración para manejar el clúster y sus servicios.
  - Manejo de Archivos en HDFS y S3
    - Almacenar datos importantes en S3 para asegurar su persistencia.
    - Utilizar HDFS para pruebas y manejo de datos temporales en el clúster.
- Consejos y Consideraciones
  - Seguridad
    - Asegurar la apertura correcta de puertos solo para conexiones necesarias.
    - Configurar usuarios y contraseñas adecuadas para acceso seguro a JupyterHub y Zeppelin.
  - Persistencia de Datos
    - Almacenar datos críticos en S3 para evitar pérdidas.
    - Utilizar HDFS para datos temporales y pruebas.




## Resultados Esperados

## Descripción del Ambiente de Desarrollo y Técnico
