# Simulador de Ensamblador RISC-V-32I Entrega Final

## Descripción General

Este proyecto simula un ensamblador RISC-V-32I, traduciendo lenguaje ensamblador a código máquina. Soporta una variedad de tipos de instrucciones incluyendo R, I, S, B, U y J, además de instrucciones de sistema y pseudo-instrucciones como NOP. El simulador lee un archivo de código ensamblador, procesa las instrucciones y produce el correspondiente código máquina binario.

## Detalles de Implementación

### Estructuras de Datos
- **Vectores** (`vector<string>`): Utilizados extensamente para almacenar secuencias de cadenas y gestionar dinámicamente datos relacionados con las instrucciones de ensamblaje y sus componentes.
- **Mapas** (`map<string, int>`): Empleados para mantener un mapeo entre los nombres de las etiquetas y sus direcciones correspondientes en el conjunto de instrucciones, facilitando las instrucciones de salto y bifurcación.
- **Conjuntos de bits** (`bitset<5>`, `bitset<12>`, `bitset<20>`, `bitset<21>`): Utilizados para codificar índices de registros y valores inmediatos en formatos binarios de tamaño fijo.

### Funciones Clave

#### Manejo de Espacios y Comentarios
- `ltrim`, `rtrim` y `trim`: Funciones para eliminar espacios innecesarios de las cadenas, asegurando un procesamiento limpio del código ensamblador.
- `hasComment` y `removeComment`: Funciones para detectar y eliminar comentarios de las líneas de código ensamblador, asegurando que solo se procesen instrucciones ejecutables.

#### Funciones de Codificación
- `encodeRegister`, `encodeRs1`, `encodeConstNumber`, `encodeConstNumberTypeU`: Estas funciones convierten componentes de la sintaxis de ensamblaje (como nombres de registros y valores inmediatos) en sus respectivas representaciones binarias.

#### Procesamiento de Instrucciones
- `extractInst`: Identifica y aísla diferentes tipos de instrucciones de una línea de código ensamblador dada.
- `processTypeR`, `processTypeI`, `processTypeS`, `processTypeB`, `processTypeU`, `processTypeJ`: Cada una de estas funciones maneja los detalles específicos de codificación para diferentes tipos de instrucciones, construyendo el código máquina completo de 32 bits basado en las especificaciones de la instrucción.

### Flujo Lógico

1. **Lectura de Entrada**: El código ensamblador se lee de un archivo de entrada, línea por línea. Cada línea se verifica en busca de etiquetas que se almacenan en el `labelAddressMap`.
2. **Procesamiento de Instrucciones**: Cada línea de instrucción se procesa según su tipo. El opcode, los registros, los valores inmediatos y las etiquetas (para instrucciones de salto y bifurcación) se codifican en formato binario.
3. **Generación de Salida**: Las instrucciones codificadas binariamente se escriben en un archivo de salida, representando el equivalente en código máquina del archivo de entrada ensamblador.

### Uso

Compile y ejecute el programa principal con su archivo `.asm` en el mismo directorio, y especifique el nombre del archivo de entrada. La salida se generará en un archivo de salida especificado.

