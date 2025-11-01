# 📚 README - Teoría del Analizador Léxico-Sintáctico para Turbo Pascal

## 1. Introducción
Este proyecto implementa un **analizador léxico-sintáctico** para un subconjunto del lenguaje **Turbo Pascal**, utilizando herramientas estándar de generación de analizadores:
- **JFlex**: Generador de analizadores léxicos (lexers).
- **CUP (Construction of Useful Parsers)**: Generador de analizadores sintácticos (parsers) basados en gramáticas LR(1).

El objetivo es reconocer la estructura léxica y sintáctica de programas escritos en Pascal, validando su corrección gramatical y generando una representación intermedia útil para etapas posteriores del compilador (como análisis semántico o generación de código).

---

## 2. Componentes Teóricos

### 🔹 Analizador Léxico (`AnalizadorLexico`)
- **Función**: Divide el flujo de caracteres de entrada en **tokens** significativos.
- **Tokens reconocidos**:
  - Palabras reservadas (`PROGRAM`, `BEGIN`, `END`, `IF`, `WHILE`, etc.)
  - Identificadores (`x`, `contador`, `MiVariable`)
  - Literales: enteros (`123`), reales (`3.14`), cadenas (`'Hola'`)
  - Operadores y símbolos: `+`, `-`, `*`, `/`, `:=`, `=`, `<`, `>`, `<>`, `<=`, `>=`, `..`, `;`, `,`, `(`, `)`, `[`, `]`, etc.
- **Mecanismo**: Usa autómatas finitos deterministas (DFA) generados por JFlex a partir de expresiones regulares.
- **Gestión de posición**: Mantiene `yyline`, `yycolumn` y `yychar` para reportar errores con contexto preciso.

### 🔹 Analizador Sintáctico (`AnalizadorSintactico`)
- **Función**: Verifica que la secuencia de tokens cumpla con las reglas gramaticales del lenguaje.
- **Gramática**: Definida en formato CUP, basada en una gramática libre de contexto para Turbo Pascal.
- **Tipo de parser**: **LR(1)** — eficiente, capaz de manejar gramáticas complejas sin retroceso.
- **Salida**: Construye un **árbol de sintaxis abstracta (AST)** o una representación intermedia como valor del símbolo raíz (`result.value`).

### 🔹 Integración Lexer-Parser
- El parser solicita tokens uno a uno mediante `next_token()`.
- Cada token es una instancia de `java_cup.runtime.Symbol`, que contiene:
  - Tipo (`sym.IDENTIFICADOR`, `sym.IF`, etc.)
  - Valor asociado (ej. `"contador"`, `123`)
  - Información de ubicación (línea y columna)

---

## 3. Características del Subconjunto de Pascal Soportado
El analizador reconoce construcciones típicas de Turbo Pascal, incluyendo:
- Declaraciones de programa, variables, constantes y tipos
- Estructuras de control: `if-then-else`, `while`, `for`, `repeat-until`
- Procedimientos y funciones
- Tipos básicos: `integer`, `real`, `boolean`, `string`
- Expresiones aritméticas, lógicas y relacionales
- Entrada/salida: `read`, `readln`, `write`, `writeln`

> ⚠️ **Nota**: No se incluye análisis semántico (verificación de tipos, declaración previa de variables, etc.), solo análisis léxico y sintáctico.

---

## 4. Herramientas Utilizadas

| Herramienta | Propósito |
|-----------|----------|
| **JFlex** | Genera el analizador léxico a partir de un archivo `.flex` |
| **CUP** | Genera el parser a partir de un archivo `.cup` con reglas gramaticales |
| **Java** | Lenguaje de implementación |
| **Swing** | Interfaz gráfica de usuario |


===============================================================================


# ▶️ README - Funcionamiento del Programa

## 1. Descripción General
La aplicación **InterfazAnalizador** es una herramienta gráfica que permite:
- Cargar código fuente en Pascal desde un archivo (`.pas` o `.txt`)
- Ejecutar análisis léxico y sintáctico en tiempo real
- Visualizar mensajes del proceso de análisis
- Mostrar el resultado final generado por el parser

Ideal para fines educativos, depuración de gramáticas o validación de programas Pascal simples.

---

## 2. Requisitos
- **Java 11 o superior**
- Archivos generados por JFlex y CUP ya compilados en el proyecto:
  - `AnalizadorLexico.java`
  - `AnalizadorSintactico.java`
  - `sym.java` (definición de símbolos/tokens)

---

## 3. Interfaz de Usuario

### 🖥️ Componentes principales

| Elemento | Función |
|--------|--------|
| **Área de código fuente** | Editor donde se pega o carga el código Pascal |
| **Botón "Abrir archivo"** | Permite seleccionar un archivo `.pas` o `.txt` |
| **Botón "Analizar"** | Inicia el proceso de análisis léxico-sintáctico |
| **Panel de salida** | Muestra mensajes del sistema (`System.out`, errores, etc.) |
| **Panel de resultado final** | Muestra la salida del parser (ej. AST serializado) |
| **Barra de estado** | Indica el estado actual: "Listo", "Analizando...", "✅ Éxito", "❌ Error" |

---

## 4. Flujo de Ejecución
1. **Carga de código**:
   - El usuario escribe directamente en el editor o abre un archivo.
   - Se valida que no esté vacío.
2. **Análisis**:
   - Al hacer clic en **"Analizar"**:
     - Se redirige temporalmente `System.out` y `System.err` a un buffer.
     - Se crea una instancia de `AnalizadorLexico` con el texto del código.
     - Se pasa el lexer al `AnalizadorSintactico`.
     - Se invoca `parser.parse()`.
3. **Resultados**:
   - **Salida estándar**: Se muestra en el panel *Salida* (útil para depuración).
   - **Resultado del parser**: Si el análisis es exitoso, `result.value` se imprime en *Resultado Final*.
   - **Errores**:
     - Errores léxicos (caracteres ilegales) → lanzan `Error` con ubicación.
     - Errores sintácticos → atrapados como excepciones y mostrados en rojo.
4. **Finalización**:
   - Las salidas del sistema se restauran.
   - La barra de estado refleja el resultado.

---

## 5. Ejemplo de Uso
1. Abrir un archivo como:
   ```pascal
   
   program Hola;
   begin
     writeln('Hola mundo');
   end.


  ```
  PROGRAM AreaCirculo;
  CONST
  PI = 3.1416;
  VAR
  radio, area: REAL;
  BEGIN
  WRITE('Radio: ');
  READLN(radio);
  area := PI * radio * radio;
  WRITELN('Área: ', area);
  READKEY;
  END.



  PROGRAM SalidaMultiple;
  VAR
  nombre: STRING;
  edad: INTEGER;
  BEGIN
  WRITE('Nombre: ');
  READLN(nombre);
  WRITE('Edad: ');
  READLN(edad);
  WRITELN('Hola, ', nombre, '! Tienes ', edad, ' años.');
  READKEY;
  END.


  PROGRAM ContadorFor;
  VAR
  i: INTEGER;
  BEGIN
  FOR i := 1 TO 5 DO
  WRITELN('Número: ', i);
  READKEY;
  END.







 
