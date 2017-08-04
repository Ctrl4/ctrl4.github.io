---
layout: post
title: Primera semana de MDL2
---

Mientras estaba en clase, pensaba *¡Hostia, como madres escribo esto en el blog!*, ya que la profesora, Elisa Rocha, (la cual explicaba muy bien), empezó la explicación con un "juego", y los ejemplos para empezar a hablar de grafos eran como anécdotas.
Sin embargo al rato pude agarrarle la mano a la estructura de la clase y ahí me decidí escribir acá las definiciones que ella hacía y mostrar los ejemplos dados en clase, intercalando con ejercicios del práctico.

---

El temario del curso será el siguiente:
- Teoría de grafos. Hasta el primer parcial (50 puntos)
- Lógica de predicados. Hasta el segundo parcial (50 puntos)

Bibliografía:
- Teoría de grafos:
    - Grimaldi. Matemática Discreta
    - Notas.
- Lógica de predicados:
    - No dijo.

---
> Antes de comenzar quisiera acotar sobre una web que encontré mientras buscaba alguna forma para poder mostrar el dibujo de los grafos en este blog, ya que si escaneo mis dibujos de la cuadernola sería impresentable. Encontré [esta web](http://graphs.grevian.org/) la cual explica la sintaxis para utilizar con el programa llamado [graphviz](http://graphviz.org/), y además cuenta con una pestaña en la propia página donde podés escribir la definición de los grafos y la misma página te renderea el resultado de manera online, sin tener que instalar nada.

> Un ejemplo muy sencillo de la sintaxis que se necesita para realizar un grafo dirigido del vértice a al vértice b sería el siguiente

    digraph{
        a->b;
    }

> Cuyo resultado sería este:

> ![image]({{site.url}}/img/digraph_a-b.png)

> Y en el caso de un grafo no dirigido tambien de a hacia b:

    graph{
        a -- b;
    }

> Resultado:

> ![image]({{site.url}}/img/graph_a-b.png)

> Graphviz cuenta con otras opciones que por el momento no he probado, y mostraré a medida que las vaya necesitando en el correr del curso.

---

Ahora si, empezando con matemática discreta y lógica 2.

Si tenemos las siguientes 4 figuras:

1) ![image]({{url.site}}/img/mdl2/clase1/ejemplo1.png)
2) ![image]({{url.site}}/img/mdl2/clase1/ejemplo2.png)
3) ![image]({{url.site}}/img/mdl2/clase1/ejemplo3.png)
4) ![image]({{url.site}}/img/mdl2/clase1/ejemplo4.png)

¿Cuáles de estas 4 imágenes podrían dibujarse sin levantar el lapiz? Entendiendo que sólamente se pueden repetir los vértices (circulos con letras adentro) y no las aristas(líneas que unen a los vértices).

1) Pasos para dibujar la figura 1 sin levantar el lápiz (usando una sintaxis parecida a la que utiliza graphviz):
- d -- c
- c -- b
- b -- a
- a -- d
- d -- e
- e -- a
- a -- c

2) Pasos para dibujar la figura 2 sin levantar el lápiz:
- c -- d
- d -- a
- a -- e
- e -- d
- d -- b
- b -- c
- c -- a
- a -- b

3) Pasos para dibujar la figura 3 sin levantar el lápiz:
- a -- d
- d -- e
- e -- a
- a -- b
- b -- g
- g -- c
- c -- f
- f -- d
- d -- c
- c -- b

>Nota: Estas no son las únicas soluciones, ni las mejores, deben haber más y son igualmente correctas.

4) Pasos para dibujar la figura 4 sin levantar el lápiz:
- No hay forma de dibujar la digura 4 sin levantar el lápiz.

¿Por qué?

---

Esto nos lleva a sacar las siguientes conclusiones:
- Para demostrar algo que tiene solución, solo basta con dar la solución o una de las varias que tenga.
- En caso contrario, ya que en la mayoría de las situaciones sería imposible demostrar de forma exhaustiva (Esto significa, demostrando que todos los casos posibles no son una solución), hace falta dar un argumento de porque no se puede resolver. No basta con intentar y no poder.

---

**Definiciones: **
- Grafo: Conjunto de objetos llamados vértices o nodos unidos por enlaces llamados aristas o arcos, que permiten representar relaciones binarias  entre elementos de un conjunto.

Se representa G=(V,A)

- Vertice: Es la unidad fundamental de la que se conforman los grafos. Un grafo no dirigido está formado por un conjunto de vértices y un conjunto de aristas (pares no ordenados de vértices), mientras que un grafo dirigido está compuesto por un conjunto de vértices y un conjunto de arcos (pares ordenados de vértices). En este contexto, los vértices son tratados como objetos indivisibles y sin propiedades, aunque puedan tener una estructura adicional dependiendo de la aplicación por la cual se usa el grafo.

Se representa V={a,b,c}

- Arista: En teoría de grafos, una arista corresponde a una relación entre dos vértices de un grafo.

Para caracterizar un grafo G son suficientes únicamente el conjunto de todas sus aristas, comúnmente denotado con la letra E (del término en inglés edge), junto con el conjunto de sus vértices, denotado por V. Así, dicho grafo se puede representar como G(V,E), o bien G = (V,E).

{% raw %}
A С VxV ={(α,β)/α€V,β€V} >Grafo dirigido
A С {{α,β}/α€V,β€V} >Grafo no dirigido

Se representa A={{c,b},{c,b}',{a,b}}
{% endraw %}
>Fuente:
> - [Grafos - Wikipedia](https://es.wikipedia.org/wiki/Grafo)
> - [Vértice - Wikipedia](https://es.wikipedia.org/wiki/V%C3%A9rtice_(teor%C3%ADa_de_grafos))
> - [Arista - Wikipedia](https://es.wikipedia.org/wiki/Arista_(teor%C3%ADa_de_grafos))
