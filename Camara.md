# Diagrama de bloques
El Módulo de la cámara y el procesamiento de imágen están basados en el siguiente diagrama de bloques para su funcionamiento

## Configuración de la cámara (I2C)

<p align="center">
  
![Screenshot](/Imagenes/diagramabloques.png) 


## Datos de entrada
Los datos de entrada son los cables de la cámara con sus señales principales los cuales son
```verilog
input wire CAM_pclk,		// El cual es la señal PCLK de la camara que hace referencia al clock para cada pixel. 
input wire CAM_href,		// El cual es la señal HREF de la camara que es la señal de referencia horizontal. 
input wire CAM_vsync,		// El cual es la señal VSYNC de la camara.
input wire [7:0]CAM_px_data,    // El cual corresponde a los 8 pines de datos de la camara.
input wire init_procesamiento,  // Señal de inicializacion para el procesamiento
```

## Captura y conversión de datos
Mediante el módulo "camread.v" se hace la captura de datos y su respectiva


## Dual port RAM (Buffer de memoria)


## Procesamiento de imágen


## Datos de salida

