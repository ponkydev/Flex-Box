# Propiedades de Flex-box

## Propiedades del Contenedor Flex:

1. display: flex: Activa Flexbox en un contenedor.

2. flex-direction: Define la dirección de los elementos dentro del contenedor.
    * Valores: row, column, row-reverse, column-reverse.

3. flex-wrap: Controla si los elementos deben ajustarse en varias filas o columnas si no caben en una línea.
    * Valores: wrap, no-wrap, wrap-reverse.

4. justify-content: Alinea los elementos en el eje principal (horizontal si es row, vertical si es column).
    * Valores: flex-start, flex-end, center, space-between, space-around, space-evenly.

5. align-items: Alinea los elementos a lo largo del eje cruzado (perpendicular al eje principal).
    * Valores: flex-start, flex-end, center, baseline, stretch.

6. align-content: Alinea las filas del contenedor cuando hay espacio extra en el eje cruzado.
    * Valores: flex-start, flex-end, center, space-between, space-around, stretch.

## Propiedades de los Elementos Flex:

1. order: Cambia el orden en que los elementos aparecen en el contenedor, sin alterar el HTML.
    * Valor: Un número (por defecto es 0).

2. flex-grow: Define cuánto puede crecer un elemento en relación con los demás.
    * Valor: Un número (por defecto es 0, lo que significa que no crecerá).

3. flex-shrink: Define cuánto puede reducirse un elemento en relación con los demás cuando hay poco espacio.
    * Valor: Un número (por defecto es 1, lo que significa que puede encogerse).

4. flex-basis: Especifica el tamaño base inicial de un elemento antes de aplicar flex-grow o flex-shrink.
    * Valores: Un tamaño (px, %, etc.) o auto.

5. align-self: Permite que un elemento se alinee de manera diferente al resto en el eje cruzado.
    * Valores: auto, flex-start, flex-end, center, baseline, stretch.

## Flex (Shorthand):

* La propiedad flex es una abreviación que combina tres propiedades relacionadas con el comportamiento flexible de los elementos:

    1. flex-grow: La capacidad de un elemento para crecer si hay espacio disponible.
    2. flex-shrink: La capacidad de un elemento para encogerse si hay poco espacio.
    3. flex-basis: El tamaño inicial del elemento antes de aplicar grow o shrink.

* La sintaxis general es: 

```css
flex: <flex-grow> <flex-shrink> <flex-basis>;
```

* Ejemplos:

    * flex = 1;
    Es un atajo para flex: 1 1 0%;, lo que significa que el elemento puede crecer y encogerse igualmente, ocupando todo el espacio disponible.

    * flex = 0 1 auto;
    Esto es el valor por defecto. Significa que el elemento puede encogerse, pero no crecerá más allá de su tamaño contenido.

    * flex = 2 1 10rem;
    Esto significa que el elemento tiene un tamaño base de 10rem, puede crecer al doble de la velocidad que otros elementos (flex-grow: 2), y puede encogerse si no hay suficiente espacio.