El sensor ultrasonido utilizado para la realizacion del proyecto fue el HC-SR04. Este dispositivo fue usado con el proposito de realizar el mapeo del laberinto y asi poder detectar los obstaculos o en nuestro caso las paredes y del mismo modo los caminos que se encontraban libres. Por otra parte, primero observaremos el driver implementado para lograr un correcto funcionamiento de este dispositivo. 

Lo primero que se hace es que al ultrasoonido al recibir un pulso por el pin TRIG el cual es mayor a 10us, inicia la emision de la onda, y empieza un conteo en el modulo hasta que se recibe una onda similar a la enviada pero ahora por el pin de ECHO. Dado que la onda va hasta el objeto y rebota, el tiempo que se tiene es el doble del que se deberia tener en cuenta para el calculo de la distancia, ademas, de que se envia una onda sonora esta debido a que sabemos cual es la velocidad de esta, de este modo podemos realizar el calculo de la distancia asi: 


$Distancia=\frac{343m/s}{2}$

