<!-- No borrar o modificar -->

[Inicio](./index.md)

## Sesión 10

# Actividad: Prueba, ejecución y explicación de ejercicios de lógica de programación.

- Selecciona dos ejercicios de la sesión 10, impleméntalos, ejecútalos y proporciona una explicación detallada de cada uno
  <br>

### Solucion

Ejercicio # 1: Calcular el movimiento rectilíneo uniforme.

- El movimiento rectilíneo uniforme (MRU) es un tipo de movimiento en el cual un objeto se mueve en línea recta y a velocidad constante, es decir, su velocidad no cambia en el tiempo. En este tipo de movimiento, la trayectoria del objeto es una línea recta, por lo que su aceleración es cero.

```

import java.util.Scanner;

public class MRU {
   public static void main(String[] args) {
      Scanner input = new Scanner(System.in);
      double velocidad, tiempo, distancia;

      // Solicita la velocidad y el tiempo
      System.out.print("Ingrese la velocidad en metros por segundo: ");
      velocidad = input.nextDouble();
      System.out.print("Ingrese el tiempo en segundos: ");
      tiempo = input.nextDouble();

      // Calcula la distancia recorrida
      distancia = velocidad * tiempo;

      // Muestra el resultado en la consola
      System.out.printf("La distancia recorrida es de %.2f metros.", distancia);
   }
}

```

- En este ejercicio nos calcula la velocidad en metros.

<br>

Ejercicio # 2: Calcular el movimiento parabólico de un proyectil.

El movimiento parabólico de un proyectil es un tipo de movimiento en el cual un objeto es lanzado con una velocidad inicial y se mueve siguiendo una trayectoria curva en forma de parábola debido a la influencia de la gravedad. Este tipo de movimiento se caracteriza por tener tanto una componente horizontal como una vertical.

Durante el movimiento parabólico de un proyectil, la fuerza de la gravedad actúa sobre el objeto, lo que hace que la trayectoria del proyectil describa una curva en forma de parábola. La velocidad horizontal del proyectil se mantiene constante a lo largo de todo el recorrido, mientras que la velocidad vertical va disminuyendo debido a la fuerza de la gravedad.

<br>

```
import java.util.Scanner;

public class MovimientoParabolico {
   public static void main(String[] args) {
      Scanner input = new Scanner(System.in);
      double velocidadInicial, angulo, alturaInicial, tiempo;
      final double gravedad = 9.81;

      // Solicita la velocidad inicial, el ángulo y la altura inicial
      System.out.print("Ingrese la velocidad inicial en metros por segundo: ");
      velocidadInicial = input.nextDouble();
      System.out.print("Ingrese el ángulo de lanzamiento en grados: ");
      angulo = input.nextDouble();
      System.out.print("Ingrese la altura inicial en metros: ");
      alturaInicial = input.nextDouble();

      // Calcula la velocidad en los ejes x e y
      double velocidadX = velocidadInicial * Math.cos(Math.toRadians(angulo));
      double velocidadY = velocidadInicial * Math.sin(Math.toRadians(angulo));

      // Calcula el tiempo de vuelo
      tiempo = (2 * velocidadY) / gravedad;

      // Calcula la distancia recorrida
      double distancia = velocidadX * tiempo;

      // Calcula la altura máxima alcanzada
      double alturaMaxima = alturaInicial + (velocidadY * velocidadY) / (2 * gravedad);

      // Muestra los resultados en la consola
      System.out.printf("La distancia recorrida es de %.2f metros.", distancia);
      System.out.printf("La altura máxima alcanzada es de %.2f metros.", alturaMaxima);
      System.out.printf("El tiempo de vuelo es de %.2f segundos.", tiempo);
   }
}


```
