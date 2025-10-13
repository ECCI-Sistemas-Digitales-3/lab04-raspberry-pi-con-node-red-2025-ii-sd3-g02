[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=20959670&assignment_repo_type=AssignmentRepo)
# Lab04: Visualización de Datos en Raspberry Pi con Node-RED 

## Integrantes

Giselle Puentes Piñeros 31594  
Juan Pablo Ramirez 103681  
Nicolas Quiroga 109393  

## Documentación

El propósito de este laboratorio es desarrollar un sistema para la detección, visualización y registro de colores empleando una Raspberry Pi. El proyecto se implementa en Node-RED, aprovechando su entorno gráfico de programación por flujos. A través del dashboard de Node-RED, el usuario puede elegir un color, observar su equivalente en formato RGB y hexadecimal, y guardar los valores seleccionados en un archivo de texto, lo que permite su análisis posterior.

## Preparación del Entorno y Puesta en Marcha del Sistema

Para la correcta implementación del proyecto en la Raspberry Pi, fue necesario realizar una serie de configuraciones iniciales que permitieron establecer la comunicación remota, instalar el entorno de trabajo y garantizar su funcionamiento automático.

## Conexión Remota a la Raspberry Pi
El primer paso consistió en habilitar el acceso remoto mediante el protocolo SSH. Esto permitió conectarse a la Raspberry Pi desde otro dispositivo a través de la terminal. Para conocer la dirección IP del equipo, se utilizó el comando hostname -I, y posteriormente se estableció la conexión con la instrucción ssh usuario@direccion_IP. Esta configuración facilita la administración del sistema sin necesidad de utilizar periféricos adicionales.

## Instalación de Node-RED
Una vez establecida la conexión, se procedió con la instalación de Node.js, npm y Node-RED, utilizando el script oficial que automatiza el proceso. Durante la instalación se aceptaron las configuraciones por defecto y se incluyeron los nodos específicos para el hardware de la Raspberry Pi. Dado que el dispositivo posee recursos limitados, se recomendó iniciar Node-RED con un parámetro que optimiza el uso de memoria (node-red-pi --max-old-space-size=256), evitando errores de ejecución.

Tras la instalación, el entorno gráfico de Node-RED quedó disponible para ser accedido desde cualquier navegador conectado a la misma red local, ingresando la dirección del equipo seguida del puerto correspondiente (por ejemplo, http://<IP_Raspberry>:1880/ui).

## Ejecución Automática como Servicio
Para que Node-RED se iniciara automáticamente al encender la Raspberry Pi, se configuró como un servicio del sistema. Esto se logró mediante los comandos sudo systemctl enable nodered.service y sudo systemctl start nodered.service, asegurando que la aplicación permaneciera activa incluso después de cerrar la sesión SSH. Además, fue posible verificar su estado y revisar los registros en tiempo real mediante systemctl status nodered.service y journalctl -u nodered -f.

## Instalación del Panel de Control (Dashboard)
Finalmente, se añadió el paquete de nodos necesario para construir la interfaz gráfica del usuario. Desde el menú de Node-RED, se accedió a la opción Manage palette → Install y se instaló el complemento node-red-dashboard. Con esta herramienta, el sistema adquirió una interfaz visual que permite la interacción directa con los flujos desarrollados, accesible también desde cualquier navegador dentro de la red local.


## Configuración de Nodos en Node-RED

En esta etapa del proyecto se definió la estructura y el funcionamiento de los nodos dentro del flujo de trabajo en Node-RED. Cada nodo cumple un rol específico en la captura, visualización y almacenamiento de los colores seleccionados a través de la interfaz gráfica.

## Nodo Selector de Color (Color Picker)
Este nodo, perteneciente al dashboard, permite al usuario elegir un color desde una paleta visual. Se configuró dentro del grupo Default con la etiqueta “Selector de color”. El formato de salida se estableció en hexadecimal (por ejemplo, #0800ff), lo que facilita la representación precisa del color en la interfaz y su posterior conversión a otros formatos.

## Nodo de Entrada de Texto (Text Input)
También ubicado en el grupo Default, este nodo muestra los valores RGB correspondientes al color seleccionado. Se añadió un mecanismo de validación para asegurar que los valores introducidos sigan el formato R,G,B, garantizando que cada componente numérico se encuentre dentro del rango 0 a 255. Esta validación evita errores en la interpretación de los datos antes de su almacenamiento.

## Nodo de Almacenamiento (File Node)
Finalmente, el sistema integra un nodo encargado de registrar los colores seleccionados en un archivo de texto. La ruta de almacenamiento se definió como /home/pi/test.txt, aunque puede modificarse según la estructura de archivos del proyecto. Para verificar la información guardada, se puede acceder al contenido del archivo directamente desde la terminal de la Raspberry Pi mediante el comando nano test.txt.

     
   ![Flujo del Laboratorio 4](lab%204.jpg)

   ![Flujo del Laboratorio 4](lab%204..jpg)



## Conclusiones

La implementación del sistema de visualización y registro de colores en la Raspberry Pi permitió comprender de manera práctica la integración entre hardware, software y herramientas de programación visual como Node-RED. A través de este entorno, fue posible diseñar una interfaz intuitiva que facilita la interacción con el usuario y la gestión de datos en tiempo real.

El uso de nodos específicos, como el Color Picker, el Text Input y el File Node, demostró la flexibilidad de Node-RED para crear aplicaciones funcionales sin necesidad de programar desde cero, aprovechando flujos gráficos y configuraciones modulares. Además, la instalación y configuración del dashboard proporcionó un entorno visual atractivo y accesible desde cualquier dispositivo conectado a la misma red.

Configurar Node-RED como servicio del sistema aseguró su ejecución continua y automática, reforzando la estabilidad y autonomía del proyecto. Por otro lado, la optimización de memoria durante la ejecución permitió un rendimiento adecuado, considerando las limitaciones de hardware propias de la Raspberry Pi.

