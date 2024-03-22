# Estructuras de datos (primer examen)

## Introducción

Para este examen usted requerirá de alguna documentación y de algo de código
fuente que estará disponible como parte del repositorio donde se encuentra este
archivo.

Este trabajo está diseñado para ser realizado en parejas. Es decir, grupos de
máximo dos estudiantes. Al respecto es necesario aclarar que en cualquier caso
se puede requerir una sustentación. En esas circunstancias la nota del trabajo
será la nota de la sustentación. Por tratarse de un trabajo en grupos ambos
integrantes deben estar en total capacidad de llevar a cabo la sustentación e
igual la nota será grupal.

## Ensamblador para RISCV

El trabajo consiste en la implementación de un ensamblador para el conjunto de
instrucciones de RISCV32IM. Un ensamblador es un programa que traduce código
fuente como el siguiente:

```assembly
main:
    addi x4, zero, 50
    addi x5, zero, 50
    beq x4, x5, label1
    addi x6, zero, 80
    beq zero, zero, label2
    

label1:
    addi x6, zero, 100

label2:
    add zero, zero, zero
```

en un archivo con el siguiente código:

```
03 20 02 13 03 20 02 93 00 52 06 63 05 00 03 13 
00 00 04 63 06 40 03 13 00 00 00 33 00 00 00 00 
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
```

Es de anotar que la salida no es exactamente esa, fue recortada para que no
ocupara tanto espacio en el documento.

Al programa de arriba lo llamaremos el programa de entrada y al de abajo lo
llamaremos el programa de salida para los efectos de ésta tarea. Entonces
básicamente lo que usted debe presentar es un programa que tome como entrada un
archivo conteniendo código de ensamblador como el de arriba y escriba como
salida un archivo con código como el de abajo.

Lo único que queda entonces es establecer es cómo cada línea del programa de
arriba debe quedar representada en el archivo de salida. Para que el desarrollo
de este ensamblador no luzca en exceso complicado, será descrito por medio de
ejercicios. Estos irán incorporando cambios sobre su programa de manera
incremental hasta terminar en un ensamblador completo.

## Ejercicio 1

En esta primera parte usted va a realizar un programa en C/C++ que lea un
archivo de entrada y escriba en un archivo de salida de la siguiente forma:

Cada línea no vacía de la entrada puede ser de una de las siguientes entidades:

- _Etiquetas_:  marcan el inicio de una sección dentro del programa.  
- _Instrucciones_: son las que finalmente serán traducidas.
- _Directivas_:  son opciones que no pertenecen al lenguaje de programación
   pero que afectan la forma como quedará el archivo de salida.
- _Comentarios_: son anotaciones de código que no tienen relevancia durante
   la ejecución.

1. Los comentarios deben ser ignorados y no deben ir en el archivo de salida.
2. Las directivas también serán ignoradas por ahora.
3. Por cada instrucción debe aparecer en el archivo de salid una línea de 32
   bits (binario) con solamente ceros. Exceptuando la parte del código de operación, el cual si debe coincidir con los códigos presentados en


## Recursos

En el repositorio encontrará los siguientes archivos:

- __rvalp.pdf__: Es un documento donde encontrará información detallada de cómo
  son escritas las instrucciones en el ensamblador. En particular le recomiendo
  echar un vistazo al capítulo 5. La sección 5.3 es muy importante porque allí
  encuentra el formato en el que cada instrucción debe quedar en la salida.
- __RISCV_CARD.pdf__: Es el documento que contiene todo el conjunto de
  instrucciones. En especial le recomiendo ver la primera página.