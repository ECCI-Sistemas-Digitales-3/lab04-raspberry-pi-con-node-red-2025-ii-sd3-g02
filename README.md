[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=20959670&assignment_repo_type=AssignmentRepo)
# Lab04: Visualización de Datos en Raspberry Pi con Node-RED 

## Integrantes

Giselle Puentes Piñeros 31594  
Juan Pablo Ramirez 103681  
Nicolas Quiroga 109393  

## Documentación

Este flujo de Node-RED Dashboard permite capturar un color desde un selector gráfico (color picker), procesarlo a través de un nodo de función, y guardar el valor resultante en un archivo de texto local. El flujo simula el funcionamiento de un sistema analógico–digital–analógico, donde una señal analógica (color) se convierte en un valor digital procesado y almacenado. 

## Descripción de clases y componentes

### Señal analógica (Entrada)

Representa la fuente de datos que simula la lectura de un sensor analógico.  
En el flujo se utilizó un nodo **Color Picker**, equivalente a una variable analógica que cambia dinámicamente.  
Cada variación representa un valor que se desea muestrear y convertir.

**Método:**  
- Envía el valor analógico hacia el bloque de procesamiento (nodo *function*), donde se traduce a un formato digital interpretable.  

---

### Conversor ADC (Procesamiento)

Simula el proceso de **muestreo y cuantificación** de la señal analógica.  
Se implementa mediante un nodo **Function** que actúa como un bloque intermedio de conversión: recibe el valor continuo, lo convierte a formato digital (texto o número) y lo prepara para su almacenamiento.

**Métodos principales:**  
- `func`: procesa la entrada y retorna un mensaje digital (`msg`) que puede ser almacenado.  
- `debug`: permite observar el resultado digital en tiempo real, verificando la integridad del proceso.  

---

### Conversor DAC (Salida)

Corresponde al proceso de **reconstrucción** o almacenamiento de la señal digital convertida.  
En el flujo se representa con el nodo **File**, que guarda los datos recibidos en un archivo (`texto.txt`) dentro del sistema.  
De esta forma, se mantiene una traza persistente de las conversiones realizadas.

**Método:**  
- `file`: guarda los valores digitales recibidos, actuando como salida o memoria del sistema.  

---

### Interfaz de usuario

El laboratorio incluyó una capa de interacción mediante el **Dashboard de Node-RED**, donde el usuario puede:  
- Seleccionar el valor de entrada (simulando la señal analógica).  
- Observar en consola el resultado de la conversión digital.  
- Guardar la información generada.  

Esta capa de interfaz cumple el mismo rol que una GUI o terminal en Python, y permite visualizar el flujo completo de datos.

---

## Resumen del sistema

El proceso completo puede dividirse en tres etapas principales:

1. **Adquisición de señal analógica:** el usuario genera una entrada variable mediante un control gráfico.  
2. **Conversión y procesamiento digital:** el valor se interpreta y se formatea en un tipo de dato digital.  
3. **Almacenamiento y salida digital:** el valor digital se guarda en un archivo que representa la reconstrucción o persistencia de la señal.  

Este flujo permite comprender los pasos fundamentales de un sistema ADC/DAC real, desde la captura de una variable física hasta su representación y almacenamiento digital.

---

## Explicación de elementos técnicos

**Node-RED Dashboard:** permite la creación de interfaces visuales (sliders, color pickers, botones) que simulan entradas analógicas o digitales.  

**Function Node:** ejecuta fragmentos de código en JavaScript o Python que procesan la información.  

**Debug Node:** muestra en tiempo real los datos en la consola lateral, útil para validar el funcionamiento del flujo.  

**File Node:** administra la escritura de información en archivos, representando la salida o etapa DAC.  

**ID y flujo:** cada nodo está identificado por un `id` único que facilita la trazabilidad dentro del sistema.  

---

## Instrucciones de uso

1. **Ejecutar el programa**
   - Inicie Node-RED y abra el flujo del laboratorio.  
   - Despliegue el panel Dashboard para acceder a la interfaz gráfica.

2. **Generar una señal analógica**
   - Use el control *Color Picker* para variar un valor de entrada (puede interpretarse como voltaje o intensidad).  
   - Cada cambio genera un nuevo valor a procesar.

3. **Procesamiento digital**
   - El nodo *Function* recibe la entrada, la convierte a formato digital y la envía a los nodos de salida.  
   - Puede verificar el valor procesado en el panel *Debug*.

4. **Almacenamiento**
   - Los datos convertidos se guardan automáticamente en el archivo `texto.txt` en el directorio especificado.  
   - Este archivo representa el resultado digital final del proceso.

5. **Ver resultados**
   - Observe los valores almacenados para analizar el comportamiento del sistema.  
   - Puede modificar los valores de entrada y repetir la prueba para comparar resultados.
     
   ![Flujo del Laboratorio 4](lab%204.jpg)

   ![Flujo del Laboratorio 4](lab%204..jpg)

7. **Finalizar**
   - Detenga el flujo desde el panel de Node-RED o cierre la interfaz gráfica.


## Conclusiones

El laboratorio facilitó la comprensión de la interacción entre los dominios analógico y digital, demostrando cómo una señal continua puede ser convertida, procesada y almacenada dentro de un sistema digital controlado.
A pesar de haberse desarrollado en un entorno simulado, los conceptos y procedimientos aplicados reflejan fielmente el funcionamiento de un sistema real de adquisición y procesamiento de datos, que integra sensores, convertidores y actuadores.

