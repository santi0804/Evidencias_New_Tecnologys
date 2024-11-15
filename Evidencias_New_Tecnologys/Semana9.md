<!-- No borrar o modificar -->
[Inicio](./index.md)

## Sesión 9 


# Calculadora de la mediana


La mediana es un valor estadístico que se utiliza para describir el centro de un conjunto de datos. Es el valor que se encuentra justo en el medio de un conjunto de datos ordenados de menor a mayor. Es decir, la mediana divide el conjunto de datos en dos partes iguales, donde la mitad de los valores están por encima de la mediana y la otra mitad están por debajo de ella.

<br>
<br>

### Calculemos con números pares e impares.
<br>


```

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package com.mycompany.calculadoramedianasesion9act;

import java.util.Arrays;

/**
 *
 * @author admin
 */
public class CalculadoraMedianasesion9act {

  public static double calcularMediana(int[] numeros) {
        Arrays.sort(numeros);
        int n = numeros.length;

        if (n % 2 != 0) {
            return numeros[n / 2];
        } else {
            int medio1 = numeros[n / 2 - 1];
            int medio2 = numeros[n / 2];
            return (medio1 + medio2) / 2.0;
        }
    }

    public static void main(String[] args) {
        int[] conjuntoImpar = {1, 3, 5, 7, 9, 13, 17, 21, 27,};
        int[] conjuntoPar = {2, 4, 6, 8, 10, 12 , 14, 16, 18, 20};

        double medianaImpar = calcularMediana(conjuntoImpar);
        double medianaPar = calcularMediana(conjuntoPar);

        System.out.println("La mediana del conjunto impar es: " + medianaImpar);
        System.out.println("La mediana del conjunto par es: " + medianaPar);
    }
}

```






