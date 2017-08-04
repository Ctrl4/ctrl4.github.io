---
layout: post
title: Primera semana de MDL2
---

Mientras estaba en clase, pensaba *¡Hostia, como madres escribo esto en el blog*, ya que la profesora, Elisa Rocha, (la cual explicaba muy bien), empezó la explicación con un "juego", y los ejemplos para empezar a hablar de grafos eran como anécdotas.
Sin embargo al rato pude agarrarle la mano a la estructura de la clase y ahí me decidí a escribir acá las definiciones que ella hacía y mostrar los ejemplos dados en clase, intercalando con ejercicios del práctico.

---

Antes de comenzar quisiera acotar sobre una web que encontré mientras buscaba alguna forma para poder mostrar el dibujo de los grafos en este blog, ya que si escaneo mis dibujos de la cuadernola sería impresentable. Encontré [esta web](http://graphs.grevian.org/) la cual explica la sintaxis para utilizar con el programa llamado [graphviz](http://graphviz.org/), y además cuenta con una pestaña en la propia página donde podés escribir la definición de los grafos y la misma página te renderea el resultado de manera online, sin tener que instalar nada.

Un ejemplo muy sencillo de la sintaxis que se necesita para realizar un grafo dirigido del vértice a al vértice b sería el siguiente

    digraph{
        a->b;
    }

Cuyo resultado sería este:

![image]({{site.url}}/img/digraph_a-b.png)

Graphviz cuenta con otras opciones que por el momento no he probado, y mostraré a medida que las vaya necesitando en el correr del curso.
