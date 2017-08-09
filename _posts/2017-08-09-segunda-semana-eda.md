---
layout: post
title: Segunda semana de EDA
tags: [apuntes, eda, programacion]
source: https://drive.google.com/file/d/0BxXdSp4t_SZeZ1dnSnc0XzJ6UnBVMlVoaDAta3F6Y3ZsSGs0/view?usp=sharing
---

Las __estructuras de datos__ se dividen en estáticas y dinámicas. En esta semana veremos las primeras, ya que a lo largo del curso nos enfocaremos en las segundas.

Estructuras de datos estáticas:


Son mecanismos que proveen los lenguajes d eprogramación para almacenar datos en memoria del computador durante la ejecución del programa. Existen dos categorías:
- __Estructuras estáticas:__ Son aquellas en las que la cantidad de memoria necesaria se determina en forma previa a ejecutarse el programa.
    - Arreglos.
    - Arreglos con tope.
    - Matrices.
-__Estructuras dinámicas:__ Son aquellas en las que la cantidad de memoria necesaria se deermina durante la ejecución del programa.
    - Listas
    - Árboles

>Nota: Doy solo dos ejemplos de estructuras dinámicas ya que las veremos más adelante con detalle, y no las listamos en clase.


#__Estructuras estáticas__:

##__Arreglos__

Un arreglo es una secuencia de N valores, todos ellos del mismo tipo, siendo N un valor constante que se define en forma previa a la ejecución del programa.
Ejemplo:

    int arreglo[5];

La variable con el nombre "arreglo" guarda 5 espacios iguales en memoria para almacenar 5 números. Cada espacio cuenta con un súbindice indicando el "lugar" correspondiente. Dicho subíndice va de 0 a N-1, en este caso de 0 a 4.

    arreglo[5] = [ ] [ ] [ ] [ ] [ ]
                  0   1   2   3   4

##__Arreglos con tope__

Un arreglo con tope es como un arreglo común, pero con la diferencia de que no estamos obligados a cargar todas las posiciones, sino que vamos cargando los valores de a uno, teniendo un tope que nos indica cuántos elementos llevamos cargados hasta el momento.              
Ejemplo:

    typedef struct{
        int arreglo[5];
        int tope;
    } ArregloConTope;

Creamos un tipo de dato llamado "ArregloConTope" el cual cuenta con un arreglo de 5 espacios, y una variable "tope" que es la que usaremos como contador el cual se incrementará en 1 cada vez que agreguemos un número al arreglo.
Por lo tanto, si nuestro arreglo tiene asignado los primeros 2 subíndices, con los valores 10 y 27, y luego está vacío(indicamos que está vacío dejando todos los valores en 0, en este caso) nuestros datos quedarían de la siguiente manera:

    arreglo[5] = [10] [27] [0] [0] [0]
    tope = 2

Si agregamos el número 30 al arreglo:

    arreglo[5] = [10] [27] [30] [0] [0]
    tope = 3

Y si eliminamos el último número:

    arreglo[5] = [10] [27] [30] [0] [0]
    tope = 2

Cabe aclarar que el lenguaje C no cuenta con funciones para hacer esto automáticamente (si cuenta con ellas, lo cual es lo más probable, lo desconozco) por lo tanto hay que realizar todas estas funciones nosotros, lo cual vamos a practicar en los ejercicios planteados más adelante.

##__Matrices__

Los arreglos en C pueden tener múltiples subíndices. Un uso común es la representación de tablas de valores que constan de información organizada en filas y columnas. Para identificar un elemento particular de una tabla, debemos especificar dos subíndices: el primero(por convención) identifica la fila del elemento, y el segundo(por convención) identifica la columna del elemento.
Ejemplo:

    int matriz[5][6]

Esto se representaría de la siguiente manera

    matriz[5][6]= [ ] [ ] [ ] [ ] [ ]
                  [ ] [ ] [ ] [ ] [ ]
                  [ ] [ ] [ ] [ ] [ ]
                  [ ] [ ] [ ] [ ] [ ]
                  [ ] [ ] [ ] [ ] [ ]
                  [ ] [ ] [ ] [ ] [ ]

---
##__Modularización__

Modularizar nuestro código surge de la necesidad de mejorar la forma en que escribimos el código. En teoría podríamos escribir los programas más complejos en un solo archivo y sin usar funciones, pero esto haría que la complejidad al momento de mantenerlo o de agregar funcionalidades a nuestro programa sea imposible, o muy difícil y por lo tanto que no valga la pena el trabajo.
Así es como se pasó de la __programación lineal__ a la __programación estructurada__.

La programación estructurada es el paradigma de programación orientado a mejorar la calidad, claridad y tiempo de desarrollo de los programas informáticos.

