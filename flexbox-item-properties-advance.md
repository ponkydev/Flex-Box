# ¿Como Flexbox calcula el tamaño de los elementos?
Lo primero que flexbox hace en su valor por defecto es mirar el tamaño del contenido para ocupar el tamaño maximo de el(max-content). El valor max-content hace que un texto ocupe el espacio necesario para no crear saltos de linea pero en flexbox cuando un item tiene demasiado contenido (En este caso texto) el width sera encogido para respetar el width del contenedor con ancho definido (Ya sea width o flex-basis) mas cercano a el o el del body.

## ¿Como flex-shrink decide que tanto encoger cada flex-item?
flex-shrink toma el ancho del contenedor con ancho definido o body y lo distribuye entre todos los items dependiendo su tamaño establecido o el valor que se le haya dado a la propiedad flex-shrink.

Ejemplo: si tenemos tres items, dos de ellos con 300px y uno con 600px y el contenedor tiene un ancho definido de 600px, los items que tenian 300px ahora tendran 150px y el que tenia 600px ahora tendra 300px, esto se hace para no perder la relacion de aspecto. Pero si el item que tenian 600px tienen un valor de 2 en la propiedad flex-shrink se encogera el doble de rapido que los demas, este ahora tendran la 200px al igual que los demas, ya que intentaran ocupar el total del ancho del contenedor.

## Funcionamiento de flex-basis:
flex-basis se utiliza para especificar el ancho o alto de un flex-item dependiendo de cual sea su main-axis (si el valor de flex-direction es column el main-axis sera el y-axis o el axis vertical, si es row el main-axis sera el x-axis o el axis horizontal), si el main-axis es el y-axis el valor de flex-basis se aplicara al height y si main-axis es el x-axis el valor del flex-basis se aplicara al width.

Esta propiedad sera sobre-escrita por un max-width o por un max-height. Al igual que min-width o min-height sobre-escribe a max-width y max-height.

## Flexbox solo se fija en el tamaño del contenido
Cuando trabajamos con flexbox para definir el tamaño de las columnas y filas este solo se fija en el tamaño del contenido obviando el padding y el border. Esto es una manera en la que flexbox trabaja para evitar que el border o el padding crezcan o se encogan al tener diferentes anchos en el contenedor. Esto funciona gracias a que flexbox resta la cantidad de border y/o padding a las medidas del contenedor para distribuir el espacio entre los elementos y al final agrega el padding y/o border al elemento.