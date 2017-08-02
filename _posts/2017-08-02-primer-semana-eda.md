---
layout: post
title: Primera semana de EDA
---

Luego de presentarse el profesor, Nicolás Artigas, pasamos directamente a un repaso de las distintas opciones que nos ofrece el lenguaje de programación C.
A lo largo de esta y de futuras entradas del blog se asumirá en la mayoría de los casos que se sabe que hace cada función, por lo tanto no voy a explicar a menos que crea necesario hacerlo.

El IDE que se utilizará en clase es Codeblocks, aunque por comodidad, yo prefiero usar el editor [Atom](https://atom.io) y compilar directamente desde la consola de linux.

Como el profesor explicó, el lenguaje utilizado en el curso es C, sin embargo el compilador será el de C++, esto es así ya que dicho compilador nos será de gran utilidad para el momento empezar a modularizar (entre otras cosas), nuestros programas.

Para compilar desde la shell se utiliza la siguiente sintaxis:

    g++ -o <nombre del ejecutable> <archivo1>.cpp <archivo2>.cpp ... <archivoN>.cpp

---

Todo lo que tenga un numeral (#) no se compila, pasa directamente al pre-procesador.

    #include <stdio.h>
    int main(){
        scanf("%d",&num); //El primer parámetro es el tipo de dato, y el segundo es la referencia (marcada por el "&") a la dirección de la variable num, donde se guardará el valor que ingrese el usuario desde teclado.
        printf("%d",num); //De la misma forma el primer parámetro es el tipo de dato, y el segundo en este caso es el valor de la variable num.
        return 0;
    }

---

__**Estructuras de Control**__

Selección:
- if
- else
- switch
Repetición
- for
- while
- dowhile
Secuencia
- operaciones
- entradas/salidas

---

A continuación dejo el link a los ejercicios (La letra de los mismos están comentadas al principio de cada ejercicio en el archivo principal del ejercicio.) que realizamos en clases, con el código y el ejecutable del mismo.

+ [Ejercicio 1](https://github.com/Ctrl4/Estructura-de-Datos-y-Algoritmos/tree/master/Semana%2001/Ejercicio01)
+ [Ejercicio 2](https://github.com/Ctrl4/Estructura-de-Datos-y-Algoritmos/tree/master/Semana%2001/Ejercicio02)
+ [Ejercicio 3](https://github.com/Ctrl4/Estructura-de-Datos-y-Algoritmos/tree/master/Semana%2001/Ejercicio03)
+ [Ejercicio 4](https://github.com/Ctrl4/Estructura-de-Datos-y-Algoritmos/tree/master/Semana%2001/Ejercicio04)
+ [Ejercicio 5](https://github.com/Ctrl4/Estructura-de-Datos-y-Algoritmos/tree/master/Semana%2001/Ejercicio05)
+ [Ejercicio 6](https://github.com/Ctrl4/Estructura-de-Datos-y-Algoritmos/tree/master/Semana%2001/Ejercicio06) (Incompleto)

---


Por lo pronto esto es todo por esta semana en lo que respecta a EDA, intentaré subir los apuntes de EDA los miércoles.
Los miércoles tengo Matemática Discreta 2, la cual creo que me llevará más tiempo de estudio ya que hace tiempo que no la estudio (a diferencia que programar por más que sea en otro lenguaje uno lo hace más a menudo). Intentaré subir los apuntes de discreta 2 al día siguiente de la clase.
Y los jueves y viernes tengo Bases de Datos, e intentaré subir estos apuntes los sábados.

¡Saludos!
