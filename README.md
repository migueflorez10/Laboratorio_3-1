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
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/96fc047c-d94e-4615-986d-6d2f41cfb282)
  - Versión de EMR: Selecciona la versión 6.14.0
  - Componentes del Clúster:
    - Hadoop: Framework para el procesamiento distribuido de grandes conjuntos de datos.
    - Hive: Data warehouse que facilita consultas SQL-like sobre grandes conjuntos de datos.
    - Hue: Interfaz de usuario web para gestionar Hadoop.
    - Spark: Framework de procesamiento de datos en tiempo real.
    - Livy: Servicio REST para la interacción con Spark (opcional, no se selecciona en este caso).
    - HBase: Base de datos NoSQL distribuida.
    - JupyterHub: Entorno de notebooks para data science y análisis.
    - Entre otros.
- Configuración del Catálogo de datos de AWS Glue
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/0948597d-f9d1-4403-b171-8d662d2992b5)
- Configurar Persistencia de Notebooks en S3
  - Configurar S3: Para persistir los notebooks creados en JupyterHub, configura un bucket S3.
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/9947a521-13c3-4986-9ddd-32803c394535)
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
  - Tipo de Instancia: Cambia las instancias por m5.xlarge (recomendado para cuentas de AWS Educate).
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/88f5bb55-74d7-464a-afeb-bc0ff34ecce2)
  - Uso de Instancias Spot: Selecciona instancias Spot para reducir costos.
  - Almacenamiento: Configura 20 GB de almacenamiento para los nodos.
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/cc75b0ff-f487-4a9f-b41a-cbbe24e3af23)
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/1f2a24b0-71c5-4347-a8d1-6da7ff49f3a1)
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
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/2aa6e678-c434-4fd6-8765-e95c2ddd3bd3)
-  Esperar la Creación del Clúster
  - La creación del clúster tomará aproximadamente 20-25 minutos. Una vez que todos los nodos estén en estado "Running" y todo esté en verde, el clúster estará listo para usarse.
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/856b44fa-4fa1-45f1-aaea-3ea78066b59a)
- Consideraciones Adicionales
  - Puertos: Asegúrate de abrir los puertos necesarios para acceder a las interfaces de administración del clúster.
  - Persistencia en S3: Configura correctamente el bucket S3 para que los datos de los notebooks sean persistentes.

### Pasos posteriores despues de haber creado el cluster 
Esta guía detalla el proceso de configuración y uso de un clúster en Amazon EMR, incluyendo la creación de buckets en S3, conexión SSH al nodo master, apertura de puertos, y uso de aplicaciones como JupyterHub y Zeppelin. Se presentan los pasos necesarios y aspectos importantes a considerar para una correcta implementación y manejo de los recursos.

- Creación del Clúster
  - Verificación del Clúster
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/42867942-9c59-4f4b-9823-28d54a58ea2d)
    - Después de aproximadamente 25 minutos, el clúster debería estar creado.
    - Un círculo en verde indica que el clúster está operativo.
  - Almacenamiento en S3
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/2a426b6e-faec-4379-90ed-841fba09b94c)
    - Los notebooks deben ser almacenados en S3.
    - Crear un bucket en S3 llamado notebooks.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/66109d2e-4d0f-41dd-a439-87c0fff2e171)
    - Recuerda que el nombre del bucket debe tener el mismo nombre que escogimos al configurar la Persistencia de Notebooks en S3 del cluster
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/1ea196fa-e96e-42f7-8ba4-d8a09403dbb7)
    - Crear bucket
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/4794e263-ecc6-41ec-82a6-e90f01a46f81)
    - Confirmamos que el bucket se haya creado exitosamente.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/5b59db5a-032b-40ec-be98-2e5fc7d4bac6)
  - Configuración del Bucket
    - Asegurarse de que el bucket está listo para almacenar los Jupyter Notebooks.
