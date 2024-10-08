# ¿Como Flexbox calcula el tamaño de los elementos?
Lo primero que flexbox hace en su valor por defecto es mirar el tamaño del contenido para ocupar el tamaño maximo de el(max-content). El valor max-content hace que un texto ocupe el espacio necesario para no crear saltos de linea pero en flexbox cuando un item tiene demasiado contenido (En este caso texto) el width sera encogido para respetar el width del contenedor con ancho definido (Ya sea width o flex-basis) mas cercano a el o el del body (Esto siempre que el flex-shrink tenga un valor distinto de 0).

## Funcionamiento de flex-grow:
flex-grow es una propiedad de Flexbox que determina cómo un flex-item (Elemento dentro del contenedor flex) puede crecer para ocupar el espacio adicional en su contenedor. Se define como un número que representa la proporción de espacio que cada elemento debe ocupar. Cuando hay espacio disponible, Flexbox utiliza este valor para calcular cuánto crecerá cada elemento en relación con los demás.

Formula que utiliza: Espacio disponible * (valor de flex-grow / suma de todos los valores flex-grow)

## ¿Como flex-shrink decide que tanto encoger cada flex-item?
flex-shrink toma el ancho del contenedor con ancho definido o body y lo distribuye entre todos los items dependiendo su tamaño establecido o el valor que se le haya dado a la propiedad flex-shrink.

Ejemplo: si tenemos tres items, dos de ellos con 300px y uno con 600px y el contenedor tiene un ancho definido de 600px, los items que tenian 300px ahora tendran 150px y el que tenia 600px ahora tendra 300px, esto se hace para no perder la relacion de aspecto. Pero si el item que tenian 600px tienen un valor de 2 en la propiedad flex-shrink se encogera el doble de rapido que los demas, este ahora tendran la 200px al igual que los demas, ya que intentaran ocupar el total del ancho del contenedor.

## Funcionamiento de flex-basis:
flex-basis se utiliza para especificar el ancho o alto de un flex-item dependiendo de cual sea su main-axis (si el valor de flex-direction es column el main-axis sera el y-axis o el axis vertical, si es row el main-axis sera el x-axis o el axis horizontal), si el main-axis es el y-axis el valor de flex-basis se aplicara al height y si main-axis es el x-axis el valor del flex-basis se aplicara al width.

Esta propiedad sera sobre-escrita por un max-width o por un max-height. Al igual que min-width o min-height sobre-escribe a max-width y max-height.

## Funcionamiento del shorthand flex:
flex es un shorthand para flex-grow, flex-shrink y flex-basis en ese mismo orden. Cuando solo le damos el valor del numero uno este agrega los siguientes valores a las propiedades que almacena: flex-grow: 1; flex-shrink: 1, flex-basis: 0;. Como podemos observar, el flex-basis tiene el valor de 0, lo que significa que el ancho o el alto del elemento tendra 0px pero como flex-grow tiene el valor de 1, este se agrandara hasta ocupar el espacio suficiente del contenido del elemento.

* Nota: Cuando el flex-basis tiene el valor de 0 y flex-grow de 1, el elemento quiere hacerse mas pequeño pero el flex-grow lo agranda para que quepa el contenido, por el contrario, cuando flex-basis tiene el valor de 100% el elemento quiere hacerse mas grande, pero el flex-shrink lo encoge hasta el tamaño del contenedor o del contenido.

## Flexbox solo se fija en el tamaño del contenido para distribuir el espacio entre elementos.
Cuando los elementos flex de un contenedor exceden el ancho total de este, flex-box distribuye el espacio disponible entre ellos, este solo se fija en el tamaño del contenido obviando el padding y el border (Al igual que content-box), osea que estas propiedades no participan en la distribucion de tamaños. Esto es una manera en la que flexbox trabaja para evitar que el border o el padding crezcan o se encogan al tener diferentes anchos en el contenedor.

* El tamaño de los elementos se ajustara de acuerdo al valor que tengan las demas propiedades de flex-box.

Ejemplo #1: si un flex-container tiene un ancho de 600px y tres flex-items, flex tiene un valor de 1 (flex-grow: 1; flex-shrink: 1, flex-basis: 0;) y uno de los elementos tiene un padding de 1rem (16px), flex-box primero restara los 32px del padding (16px de cada lado) al total de los 600px (igual a 568px), luego distribuira esos 568px entre los tres flex-items (Si todos tienen el mismo valor de flex-shrink) y al final agregara denuevo los 32px de padding al elemento que lo tenga, haciendo que este ocupe mas espacio que los demas (221.33px mientras los demas solo tendran 189.33px).

Ejemplo #2: tenemos la misma situacion que en el ejemplo pasado, pero esta vez flex-basis tiene un valor de 100% y el elemento con padding es el del medio, lo que flex-box hara es sumar el total del ancho que los elementos quieren alcanzar (600px + 568px (Este tiene padding de 1rem y flex solo se fija en el contenido, osea que el contenido solo ocupa 568px gracias a l padding) + 600px = 1768px), luego resta este total con el ancho del contenedor para obtener el espacio excedido (1,768px - 568px (flexbox toma el padding del elemento para agregarlo mas tarde) = 1,200px), ahora flex-box divide el espacio excedido sobre el total de la suma de los anchos de los elementos y lo multiplica por 100 para saber que porcentaje quitarle de ancho a cada elemento (1,200 / 1,768 * 100 = 67.87%): elemento #1 (67.87% de 600px = 407.22px); elemento #2 (67.87% de 568px = 385.5px); elemento #3 (67.87% de 600px = 407.22px);, al final cada elemento resultara con un ancho de (elemento #1: 600px - 407.22px = 192.78px; elemento #2: 568px - 385.5px = 182.5px + 32px (de padding) = 214.5px; elemento #3: 600px - 407.22px = 192.78px). Si sumamos el total del resultado del ancho de cada elemento obtendremos el total del ancho del contenedor (192.78px + 214.5px + 192.78px = 600px)

* Como podemos notar, flex-box funciona de manera distinta segun los valor que tengan sus propiedades y en todo momento nunca toma en cuenta el padding ni border para realizar sus distribuciones de espacio disponible y lo agrega al final, por eso el elemento con padding siempre ocupara mas espacio que los demas.