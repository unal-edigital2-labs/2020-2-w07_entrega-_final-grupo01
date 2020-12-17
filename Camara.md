# Diagrama de bloques
El Módulo de la cámara y el procesamiento de imágen están basados en el siguiente diagrama de bloques para su funcionamiento

<p align="center">
  
![Screenshot](/Imagenes/diagramabloques.png) 


## Configuración de la cámara (I2C)
Mediante el archivo "OV7670_SETUP_i2c.ino" se realiza la configuración de la cámara para establecer los valores del formato que enviará la cámara

```c
OV7670_write(0x12, 0x0C);  //COM7: Establece QCIF y RGB
OV7670_write(0x11, 0xC0);  //CLKR: Set internal clock to use external clock
OV7670_write(0x0C, 0x08);  //COM3: Habilita la Escala de tamaño
OV7670_write(0x3E, 0x00);
OV7670_write(0x40,0xD0);   //COM15: Establece RGB 565

//Color Bar                // Establece el test de barra de colores
OV7670_write(0x42, 0x08);    
OV7670_write(0x12, 0x0E);

OV7670_write(0x3A,0x04);
OV7670_write(0x14,0x18);   // control de ganancia 

OV7670_write(0x17,0x14);   //cambia hstart
OV7670_write(0x18,0x02);   // cambia hstop
OV7670_write(0x32,0x80);   // href deja el valor qye  viene por default
OV7670_write(0x19,0x03);   // vref start
OV7670_write(0x1A,0x7B);   // vref stop
OV7670_write(0x03,0x0A);   // cambia vref
```
## Datos de entrada
Los datos de entrada son los cables de la cámara con sus señales principales los cuales son
```verilog
input wire CAM_pclk,		// El cual es la señal PCLK de la camara que hace referencia al clock para cada pixel. 
input wire CAM_href,		// El cual es la señal HREF de la camara que es la señal de referencia horizontal. 
input wire CAM_vsync,		// El cual es la señal VSYNC de la camara que es la señal de referencia para imagen.
input wire [7:0]CAM_px_data,    // El cual corresponde a los 8 pines de datos de la camara.
input wire init_procesamiento,  // Señal de inicializacion para el procesamiento
```

## Captura y conversión de datos
Mediante el módulo "camread.v" se hace la captura de datos y su respectiva conversión


## Dual port RAM (Buffer de memoria)
Mediante el módulo "buffer_ram_dp.v" se hace el almacenamiento de datos en el buffer o FIFO para posteriormente procesarlos o enviarlos a la VGA

## Procesamiento de imágen


## Datos de salida

```verilog
output wire [1:0] color,   // Salida de referencia del color procesado.
output wire [1:0] figure,  // Salida de referencia de la figura procesada.
output  wire  done,
output wire CAM_xclk,      // System  clock input de la camara.
output wire CAM_pwdn,      // Power down mode.
output wire CAM_reset,     // Reset para borrar los registros de la camara.
output wire VGA_Hsync_n,   // Salida de sincronizacion Horizintal para la VGA.
output wire VGA_Vsync_n,   // Salida de sincronizacion Vertical para la VGA.
output wire [3:0] VGA_R,   // Salida de 4 bits VGA roja
output wire [3:0] VGA_G,   // Salida de 4 bits VGA verde.
output wire [3:0] VGA_B,   // Salida de 4 bits VGA azul.
```
