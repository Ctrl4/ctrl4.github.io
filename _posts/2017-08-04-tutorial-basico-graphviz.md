---
layout: post
title: Tutorial básico de Graphviz para matemática discreta (Actualizable)
---

Como me di cuenta que el post de [discreta 2]({{site.url}}/2017-08-04-primer-semana-mdl2/) se me iba a hacer demasiado largo si al comienzo del mismo explicaba cosas básicas de Graphviz _(el programa que encontré para poder dibujar de forma sencilla y prolija los grafos con los que vamos a trabajar en la materia)_ decidí crear un nuevo post en cual ir actualizando a medida que vaya siendo necesario, como utilizar este software.

---

Un ejemplo muy sencillo de la sintaxis que se necesita para realizar un grafo dirigido del vértice a al vértice b sería el siguiente

    digraph{
        a->b;
    }

Cuyo resultado sería este:

![image]({{site.url}}/img/digraph_a-b.png)

Y en el caso de un grafo no dirigido tambien de a hacia b:

    graph{
        a -- b;
    }

Resultado:

![image]({{site.url}}/img/graph_a-b.png)

Para realizar un grafo no dirigido de a hacia b, b hacia c y c hacia a, con un camino que vaya de a hacia c pasando por b, se escribe de la siguiente forma:

    graph{
        a -- b -- c[color = red, penwidth=3.0 ];
        a -- c;
    }

![image]({{site.url}}/img/graph_camino.png)

Graphviz cuenta con otras opciones que por el momento no he probado, y mostraré a medida que las vaya necesitando en el correr del curso.
