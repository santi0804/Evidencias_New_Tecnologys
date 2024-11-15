
<!-- No borrar o modificar -->
[Inicio](./index.md)

### Sesión 8 


# Actividad: Ejecicios de métodos en Java


1. Escribe un método que reciba dos números como parámetros y devuelva el mayor de los dos.

2. Escribe un método que reciba una cadena de texto como parámetro y devuelva el número de vocales que contiene.

3. Escribe un método que reciba una cadena de texto como parámetro y devuelva una nueva cadena con todas las letras mayúsculas en minúsculas y viceversa.

4. Escribe un método que reciba una cadena de texto como parámetro y devuelva el número de palabras que contiene.

5. Escribe un método que reciba una cadena de texto como parámetro y devuelva una nueva cadena con todas las palabras en orden alfabético.
<br>
<br>


## Solución.


#### 1.

En este método se recibe dos números como parámetros y devuelve el mayor de los dos:


```

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package com.mycompany.sesion8act;

/**
 *
 * @author admin
 */
public class Sesion8act {
    public static void main(String[] args) {
        int numero1 = 50;
        int numero2 = 156;

        int mayor = encontrarMayor(numero1, numero2);

        System.out.println("El número mayor es: " + mayor);
    }

    public static int encontrarMayor(int num1, int num2) {
        if (num1 > num2) {
            return num1;
        } else {
            return num2;
        }
    }
}

```

#### 2.

 Aqui contamos el número de vocales en una cadena de texto


```

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package com.mycompany.sesion8act;

/**
 *
 * @author admin
 */
public class Sesion8act {
    public static void main(String[] args) {
        String texto = "Hola, ¿cómo estás?";

        int cantidadVocales = contarVocales(texto);

        System.out.println("El número de vocales es: " + cantidadVocales);
    }

    public static int contarVocales(String texto) {
        int contador = 0;
        String vocales = "aeiouAEIOU";

        for (int i = 0; i < texto.length(); i++) {
            char caracter = texto.charAt(i);
            if (vocales.indexOf(caracter) != -1) {
                contador++;
            }
        }

        return contador;
    }
}


```

#### 3.

Aqui modificamos las letras mayusculas de las minusculas.
<br>


```

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package com.mycompany.sesion8act;

/**
 *
 * @author admin
 */
public class Sesion8act {
    
    public static void main(String[] args) {
        String texto = "Por aqui, APRENDIENDO con mucho esfuerzo?";

        String textoModificado = cambiarMayusculasMinisculas(texto);

        System.out.println("Texto modificado: " + textoModificado);
    }

    public static String cambiarMayusculasMinisculas(String texto) {
        StringBuilder resultado = new StringBuilder();

        for (int i = 0; i < texto.length(); i++) {
            char caracter = texto.charAt(i);

            if (Character.isUpperCase(caracter)) {
                resultado.append(Character.toLowerCase(caracter));
            } else if (Character.isLowerCase(caracter)) {
                resultado.append(Character.toUpperCase(caracter));
            } else {
                resultado.append(caracter);
            }
        }

        return resultado.toString();
    }
}


```

#### 4.

Con este codigo podemos contar las palabras del texto ingresado al inicio de la cadena de texto.


```

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package com.mycompany.sesion8act;

/**
 *
 * @author admin
 */
public class Sesion8act {
    
    public static void main(String[] args) {
        String texto = "Por aqui contando las palabras, probando probando";

        int cantidadPalabras = contarPalabras(texto);

        System.out.println("El número de palabras es: " + cantidadPalabras);
    }

    public static int contarPalabras(String texto) {
        String[] palabras = texto.split("\\s+");
        return palabras.length;
    }
}


```


#### 5.
<br>

Con este codigo podremos ordenar las palabras que sean ingrezadas en desoden.


```

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */
package com.mycompany.sesion8act;

import java.util.Arrays;

/**
 *
 * @author admin
 */
public class Sesion8act {

    public static void main(String[] args) {
        String texto = " y que mas tienen por decir- Haber quien jode, en este codigo,";

        String textoOrdenado = ordenarPalabras(texto);

        System.out.println("Texto ordenado: " + textoOrdenado);
    }

    public static String ordenarPalabras(String texto) {
        String[] palabras = texto.split("\\s+");

        // Ordenar el arreglo de palabras
        Arrays.sort(palabras);

        // Unir las palabras ordenadas en una sola cadena
        StringBuilder resultado = new StringBuilder();
        for (String palabra : palabras) {
            resultado.append(palabra).append(" ");
        }

        return resultado.toString().trim();
    }
}

```