- Conexión al Clúster
  - volvemos al servicio ERM a ver nuestro cluster
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/ad483a9b-6f49-4cbe-a044-309484643be6)
  - Filtrar Clúster Activos(opcional si tienes varios clusters)
    - En la interfaz de administración, filtrar para mostrar solo los clústeres activos.
    - Damos clic en el nombre de nuestro cluster para ingresar y ver las configuraciones
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/141808d9-d5c9-4059-9c1c-eb544b3cf6cb)
    - Conectar al nodo master vía SSH.
      - Damos clic en el siguiente link
      ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/30e3db54-d738-4e16-8563-60d7f9e8c0ab)
      - Al momento de dar clic nos aparecera lo siguiente:
      ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/4c5008a9-9b21-4214-8b01-6b43d4aa2304)
      - Copiamos la instruccion que nos proporciona, que en nuestro caso seria el siguiente:
      ```
      ssh -i ~/vockey.pem hadoop@ec2-44-210-115-214.compute-1.amazonaws.com
      ```
      - Abrimos una terminal(opcional):
        - Crea una consola que tenga previamente descargada las claves para conectarse al nodo master
        ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/ad20c1c4-e6eb-4c25-89e5-bf1529f8d94e)

  - Instrucciones SSH
    - Seguir las instrucciones proporcionadas para conectarse al nodo master.
    - Descargar las claves necesarias y usar ssh para acceder al nodo master.
  - Uso de HDFS
    - Una vez conectado al nodo master, utilizar HDFS para manejar el sistema de archivos distribuido.
- Apertura de Puertos
- En nuestro cluster, debemos dar clic en la opcion "aplicaciones"
![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/e39c35b7-c648-4f99-bade-02930a072f43)
- Al bajar un poco en la pagina, nos encontraremos las aplicaciones principlaes que vamos a emplear(IU de la aplicación en el nodo principal):
![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/f8a02ccf-606b-41fd-82aa-dc3f1bb129e6)
  - Puertos Necesarios
    - Los puertos que deben estar abiertos son:
      ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/e87b61c8-c3ed-44b2-a0f2-d04d330110e1)
      - JupyterHub: 9443
      - Zeppelin: 8890
      - Hue: 8888
  - Configuración de Puertos en el Clúster
  ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/c2b97ab5-9097-4cb9-9e66-d35139758942)
    - En la sección de Security Groups, editar las políticas para agregar los puertos necesarios.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/9bae5d62-cd28-45e6-9396-7b2cacadc657)
    - Verificar que el puerto 22 para SSH esté abierto.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/ca556866-0f07-40da-8f17-1d8bf3ed6d21)
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/17b1f3f2-6cda-4eba-960e-8c65572a1a2f)

  - Verificación de Puertos
    - Asegurarse de que los puertos estén configurados correctamente tanto en el Security Group del nodo master como en la red WiFi.
    - Nos iremos al servico "ec2".
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/d11a9e81-6fc0-4cb6-b943-2b1eb312cd9f)
    - A la opcion de Security Groups
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/3e83bd60-cee5-4dfc-9347-fc29f4592651)
    - Vamos a seleccionar el nodo master para editar las politicas de seguridad.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/9bce3426-f43e-4b0d-839d-c3d87e98c051)
    - Despues de dar clic e ingresar, nos vamos a las reglas de entrada y las editamos.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/46011522-7fe9-4754-a7c8-e288ef09d16f)
    - Verificamos que los puertos 22, 8888, 9443, 8890 esten habilitados, si no lo estan, debes crearlos.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/7b05ba66-09b8-4c19-8d4b-41b5cfee1b64)
    - Regresamos a nustro cluster
    - Volvemos al apartado de aplicaciones y copiamos el link de la interfaz de `HUE`.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/7976468d-0ad1-4c85-97b0-dba917da091f)
    - Lo pegamos en el navegador, nos conectamos y podremos visualizar la siguiente interfaz:
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/c3c6eb37-675d-4363-b0da-6f6a6e835d52)
    - Creamos una cuenta
      - Creamos un `username`
      - Creamos un `password`
      ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/8f6311ca-b9ab-4bff-b20b-d297d15b9907)
    - Al momento de crear la cuenta, visualizaremos lo siguiente:
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/3250c5ff-9713-4a3e-b01d-447599c40991)
    - Lo que observamos es la interfaz de administracion de todos los servicios de `HUE`y `Spark`
    - En esta seccion podemos observar todos los servicios
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/05fe95b2-3a21-4ab6-adef-53dcf5af3875)
    - Entre estos servicios, vamos a entrar al servicio `Hive` (opcional)
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/e10d0271-3f88-4a47-ae4c-1b6bd4f40d48)
    - En la interfaz SQL vamos a ingresar el siguiente comando (opcional):
    ```
    show databases
    ```
    - Corremos el comando (opcional):
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/c11fd390-d9df-461d-848f-bed70d49e236)
    - Observamos que por el momento solo tenemos una base de datos llamada `Default`.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/14f33756-47de-4485-87be-775f3c34245e)
    - Ahora, debemos ir a la seccion "files"
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/ec177434-110b-4247-b0f9-8b1b56e897de)
    - Podemos observar un mensaje que nos indica que tenemos un error en los servicios HDFS, para poder solucionar ese error, vamos a
    realizar los siguientes pasos:
    - Entraremos al por SSH al nodo master del cluster, esto lo podemos hacer entrando al nodo master en el servicio ec2.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/d8e20542-62a3-4f76-bd17-436106dfe588)
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/24292823-7324-47e4-bc9c-47bb89195c25)
    - Entrar al EC2 master por medio de SSH:
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/f6fdf52a-664a-4a39-96ef-f5db9219280e)
    - Realizamos los siguientes comandos:
    - Ejecuta el siguiente comando para editar el archivo hue.ini:
    ```
    sudo sed -i 's/.ec2.internal:14000/.ec2.internal:9870/' /etc/hue/conf/hue.ini
    ```
    - A continuación, reinicia el servicio hue:
    ```
    sudo systemctl restart hue
    ```
    - Con estos pasos debemos poder solucionar el error, y veriamos lo siguiente en el servicio Hue:
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/2aa51d56-b582-4727-8873-6a345ccc1cdb)
    - Ya podriamos crear y subir cualquier archivo que necesitemos para HDFS.

    
