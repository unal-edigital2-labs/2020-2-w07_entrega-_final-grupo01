Para el movimiento del carrito se hizo uso de dos motores DC en conjunto con un puente H L298, esto para evitar que debido a un pico elevado de corriente se genera un daño en la tarjeta de arduino, las conexiones realizadas son las que podemos observar en la imagen que se encuentra a continuacion: 

![Screenshot](PuenteH.jpg) 

Observamos como se controlara el movimiento de los motores mediante el uso de arduino donde se polarizara cada uno de los motores dependiendo la accion que se necesite. Iniciaremos primero  para el caso de que el movimiento requerido sea hacia adelante, caso en el cual se polarizaran ambos motores de igual forma como se muestra a continuacion

``` 

void Adelante() {
  digitalWrite(Motor1_1, LOW);
  digitalWrite(Motor1_2, HIGH);
  digitalWrite(Motor2_2, HIGH);
  digitalWrite(Motor2_1, LOW);
}

```
Ahora si el movimiento requerido es hacia retroceder, se debe polarizaciar todo al contrario de como lo tenemos en la parte anterior, asi obtendremos el siguiente codigo: 

``` arduino

void Adelante() {
  digitalWrite(Motor1_1, HIGH);
  digitalWrite(Motor1_2, LOW);
  digitalWrite(Motor2_2, LOW);
  digitalWrite(Motor2_1, HIGH);
}

```

Ahora en los casos donde el movimiento sea hacia los lados, se deber asegurar que el robot gire sobre su propio eje 
