<!-- No borrar o modificar -->
[Inicio](./index.md)


## Sesión 7 

# Actividad: Ejecicios Array - ArrayList

<br>

## 1. En parejas, probar, analizar y explicar el funcionamiento de los siguientes ejemplos de Array y ArrayList.

<br>

#### Ejemplo Array


```

import java.util.Arrays;

public class EjercicioArray {

    public static void main(String[] args) {
        // Crear un array de números enteros
        int[] numeros = {5, 2, 10, 7, 1};

        // Imprimir el array original
        System.out.println("Array original: " + Arrays.toString(numeros));

        // Calcular la suma de los elementos del array
        int suma = 0;
        for (int i = 0; i < numeros.length; i++) {
            suma += numeros[i];
        }
        System.out.println("La suma de los elementos es: " + suma);

        // Encontrar el número más grande en el array
        int maximo = numeros[0];
        for (int i = 1; i < numeros.length; i++) {
            if (numeros[i] > maximo) {
                maximo = numeros[i];
            }
        }
        System.out.println("El número más grande es: " + maximo);

        // Ordenar el array en orden ascendente
        Arrays.sort(numeros);
        System.out.println("Array ordenado: " + Arrays.toString(numeros));
    }
}

```

#### Ejemplo Array list

```

import java.util.ArrayList; 
import java.util.Scanner;

public class AppNotas {

  public static void main(String[] args) {

    ArrayList<String> notas = new ArrayList<>();
    
    Scanner scan = new Scanner(System.in);

    while(true) {

      System.out.println("1. Agregar nota");  
      System.out.println("2. Mostrar notas");
      System.out.println("3. Salir");

      int opcion = scan.nextInt();

      if (opcion == 1) {
        agregarNota(notas, scan);  
      } else if (opcion == 2) {
        mostrarNotas(notas);
      } else {
        break;
      }

    }

  }

  public static void agregarNota(ArrayList<String> notas, Scanner scan) {
    
    System.out.println("Ingrese el titulo de la nota:");
    String titulo = scan.nextLine();
    
    System.out.println("Ingrese el contenido de la nota:");
    String contenido = scan.nextLine();
    
    notas.add(titulo + " - " + contenido);

  }

  public static void mostrarNotas(ArrayList<String> notas) {

    for(String n : notas) {
      System.out.println(n);
    }

  }

}

```


## Crear un ejemplo de Array y otro de ArrayList para visualizar sus diferencias.


#### Solución

Aqui buscaremos el valor minimo y el valor maximo, aplicando las técnicas que nos enseña el profe.
<br>


```

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */
package com.mycompany.sesion7act;

/**
 *
 * @author admin
 */
public class Sesion7act {

    public static void main(String[] args) {
        int[] numeros = {5, 12, 3, 8, 1, 6, 9, 2, 7, 10};

        int min = encontrarMinimo(numeros);
        int max = encontrarMaximo(numeros);

        System.out.println("El valor mínimo es: " + min);
        System.out.println("El valor máximo es: " + max);
    }

    public static int encontrarMinimo(int[] array) {
        int min = array[0]; // Suponemos que el primer elemento es el mínimo

        for (int i = 1; i < array.length; i++) {
            if (array[i] < min) {
                min = array[i];
            }
        }

        return min;
    }

    public static int encontrarMaximo(int[] array) {
        int max = array[0]; // Suponemos que el primer elemento es el máximo

        for (int i = 1; i < array.length; i++) {
            if (array[i] > max) {
                max = array[i];
            }
        }

        return max;
    }
}

```

<br>

Este ejercicio consiste en crear una lista de nombres y luego imprimirlos en orden inverso.


```

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */
package com.mycompany.sesion7act;

/**
 *
 * @author admin
 */
public class Sesion7act {

    public static void main(String[] args) {
        // Crear un ArrayList de Strings
        ArrayList<String> nombres = new 
         ArrayList<String>();

        // Agregar nombres a la lista
        nombres.add("Juan");
        nombres.add("María");
        nombres.add("Pedro");
        nombres.add("Laura");

        // Imprimir la lista en orden original
        System.out.println("Lista original:");
        for (String nombre : nombres) {
            System.out.println(nombre);
        }

        // Invertir la lista
        invertirArrayList(nombres);

        // Imprimir la lista invertida
        System.out.println("\nLista 
         invertida:");
        for (String nombre : nombres) {
            System.out.println(nombre);
        }
    }

    public static void invertirArrayList(ArrayList<String> lista) {
        int i = 0;
        int j = lista.size() - 1;

        while (i < j) {
            String temp = lista.get(i);
            lista.set(i, lista.get(j));
            lista.set(j, temp);

            i++;
            j--;
        }
    }
}


```