En nuestro caso separaremos el código con los cabezales (o archivos .h) donde se definen las funciones y estructuras, y habrán tantos archivos .h como conjunto de problemas necesitemos solucionar. Ejemplo: si nuestro problema implica el uso de arreglos, arreglos con tope y matrices, y con ellos necesitamos hacer varias operaciones (agregar datos al arreglo, vaciarlos, ver si un valor pertenece a una matriz, etc) entonces haremos un arreglos.h, arreglosConTope.h y matrices.h. Con la definición de cada una de sus funciones en dicho archivo.
Cada archivo .h irá acompañado de su correspondiendo .cpp en donde se implementará la lógica de lo que definimos en el .h. Por lo tanto en el caso anterior tendríamos un arreglos.cpp, arreglosConTope.cpp y matrices.cpp.
Y luego un main.cpp donde se encontrará la lógica principal de nuestro programa, en donde se las funciones de cada archivo se unirán para realizar la solución a un problema dado.

La siguiente imagen es para visualizar lo anterior:
![image]({{site.url/img/eda/semana2/modularizacion.png}})

---

Dejo el link al código fuente del ejercicio sobre [estructuras estáticas](https://github.com/Ctrl4/Estructura-de-Datos-y-Algoritmos/tree/master/Semana%2002/estructuras_estaticas). La letra está en los __.h__ (arreglos.h,arreglosConTope.h,matrices.h). (Sin terminar)

---

##__Tipos abstractos de datos(TAD)__

El problema fundamental que se presenta en el desarrollo de programas está vinculado a la alta complejidad de los mismos. En la mayoría delos casos, dicha complejidad escapa a la posibilidad de una comprensión directa e inmediata de la totalidad del problema a resolver. Surge entonces la necesidad de una primera fase de análisis, previa a la implementación de un problema en un lenguaje de programación, cuyo objetivo fundamental es lograr una correcta comprensión del problema a resolver.
El análisis es el primer paso en la construcción de programas que permite obtener una descripción lo más precisa posible (aunque no necesariamente formal) de dicho problema. __Una manera__ de tratar con la complejidad de los problemas es _descomponer el problema en problemas más pequeños_, a su vez para resolver estos últimos puede volver a aplicarse el mismo cirterio y continuar con el proceso hasta poder resolverse sin necesidad de descomposición.
__Otra de las funciones del análisis__ es la de _reducir el problema estudiado_, o parte de él, _a problemas ya conocidos y resueltos_, de esa forma poder usar algunas de las soluciones que se conocen para dichos problemas. La abstracción en el análisis de un problema consiste en individualizar elementos de la realidad que interesan, así como su comportamiento, para luego traducir en operaciones que permiten su manipulación. Como ya sabemos un __tipo de datos__ es un __conjunto de valores,__ acompañado de un __conjunto de operaciones__ que determinan el comportamiento de esos valores. Lo que se está haciendo conceptualmente es individualizar los tipos de datos presentes en el problema. En particular estos tipos de datos identificados se dicen abstractos porque no se está trabajando aún con una implementación en particular.

Lo que hacemos en el análisis es __establecer las características__ que tendrán estos tipos de datos, pero sin definir aún estructuras de datos para su implementación. Lo que interesa es __definir qué operaciones__ interesa realizar sobre los elementos, pero sin definir aún ómo se implementarán dichas operaciones.

Recién a la hora de implementar la solución del problema es que se realiza una implementacón de los tipos abstractos identificados en la realidad, para lo que se elegirán las estructuras de datos más adecuadas para representarlos y se definirán algoritmos lo más eficiente posibles para manipular dichas estructuras. Veremos incluso que para un mismo tipo abstracto de datos, pueden existir diferentes estructuras posibles para su implementación. Incluso sucede que el análisis puede realizarse en forma independiente de la elección del lenguaje de programación concreto a utilizar. Los tipos abstractos de datos que pueden aparecer en las diferentes realidades no son muchos, y podemos agruparlos en familias de acuerdo al comportamiento.

Podemos clasificar los Tipos Abstractos de Datos en las siguientes categorías:
- __Elementales:__ También conocidos como primitivos, incluye aquellos que son indivisibles. Ejemplo: enteros, reales, caracteres y booleanos, etc.
- __Intermedios:__ Incluye aquellos tipos abstractos de datos que representan entidades de la realidad del problema a resolver, como por ejemplo las estructuras.
- __Colecciones:__ Son aquellos tipos abstractos de datos que representan agrupaciones de elementos (ya sean elementales o intermedios) dentro de la realidad del problema a resolver.

Nos centraremos particularmente en el análisis de los diferentes tipos de colecciones que podemos representar en una realidad. En general, todas las colecciones se construyen de la misma manera, en forma inductiva, originalmente es una colección vacía y luego le vamos agregando de a un nuevo elemento. Lo que diferencia a los distintos tipos de colección es su comportamiento. Dependiendo de la forma como se agrupan los elementos de la colección y el tratamiento de los mismos se definen diferentes tipos de colecciones.

---

Después del choclo anterior de texto el cual es sacado del archivo que envió el profesor agregado en la [fuente]({{source}}) dejo el link al ejercicio de [tipos abstractos de datos](https://github.com/Ctrl4/Estructura-de-Datos-y-Algoritmos/tree/master/Semana%2002/tipos_abstractos_de_datos).
