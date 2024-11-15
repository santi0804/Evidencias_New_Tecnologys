<!-- No borrar o modificar -->
[Inicio](./index.md)


# Actividad 4: Ejercicios de control de flujo con expresiones compuestas

<br>

Con la información anterior, implementa los siguientes ejercicios:

1. eterminar si el estudiante es mayor de edad y tiene un estado activo.

2. Determinar si el estudiante tiene una beca o una carrera relacionada con el desarrollo de software.

3. Determinar si el estudiante está en el último semestre de su carrera y tiene un estado activo.

4. Determinar si el estudiante tiene una carrera relacionada con el desarrollo de software y un promedio superior a 4.0.

5. Mostrar toda la información del estudiante si está matriculado en el Cesde.

6. Asignar una beca del 50% si el estudiante está matriculado en el Cesde,
   tiene un promedio superior a 4.0 y está activo.

7. Determinar la cantidad de beca que recibe el estudiante según su promedio:

- 0.0 - 3.4: El estudiante no recibe beca.

- 3.5 - 3.9: El estudiante recibe una beca parcial del 25%.

- 4.0 - 4.4: El estudiante recibe una beca parcial del 50%.

- 4.5 - 5.0: El estudiante recibe una beca completa.

## Soluciones.

<br>

```

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Project/Maven2/JavaApp/src/main/java/${packagePath}/${mainClassName}.java to edit this template
 */
package com.mycompany.actividadseccion4;

import java.util.Scanner;

/**
 *
 * @author CESDE
 */
public class ACTIVIDADSECCION4 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Variables de tipo String
        String nombre = "Santiago";
        String apellido = "Tamayo";
        String identificación = "1035419520";
        String correo = "stamayoper@cesde.net";
        String carrera = "Desarrollo de Software";
        String universidad = "Cesde";
        // Variable de tipo int
        int edad = 35;
        boolean esActivo = true;
        boolean becado = false;
        char genero = 'M';
        double promedio = 4.5;
        int semestre = 2;
        //Determinar si el estudiante es mayor de edad y tiene un estado activo.
        System.out.println("-----------------------------------------------");
        System.out.println("EJERCICIO 1");

        if (edad >= 18 && esActivo);

        System.out.println("Es mayor de edad y esta activo");

        //Determinar si el estudiante tiene una beca o una carrera relacionada con el desarrollo de software.
        System.out.println("-----------------------------------------------");
        System.out.println("EJERCICIO 2");

        if (becado || carrera == "Desarrollo de Software");

        System.out.println(" cumple con alguna de las dos condiciones");


        //Determinar si el estudiante está en el último semestre de su carrera y tiene un estado activo.
        System.out.println("-----------------------------------------------");
        System.out.println("EJERCICIO 3");

        if (semestre >= 3 && esActivo) {

            System.out.println(" cumple con alguna de las dos condiciones");

        } else {
            System.out.println("no cumples con una de las condicicones");
        }

        //Determinar si el estudiante tiene una carrera relacionada con el desarrollo de software y un promedio superior a 4.0.
        System.out.println("-----------------------------------------------");
        System.out.println("EJERCICIO 4");

        if (carrera.equals("Desarrollo de Software") && promedio >= 4.0)
        {
            System.out.println(" cumples con las 2 condiciones");
        }

        //Mostrar toda la información del estudiante si está matriculado en el Cesde.
        System.out.println("-----------------------------------------------");
        System.out.println("EJERCICIO5 5");

        if (esActivo == true) {

            System.out.println("Nombre: " + nombre + " " + apellido);
            System.out.println("Identificacion: " + identificación);
            System.out.println("Correo: " + correo);
            System.out.println("Universidad: " + universidad);

        }

            //Asignar una beca del 50% si el estudiante está matriculado en el Cesde, tiene un promedio superior a 4.0 y está activo.
            System.out.println("-----------------------------------------------");
            System.out.println("EJERCICIO5 6");

            if (universidad.equals ("cesde") && promedio >4.0 && esActivo) {
                becado = true;
                System.out.println("Se le asigna beca del 50% al estudiante");
            }

            //Determinar la cantidad de beca que recibe el estudiante según su promedio
            System.out.println("-----------------------------------------------");
            System.out.println("EJERCICIO5 7");

            if (promedio >= 0.0  && promedio <= 3.4) {
                System.out.println("El estudiante no recibe beca");
            }
            else if (promedio >= 3.5  && promedio <= 3.9){
                System.out.println("El estudiante no recibe beca parcial del 25%");
            }
            else if (promedio >= 4.0  && promedio <= 4.4){
                System.out.println("El estudiante recibe una beca parcial del 50%.");
            }
            else if (promedio >= 4.5  && promedio <= 5.0){
                System.out.println("El estudiante recibe una beca completa.");
            }

            //Determinar genero del estudiante por letra
            System.out.println("-----------------------------------------------");
            System.out.println("EJERCICIO5 8");


            if  (genero == 'M'){
                System.out.println("El estudiante es hombre");
            } else {
                 System.out.println("El estudiante no es hombre");
            }

            //Determinar genero del estudiante por letra
            System.out.println("-----------------------------------------------");
            System.out.println("EJERCICIO5 9");

            //Si es nuevo el estudiante  tiene tiene 2 semestres, de 2 a 5 el estudiante ya esta adaptado// y de 6 a 9 ya es un un antiaguo


            switch (semestre){
                case 1:
                   System.out.println("El estudiante es nuevo");
                   break;
                case 2:
                case 3:
                case 4:
                case 5:
                   System.out.println("El estudiante esta adaptado");
                   break;
                case 6:
                case 7:
                case 8:
                case 9:
                   System.out.println("El estudiante es antiguo");
                   break;
                case 10:
                   System.out.println("Estudiante graduado");
                   break;
                default:
                   System.out.println("Semestre incorrecto");
                   break;
            }

            if (semestre  != 10){
                System.out.println("No realiza trabajos adicionales");
            }
   }
 }

```
