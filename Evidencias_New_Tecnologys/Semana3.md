<!-- No borrar o modificar -->
[Inicio](./index.md)


# Actividad 3: Ejercicios de operaciones básicas en Java.

<br>

1. Suma y multiplicación: Escribe un programa que solicite al usuario dos números enteros y luego imprima la suma y multiplicación de esos números.

2. Resta y división: Escribe un programa que tome dos números enteros ingresados por el usuario y calcule la resta y división de esos números.

3. Operaciones combinadas: Escribe un programa que solicite al usuario tres números enteros y realice las siguientes operaciones: suma de los tres números, multiplicación del primer número por el segundo y división del resultado entre el tercer número.

4. Operaciones con decimales: Escribe un programa que solicite al usuario dos números decimales y realice las siguientes operaciones: suma, resta, multiplicación y división.

5. Incremento y decremento: Escribe un programa que declare una variable entera y la inicialice con un valor. Luego, incrementa su valor en 1 y muestra el resultado. Después, decrementa su valor en 1 y muestra el resultado nuevamente.

6. Operador de asignación compuesta: Escribe un programa que declare una variable entera y la inicialice con un valor. Utiliza el operador de asignación compuesta para sumar 5 a la variable y luego mostrar su valor.

7. Operadores lógicos: Escribe un programa que tome dos valores booleanos ingresados por el usuario y muestre el resultado de las operaciones lógicas AND, OR y NOT entre esos valores.

8. Operador ternario: Escribe un programa que tome un número entero ingresado por el usuario y utilice el operador ternario para determinar si el número es positivo o negativo. Luego, muestra el resultado en la salida.

9.

10.

## Solución

```

 1

import java.util.Scanner;
public class PromedioTresNumeros {
public static void main(String[] args) {
Scanner scanner = new Scanner(System.in);
System.out.print("Ingrese el primer número: ");
double numero1 = scanner.nextDouble();
System.out.print("Ingrese el segundo número: ");
double numero2 = scanner.nextDouble();
double suma = (numero1 + numero2 );
System.out.println("La suma de los dos números es: " );
scanner.close();
}
}

```

```

 2

import java.util.Scanner;
public class RestaDivisionCalculator {
public static void main(String[] args) {
Scanner scanner = new Scanner(System.in);
System.out.print("Ingresa el primer número: ");
int numero1 = scanner.nextInt();
System.out.print("Ingresa el segundo número: ");
int numero2 = scanner.nextInt();
// Calculando la resta
int resta = numero1 - numero2;
System.out.println("La resta de " + numero1 + " y " + numero2 + " es: " + resta);
// Verificando la división por cero
if (numero2 != 0) {
// Calculando la división
double division = (double) numero1 / numero2;
System.out.println("La división de " + numero1 + " entre " + numero2 + " es: " + division);
} else {
System.out.println("No se puede dividir por cero.");
}
scanner.close();
}
}

```

```
3

import java.util.Scanner;
public class OperacionesCombinadas {
public static void main(String[] args) {
Scanner scanner = new Scanner(System.in)
System.out.println("Ingrese el primer número entero:");
int numero1 = scanner.nextInt();
System.out.println("Ingrese el segundo número entero:");
int numero2 = scanner.nextInt();
System.out.println("Ingrese el tercer número entero:");
int numero3 = scanner.nextInt();
// Realizar las operaciones
int suma = numero1 + numero2 + numero3;
int multiplicacion = numero1 * numero2;
double division = (double) multiplicacion / numero3;
// Mostrar resultados
System.out.println("La suma de los tres números es: " + suma);
System.out.println("La multiplicación del primer número por el segundo es: " + multiplicacion);
System.out.println("La división del resultado entre el tercer número es: " + division);
scanner.close();
}
}


```

```
4

import java.util.Scanner;
public class CalculadoraDecimales {
public static void main(String[] args) {

Scanner scanner = new Scanner(System.in);
System.out.print("Ingrese el primer número decimal: ");
double numero1 = scanner.nextDouble();
System.out.print("Ingrese el segundo número decimal: ");
double numero2 = scanner.nextDouble();
// Realizar operaciones
double suma = numero1 + numero2;
double resta = numero1 - numero2;
double multiplicacion = numero1 * numero2;
if (numero2 != 0) {
double division = numero1 / numero2;
System.out.println("División: " + division);
} else {
System.out.println("No se puede dividir entre cero.");
}
// Imprimir resultados
System.out.println("Suma: " + suma);
System.out.println("Resta: " + resta);
System.out.println("Multiplicación: " + multiplicacion);
scanner.close();
}
}

```

```
5

public class IncrementDecrementExample {
public static void main(String[] args) {
// Declarar una variable entera e inicializarla con un valor
int numero = 5;
// Incrementar el valor en 1 y mostrar el resultado
numero++;

System.out.println("Después de incrementar: " + numero);
// Decrementar el valor en 1 y mostrar el resultado nuevamente
numero--;
System.out.println("Después de decrementar: " + numero);
}
}

```

```

6

public class SumaCompuesta {
public static void main(String[] args) {
// Declarar y inicializar la variable entera
int numero = 10; // Puedes cambiar este valor según lo que desees

// Utilizar el operador de asignación compuesta para sumar 5 a la variable
numero += 5;

// Mostrar el valor de la variable después de la suma
System.out.println("El valor de la variable después de sumar 5 es: " + numero);
}
}

```

```
7

import java.util.Scanner;
public class OperacionesLogicas {
public static void main(String[] args) {
Scanner scanner = new Scanner(System.in)
System.out.print("Ingresa el primer valor booleano (true/false): ");
boolean valor1 = scanner.nextBoolean();

System.out.print("Ingresa el segundo valor booleano (true/false): ");

boolean valor2 = scanner.nextBoolean();
// Operación lógica AND
boolean resultadoAND = valor1 && valor2;
System.out.println("Resultado de la operación AND: " + resultadoAND);
// Operación lógica OR
boolean resultadoOR = valor1 || valor2;
System.out.println("Resultado de la operación OR: " + resultadoOR);
// Operación lógica NOT para el primer valor
boolean resultadoNOT1 = !valor1;
System.out.println("Resultado de la operación NOT para el primer valor: " +
resultadoNOT1);
// Operación lógica NOT para el segundo valor
boolean resultadoNOT2 = !valor2;
System.out.println("Resultado de la operación NOT para el segundo valor: " +
resultadoNOT2);
}

```

```
8

import java.util.Scanner;
public class PosNegTernary {
public static void main(String[] args) {
Scanner scanner = new Scanner(System.in);
System.out.print("Ingresa un número entero: ");
int numero = scanner.nextInt();
String resultado = (numero >= 0) ? "positivo" : "negativo";
System.out.println("El número ingresado es " + resultado);
scanner.close();
}
}

```
