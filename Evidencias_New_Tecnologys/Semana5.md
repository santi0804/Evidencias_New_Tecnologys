<!-- No borrar o modificar -->
[Inicio](./index.md)


# Actividad 5: Ejercicios de bucles

<br>

Resolver los siguientes ejercicios:

<br>

## Ejercicios - while

- Pedir al usuario que ingrese un número y mostrar su tabla de multiplicar hasta el número 10.

- Pedir al usuario que ingrese una cadena de caracteres y contar la cantidad de caracteres que son números.

## Ejercicios - do while

- Escribe un programa en Java que imprima los números del 1 al 100, pero que se detenga si el usuario introduce un número negativo.

- Escribe un programa en Java que pida al usuario un número entero e imprima la tabla de multiplicar de ese número, pero que se detenga si el usuario introduce el número 0.

## Ejercicios - for

- Imprimir los números impares del 1 al 50.
- Imprimir los números primos del 1 al 100.

<br>
<br>

SOLUCION.

while

```

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Project/Maven2/JavaApp/src/main/java/${packagePath}/${mainClassName}.java to edit this template
 */

package com.mycompany.sesion8;

import java.util.Scanner;

/**
 *
 * @author CESDE
 */
public class SESION8 {


      public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Ingresa un número: ");
        int numero = scanner.nextInt();

        System.out.println("Tabla de multiplicar del " + numero + ":");

        for (int i = 1; i <= 10; i++) {
            System.out.println(numero + " x " + i + " = " + (numero * i));
        }

        scanner.close();
    }
}

```

```
/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Project/Maven2/JavaApp/src/main/java/${packagePath}/${mainClassName}.java to edit this template
 */

package com.mycompany.sesion8;

import java.util.Scanner;

/**
 *
 * @author CESDE
 */
public class SESION8 {


     public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Ingresa una cadena de caracteres: ");
        String cadena = scanner.nextLine();

        int contador = 0;
        int i = 0;

        while (i < cadena.length()) {
            char caracter = cadena.charAt(i);

            if (Character.isDigit(caracter)) {
                contador++;
            }

            i++;
        }

        System.out.println("La cantidad de caracteres que son números es: " + contador);
    }
}

```

do while

```

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int numero = 0;

        do {
            System.out.print("Introduce un número (o un número negativo para salir): ");
            numero = scanner.nextInt();

            if (numero >= 1 && numero <= 100) {
                System.out.println("Número válido: " + numero);
            } else if (numero < 0) {
                System.out.println("Programa terminado.");
            } else {
                System.out.println("El número debe estar entre 1 y 100.");
            }
        } while (numero >= 1 && numero <= 100);

        scanner.close();
    }
}

```

```
public class TablaMultiplicar {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int numero;

        do {
            System.out.print("Introduce un número entero (0 para salir): ");
            numero = scanner.nextInt();

            if (numero != 0) {
                System.out.println("Tabla de multiplicar de " + numero + ":");
                for (int i = 1; i <= 10; i++) {
                    System.out.println(numero + " x " + i + " = " + (numero * i));
                }
            }
        } while (numero != 0);

        System.out.println("¡Hasta luego!");
    }
}

```

For

```
/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Project/Maven2/JavaApp/src/main/java/${packagePath}/${mainClassName}.java to edit this template
 */

package com.mycompany.sesion8;

import java.util.Scanner;

/**
 *
 * @author CESDE
 */
public class SESION8 {



    public class NumerosImpares {

    }
    public static void main(String[] args) {
        for (int i = 1; i <= 50; i++) {
            if (i % 2 != 0) {
                System.out.println(i);
            }
        }
    }

}

```

```
*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Project/Maven2/JavaApp/src/main/java/${packagePath}/${mainClassName}.java to edit this template
 */
package com.mycompany.sesion8;

import java.util.Scanner;

/**
 *
 * @author CESDE
 */
public class SESION8 {

    public class NumerosImpares {

    }

    public class NumerosPrimos {

        public static void main(String[] args) {
            for (int i = 2; i <= 100; i++) {
                if (esPrimo(i)) {
                    System.out.println(i);
                }
            }
        }

        public static boolean esPrimo(int num) {
            if (num < 2) {
                return false;
            }
            for (int i = 2; i <= Math.sqrt(num); i++) {
                if (num % i == 0) {

                }
            }
            return false;

        }

    }
}


```
