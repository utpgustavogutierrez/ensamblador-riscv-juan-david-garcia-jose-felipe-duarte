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

### Ejemplo de Uso

A continuación se presenta un ejemplo del archivo `input.asm` utilizado para probar todas las funciones del simulador:

```asm
# Instrucciones tipo R
add x1, x2, x3
sub x4, x5, x6
sll x7, x8, x9
slt x10, x11, x12
sltu x13, x14, x15
xor x16, x17, x18
srl x19, x20, x21
sra x22, x23, x24
or x25, x26, x27
and x28, x29, x30

# Instrucciones tipo I
addi x1, x2, 10
lw x3, 100(x4)
lb x5, 50(x6)
lh x7, 75(x8)
lbu x9, 60(x10)
lhu x11, 45(x12)
slti x13, x14, -5
sltiu x15, x16, 20
xori x17, x18, 15
ori x19, x20, 25
andi x21, x22, 30

# Instrucciones tipo S
sw x31, 200(x1)
sb x30, 204(x2)
sh x29, 208(x3)

# Instrucciones tipo B
beq x4, x5, loop
bne x6, x7, end
blt x8, x9, somewhere
bge x10, x11, here
bltu x12, x13, there
bgeu x14, x15, nowhere

# Instrucciones tipo U
lui x18, 0xFFF
auipc x19, 0x1FF

# Instrucciones tipo J
jal x20, func

# Instrucciones de sistema
ecall
ebreak
nop

# Labels para instrucciones de salto
loop: 
end:
somewhere:
here:
there:
nowhere:
func:
```
y su salida es 

```asm

00000000001100010000000010110011
01000000011000101000001000110011
00000000100101000001001110110011
00000000110001011010010100110011
00000000111101110011011010110011
00000001001010001100100000110011
00000001010110100101100110110011
01000001100010111101101100110011
00000001101111010110110010110011
00000001111011101111111000110011
00000000101000010000000010010011
00000110010000100010000110000011
00000011001000110000001010000011
00000100101101000001001110000011
00000011110001010100010010000011
00000010110101100101010110000011
11111111101101110010011010010011
00000001010010000011011110010011
00000000111110010100100010010011
00000001100110100110100110010011
00000001111010110111101010010011
00001101111100001010010000100011
00001101111000010000011000100011
00001101110100011001100000100011
00000010010100100000100001100011
00000010011100110001011001100011
00000010100101000100010001100011
00000010101101010101001001100011
00000010110101100110000001100011
00000000111101110111111001100011
00000000000000000000100100110111
00000000000000000000100110010111
00000001000000000000101001101111
00000000000000000000000001110011
00000000000100000000000001110011
00000000000000000000000000010011


