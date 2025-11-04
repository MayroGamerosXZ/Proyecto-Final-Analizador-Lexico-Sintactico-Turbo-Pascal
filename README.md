# 📄 Analizador Léxico-Sintáctico Turbo Pascal

Este proyecto implementa un **analizador léxico y sintáctico** para código Turbo Pascal, utilizando **JFlex** y **CUP**.  
Incluye dos modos de ejecución: **Terminal** y **Interfaz Gráfica (GUI)**.

---

## ✅ 1. Ejecución desde Terminal

### ▶️ Paso 1: Ejecutar la clase principal
Abre el proyecto en tu IDE y busca la clase:

```
AnalizadorLexicoSintacticoMayro.java
```

Haz clic en el botón verde **Run** (▶️).

Se abrirá una ventana de consola con el siguiente menú:

```
run:
Elija una opcion:
1) Generar
2) Ejecutar
3) Salir
Opcion:
```

---

### 🔹 Opción 1: **Generar**
- **Qué hace:** Genera los archivos del analizador léxico y sintáctico (usando JFlex y CUP).
- **Cuándo usarlo:** Solo si modificaste las gramáticas `.flex` o `.cup`.
- **Resultado:** Se crean/actualizan las clases `Lexer.java`, `Parser.java`, etc.
- ⚠️ **No es necesario ejecutar esto cada vez**, solo cuando cambies reglas léxicas o sintácticas.

---

### 🔹 Opción 2: **Ejecutar**
- **Qué hace:** Abre el modo interactivo para analizar código fuente.
- **Cómo funciona:**
  - Ingresa el nombre del archivo `.txt` o `.pas` que contiene el código.
  - Ejemplo:
    ```
    ejemplos/caso5.txt
    ```
  - El programa mostrará:
    - Tokens reconocidos: `[Tipo] Valor | Línea:Col`
    - Errores léxicos o sintácticos
    - Mensaje final: `Análisis completado` o `Error en línea X`

✅ Ideal para pruebas rápidas y depuración.

---

### 🔹 Opción 3: **Salir**
Cierra el programa.

---

## 🖥️ 2. Ejecución con Interfaz Gráfica (GUI)

### 🔍 Paso 1: Abre la clase `Interfaz.java`
Ubícala en la carpeta `gui` o raíz del proyecto.

### ▶️ Paso 2: Ejecuta la clase
Haz clic derecho → **Run 'Interfaz.main()'**

💡 Si no aparece la opción, asegúrate de:
- Proyecto compilado
- `Interfaz.java` contiene:
```java
public static void main(String[] args)
```

---

## 🎨 3. Uso de la Interfaz Gráfica

Al ejecutar, verás una ventana similar a:

```
┌──────────────────────────────────────────────┐
│ Analizador Lexico-Sintactico Turbo Pascal   │
├──────────────────────────────────────────────┤
│ [Abrir archivo]   [▶ Analizar]              │
├──────────────────────────────────────────────┤
│ Código Fuente                                │
│ (Área de texto editable)                     │
├──────────────────────────────────────────────┤
│ Resultado Final                              │
│ (Mostrará tokens y errores aquí)            │
└──────────────────────────────────────────────┘
```

---

### 🔹 Botón **Abrir archivo**
- Permite seleccionar un archivo `.txt` o `.pas`.
- Carga el contenido en el área **Código Fuente**.
- ✅ Puedes editar manualmente antes de analizar.

### 🔹 Botón **Analizar**
- Procesa el código actual.
- Muestra resultados en **Resultado Final**:

#### ➤ Ejemplo de éxito:
```
[ID] variable | Línea:1 Col:1
[ASIGNACION] := | Línea:1 Col:9
[NUM] 42 | Línea:1 Col:12
```

#### ➤ Ejemplo de error:
```
❌ Error léxico en Línea:2 Col:5 → Carácter inválido: '@'
❌ Error sintáctico en Línea:3 Col:1 → Esperado 'begin', encontrado 'end'
```

✅ La GUI permite corregir y reanalizar sin reiniciar.

---

## 💡 Consejos Rápidos
- Usa los archivos de ejemplo en `ejemplos/` (caso1.txt, caso5.txt).
- Si el botón **Analizar** no responde, verifica que hayas cargado código.
- Si aparece `ClassNotFoundException`, compila todo el proyecto.
- Si no se ven los botones, revisa la implementación de la GUI (`JFrame`, `JButton`, `JTextArea`).

---

## 🛑 Problemas Comunes
- **Error al analizar:** Verifica que el archivo tenga extensión `.txt` y formato válido.
- **Botones invisibles:** Asegúrate de que la clase `Interfaz` esté bien implementada.

---

✅ ¡Listo! Ahora puedes usar el analizador desde **Terminal** o **GUI** sin leer documentación extensa.

✨ ¡Feliz análisis léxico-sintáctico!
