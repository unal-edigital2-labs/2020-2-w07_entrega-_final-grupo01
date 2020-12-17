El sensor ultrasonido utilizado para la realizacion del proyecto fue el HC-SR04. Este dispositivo fue usado con el proposito de realizar el mapeo del laberinto y asi poder detectar los obstaculos o en nuestro caso las paredes y del mismo modo los caminos que se encontraban libres. Por otra parte, primero observaremos el driver implementado para lograr un correcto funcionamiento de este dispositivo. 

Lo primero que se hace es que el ultrasoonido al recibir un pulso por el pin TRIG el cual es mayor a 10us, inicia la emision de la onda, y empieza un conteo en el modulo hasta que se recibe una onda similar a la enviada pero ahora por el pin de ECHO. Dado que la onda va hasta el objeto y rebota, el tiempo que se tiene es el doble del que se deberia tener en cuenta para el calculo de la distancia, ademas, de que se envia una onda sonora esto debido a que conocemos la velocidad del sonido, de este modo podemos realizar el calculo de la distancia asi: 

Distancia=Tiempo*342/2

Ademas, debemos tener en cuenta que para la contruccion del driver y el contador se hace uso de una señal de cierta frecuencia conocida, con la cual podremos aumentar el contador cada vez que detecte un flanco de subida, lo que nos permitira a al final obtener una relacion entre los ciclos por cada unidad de distancia. Ahora pasando a la construccion del driver tendremos que, lo primero que se debe hacer es el divisor de frecuencia, en el cual pasaremos de los 100MHz a 34.2KHz


```verilog

module	divisorfrec	#(
				parameter top=12'b101101101100
			)
			(
				input           clk,
				output	reg	CLKOUT
			);

	reg [11:0] count_2924;
	
	initial
	begin
		CLKOUT=1'b1;
		count_2924=0;
	end
	
	always @(posedge clk) 
	begin
		count_2924 <= count_2924 + 1;
		if(count_2924 == top)
		begin
			count_2924<=0;
			CLKOUT <= ~CLKOUT;
		end
	end
endmodule

```

Ahora con este nuevo reloj del sistema sabemos que sera necesario un contador para saber el tiempo que pasa entre la salidad de la señal por el pin TRIG hasta las llegada del mismo por el pin de ECHO. Para ello hacemos uso de la siguiente funcion If-else la cual nos indicara cuando debe empezar a contar el reloj, la cual sera dada por el momento en que la señal que fue enviaba llegue hasta el pin ECHO.

``` verilog
if(reset)
		begin
			count0=0;
			calculate=0;
			pulse=0;
		end

		else
		begin
			if(ENABLE)
			begin
				pulse=1'b1;
			end
			
			if(ECHO)
			begin
				count0=count0+1;
			end
			
		end
	end

```

Con base en lo anterior y dado que ya tenemos la informacion del tiempo que demora la señal en ir hasta el objeto y regresar procedemos a calcular la distancia a la que se encuentra. A continuacion encontramos la caja negra que representa el ultrasonido junto con todas sus entradas y salidas 



