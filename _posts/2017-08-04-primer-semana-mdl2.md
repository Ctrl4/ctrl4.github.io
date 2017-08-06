---
layout: post
title: Primera semana de MDL2(por terminar)
tags: [apuntes, mdl2, matematica]
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

> Clickeá [aquí]({{site.url}}/2017-08-04-tutorial-basico-graphviz) para el post que explicá las funciones básicas del programa.

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

__Definiciones:__
- Grafo: Conjunto de objetos llamados vértices o nodos unidos por enlaces llamados aristas o arcos, que permiten representar relaciones binarias  entre elementos de un conjunto.

Se representa G=(V,A)

- Vertice: Es la unidad fundamental de la que se conforman los grafos. Un grafo no dirigido está formado por un conjunto de vértices y un conjunto de aristas (pares no ordenados de vértices), mientras que un grafo dirigido está compuesto por un conjunto de vértices y un conjunto de arcos (pares ordenados de vértices). En este contexto, los vértices son tratados como objetos indivisibles y sin propiedades, aunque puedan tener una estructura adicional dependiendo de la aplicación por la cual se usa el grafo.

Se representa V={a,b,c}

- Arista: En teoría de grafos, una arista corresponde a una relación entre dos vértices de un grafo.

Para caracterizar un grafo G son suficientes únicamente el conjunto de todas sus aristas, comúnmente denotado con la letra E (del término en inglés edge), junto con el conjunto de sus vértices, denotado por V. Así, dicho grafo se puede representar como G(V,E), o bien G = (V,E).

{% raw %}

__Grafo dirigido:__

A С VxV ={(α,β)/α€V,β€V}

__Grafo no dirigido:__

A С {{α,β}/α€V,β€V}

Se representa A={{c,b},{c,b}',{a,b}}

>Por una _"falla en la matemática"_ no hay forma de representar si hay 2 vértices distintos a los mismos nodos. Por eso en el ejemplo anterior, en la arista {c,b} es distinto de la arista {c,b}'

{% endraw %}

>Fuente:
> - [Grafos - Wikipedia](https://es.wikipedia.org/wiki/Grafo)
> - [Vértice - Wikipedia](https://es.wikipedia.org/wiki/V%C3%A9rtice_(teor%C3%ADa_de_grafos))
> - [Arista - Wikipedia](https://es.wikipedia.org/wiki/Arista_(teor%C3%ADa_de_grafos))

---

__Ejemplo de grafo dirigido__

![image]({{url.site}}/img/mdl2/ejemplo_digraph.png)

V={a,b,c}
A={(a,b),(b,c),(a,c)}

---

__Definiciones:__
- Camino: Utilizando el lenguaje que veniamos utilizando, un camino es "algo que se dibuja sin levantar el lapiz"

O según [Wikipedia](https://es.wikipedia.org/wiki/Camino_(teor%C3%ADa_de_grafos)): En Teoría de Grafos, se llama Camino a una secuencia de vértices dentro de un grafo tal que exista una arista entre cada vértice y el siguiente. Se dice que dos vértices están conectados si existe un camino que vaya de uno a otro, de lo contrario estarán desconectados. Dos vértices pueden estar conectados por varios caminos. El número de aristas dentro de un camino es su longitud. Así, los vértices adyacentes están conectados por un camino de longitud 1, y los segundos vecinos por un camino de longitud 2.

__Ejemplo:__

![image]({{site.url}}/img/mdl2/clase1/ejemplo_camino.png)

    C=(d,c,b)
    C=(b,c,d) es un camino

{% raw %}
Si V={x1, x2,....xn}
   C=(Y1,Y2,...,Yn) es un camino si Y:€V∀i
   {Y1,Y2},{Y2,Y3},...,{Yk-1,Yk}
{% endraw %}

- Ciclo: Es un camino que empieza y termina en el mismo vértice. También se le puede llamar, camino cerrado o circuito.

Es decir

    C = (Y1,...,Yk)
    Y1 = Yk

__Ejemplo:__

![image]({{site.url}}/img/mdl2/clase1/ejemplo_ciclo.png)

    C=(d,c,b,a,d) Es un ciclo
    C=(d,c,e) No es un camino ni un ciclo

---

__Ciudades y Carreteras__
- Dado un grafo G decidir si es posible encontrar un __camino__ que __no repita aristas.__
- Dado un grafo G decidir si es posible encontrar un __ciclo__ que __no repita aristas.__

![image]({{site.url}}/img/mdl2/clase1/ejemplo_recorrido.png)

- 1)¿Es posible visitar todas las ciudades sin repetir ninguna?
- 2)¿Es posible sitar todas las ciudades sin repetir, empezando y terminando en la misma ciudad?

1)En el ejemplo si.

![image]({{site.url}}/img/mdl2/clase1/ejemplo_recorrido1.png)

2)No es posible. Cada ciudad debería conectar con al menos con otras 2 ciudades.


__Definiciones:__
- Recorrido: Es un camino que tiene todos los vértices.
- Camino simple: Camino que no repite vértices.

---

__Problema de los saludos en una reunión__

En una reunión hay n invitados, se saludan todos con un apretón de manos ¿Cuántos apretones de mano hay?

(n(n-1))/2 = Número de saludos = Número de aristas de Cn

![image]({{site.url}}/img/mdl2/clase1/ejemplo_grafoCompleto.png)

n = 4

__Definición:__
- Grafo completo de n vértices: Es el grafo que tiene todas las aristas Cn.

---

__Ejercicios del práctico:__
Por terminar.