- Uso de JupyterHub y Zeppelin
  - Acceso a JupyterHub
    - Conectar a JupyterHub usando la URL y el puerto configurado (9443).
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/b2ab57f6-97ca-4827-bb5b-d90d09dd88c5)
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/01e1cfc5-eb46-4a29-aeda-b9e185494ce4)
    - Crear un usuario y contraseña la primera vez que se ingrese.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/0aa2fd20-8bb8-4324-bab6-83471ccd1025)
      - Utilizar el usuario por defecto:
        - jovyan
        - jupyter
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/23164d8d-fc75-4b5f-a7ea-f53d91bfeb79)
  - Creación y Almacenamiento de Notebooks
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/8b9f5c7e-54a1-474d-a535-aeb1fd97c9af)
    - Crear notebooks en JupyterHub.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/00735ddd-c04f-4779-91a7-c73358de4d19)
    - Asegurarse de que los notebooks se almacenan en S3 para evitar la pérdida de datos.
      - ponemos otro nombre al notebook para verificar
      ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/403163a9-6506-4a6a-9f4f-7c19588a14e7)
      ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/b4634b0e-906f-48af-8d59-9bf43f98c646)
      ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/28fc70ea-b1a7-438b-abf8-eadebb2d9595)

  - Configuración de Spark en JupyterHub
    - Verificar las variables spark y SparkContext para confirmar que Spark está configurado correctamente.
  - Uso de Zeppelin
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/2b84d53a-8712-4bb1-8ba8-ca3f9fa075fa)
    - Conectar a Zeppelin usando el puerto 8890.
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/15fad67b-9fd9-471d-8343-77a727ef6189)
    - Creamos un nuevo "note"
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/00e9580a-2a66-4273-be43-753fc2a07022)
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/6cea8361-14e8-428c-93b6-60f1f2488e8f)
    - Haciendo los siguientes comandos  podemos confirmar que ya tenemos conexiones spark
    ![image](https://github.com/migueflorez10/Laboratorio_3-1/assets/68928440/8493fbf1-95fc-4392-b17f-4f39cf8890d0)
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
