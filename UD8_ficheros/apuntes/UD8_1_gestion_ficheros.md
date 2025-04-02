# Gestion de ficheros y eventos

- [1. Introducción a ficheros y eventos](#1-introducción-a-ficheros-y-eventos)
  - [1.1. Importancia de la gestión de ficheros en programación](#11-importancia-de-la-gestión-de-ficheros-en-programación)
  - [1.2. Conceptos básicos: ficheros, directorios y flujos de datos](#12-conceptos-básicos-ficheros-directorios-y-flujos-de-datos)
  - [1.3. Fragmentos de código](#13-fragmentos-de-código)
- [2. Flujos (Streams) en Java](#2-flujos-streams-en-java)
  - [2.1. Concepto de flujo de datos](#21-concepto-de-flujo-de-datos)
    - [2.1.1. Diferencias clave entre Streams de E/S y Streams de Java 8](#211-diferencias-clave-entre-streams-de-es-y-streams-de-java-8)
  - [2.2. Tipos de flujos: bytes vs. caracteres](#22-tipos-de-flujos-bytes-vs-caracteres)
    - [2.2.1. Flujos de bytes (`InputStream`/`OutputStream`)](#221-flujos-de-bytes-inputstreamoutputstream)
    - [2.2.2. Flujos de caracteres (`Reader`/`Writer`)](#222-flujos-de-caracteres-readerwriter)
  - [2.3. Clases principales de flujos](#23-clases-principales-de-flujos)
  - [2.4. Excepciones en flujos](#24-excepciones-en-flujos)
    - [2.4.1. Excepción `IOException`](#241-excepción-ioexception)
    - [2.4.2. Problema al no cerrar los recursos](#242-problema-al-no-cerrar-los-recursos)
    - [2.4.3. Uso de `try-with-resources` en flujos de datos](#243-uso-de-try-with-resources-en-flujos-de-datos)
    - [2.4.4. Múltiples recursos en `try-with-resources`](#244-múltiples-recursos-en-try-with-resources)
- [3. Manipulación de ficheros y directorios](#3-manipulación-de-ficheros-y-directorios)
  - [3.1. Operaciones con ficheros y directorios](#31-operaciones-con-ficheros-y-directorios)
    - [3.1.1. Creación de ficheros y directorios](#311-creación-de-ficheros-y-directorios)
    - [3.1.2. Eliminación de ficheros y directorios](#312-eliminación-de-ficheros-y-directorios)
    - [3.1.3. Renombrado de ficheros y directorios](#313-renombrado-de-ficheros-y-directorios)
  - [3.2. Apertura y cierre de ficheros](#32-apertura-y-cierre-de-ficheros)
    - [3.2.1. Modos de acceso](#321-modos-de-acceso)
  - [3.3. Tipos de acceso según el direccionamiento](#33-tipos-de-acceso-según-el-direccionamiento)
- [4. Lectura y escritura de ficheros](#4-lectura-y-escritura-de-ficheros)
  - [4.1. Ficheros de texto](#41-ficheros-de-texto)
    - [4.1.1. Lectura de un fichero de texto](#411-lectura-de-un-fichero-de-texto)
    - [4.1.2. Escritura de un fichero de texto](#412-escritura-de-un-fichero-de-texto)
    - [4.1.3. Ejemplo práctico de lectura y escritura de archivos de texto](#413-ejemplo-práctico-de-lectura-y-escritura-de-archivos-de-texto)
    - [4.1.4. Ficheros CSV](#414-ficheros-csv)
  - [4.2. Ficheros binarios](#42-ficheros-binarios)
    - [4.2.1. Lectura de un fichero binario](#421-lectura-de-un-fichero-binario)
    - [4.2.2. Escritura de un fichero binario](#422-escritura-de-un-fichero-binario)
    - [4.2.3. Ejemplo: Copia de una imagen](#423-ejemplo-copia-de-una-imagen)
  - [4.3. Ficheros de acceso aleatorio](#43-ficheros-de-acceso-aleatorio)
  - [4.4. Ficheros ZIP](#44-ficheros-zip)
    - [4.4.1. Compresión de archivos](#441-compresión-de-archivos)
    - [4.4.2. Descompresión de archivos](#442-descompresión-de-archivos)
- [5. Flujos de consola](#5-flujos-de-consola)
  - [5.1. Flujos de entrada estándar](#51-flujos-de-entrada-estándar)
  - [5.2. Flujos de salida estándar](#52-flujos-de-salida-estándar)
    - [5.2.1. Formato de salida](#521-formato-de-salida)
- [6. Flujos de `String`](#6-flujos-de-string)
  - [6.1. StringReader](#61-stringreader)
  - [6.2. StringWriter](#62-stringwriter)
  - [6.3. Uso de BufferedReader con StringReader](#63-uso-de-bufferedreader-con-stringreader)
  - [6.4. Uso práctico de `StringReader`](#64-uso-práctico-de-stringreader)
- [7. Flujos tokenizados](#7-flujos-tokenizados)
  - [7.1. La clase `StreamTokenizer`](#71-la-clase-streamtokenizer)
    - [7.1.1. Configuración de `StreamTokenizer`](#711-configuración-de-streamtokenizer)
- [8. Flujos orientados a objetos](#8-flujos-orientados-a-objetos)
  - [8.1. Serialización de objetos](#81-serialización-de-objetos)
  - [8.2. Deserialización de objetos](#82-deserialización-de-objetos)
  - [8.3. Consideraciones sobre la serialización](#83-consideraciones-sobre-la-serialización)
    - [8.3.1. Identificador de versión (`serialVersionUID`)](#831-identificador-de-versión-serialversionuid)
    - [8.3.2. Compatibilidad entre versiones](#832-compatibilidad-entre-versiones)
    - [8.3.3. Exclusión de atributos (`transient`)](#833-exclusión-de-atributos-transient)
    - [8.3.4. Control personalizado con `writeObject` y `readObject`](#834-control-personalizado-con-writeobject-y-readobject)
    - [8.3.5. Serialización y herencia](#835-serialización-y-herencia)
    - [8.3.6. Serialización de objetos en colecciones](#836-serialización-de-objetos-en-colecciones)
    - [8.3.7. Referencias a objetos no serializables](#837-referencias-a-objetos-no-serializables)
    - [8.3.8. Interfaces relacionadas (`Externalizable`)](#838-interfaces-relacionadas-externalizable)
  - [8.4. ObjectInputStream y ObjectOutputStream](#84-objectinputstream-y-objectoutputstream)
- [9. Procesamiento de JSON en archivos](#9-procesamiento-de-json-en-archivos)
  - [9.1. Lectura de un archivo JSON en Java](#91-lectura-de-un-archivo-json-en-java)
    - [9.1.1. Ejemplo: lectura de un archivo JSON con Jackson](#911-ejemplo-lectura-de-un-archivo-json-con-jackson)
  - [9.2. Escritura de un archivo JSON en Java](#92-escritura-de-un-archivo-json-en-java)
    - [9.2.1. Ejemplo: escritura de un objeto Java en JSON](#921-ejemplo-escritura-de-un-objeto-java-en-json)
  - [9.3. Procesamiento de JSON como flujo de datos](#93-procesamiento-de-json-como-flujo-de-datos)
    - [9.3.1. Ejemplo: lectura de un JSON línea por línea](#931-ejemplo-lectura-de-un-json-línea-por-línea)
  - [9.4. Manejo de archivos JSON con colección de datos](#94-manejo-de-archivos-json-con-colección-de-datos)
    - [9.4.1. Escritura de una lista de objetos en JSON](#941-escritura-de-una-lista-de-objetos-en-json)
    - [9.4.2. Lectura de una lista de objetos desde JSON](#942-lectura-de-una-lista-de-objetos-desde-json)

## 1. Introducción a ficheros y eventos

Hasta el momento, hemos estado desarrollando programas en los que creábamos una serie de objetos o estructuras de datos (colecciones como arrays, listas, mapas...). Esos datos se almacenaban en memoria dinámica, y cuando el programa terminaba, los datos se perdían. Es decir, cada vez que ejecutábamos el programa, empezábamos desde cero.

En nuestra aplicación de gestión de bibliotecas implica que cada vez que ejecutamos el programa, tenemos que volver a introducir las publicaciones, usuarios, préstamos... lo cual no es muy práctico ni viable. Por eso tenemos que hablar de la persistencia de datos.

La **persistencia de datos** es la capacidad de almacenar información de forma permanente, de modo que los datos se mantengan entre ejecuciones del programa. Para lograr esto, podemos hacerlo a través de **ficheros** o **bases de datos**, que permiten almacenar nuestros datos de manera estructurada en un medio de almacenamiento persistente (memoria secundaria, típicamente un disco duro o una unidad SSD).

- **Bases de datos**: Permiten almacenar y manipular grandes volúmenes de datos con estructuras optimizadas para consultas rápidas.
- **Ficheros**: Son una alternativa más simple que se usa cuando los datos deben guardarse en un formato estructurado (como CSV, JSON, XML) o en archivos binarios.

En esta unidad vamos a aprender a trabajar con ficheros. Veremos los conceptos básicos relacionados con ficheros y directorios, los diferentes tipos de ficheros, los flujos de datos y cómo leer y escribir en ellos. También veremos cómo gestionar eventos, que son acciones o sucesos que ocurren durante la ejecución de un programa.

### 1.1. Importancia de la gestión de ficheros en programación

En el desarrollo de software, la **gestión de ficheros** es una tarea fundamental que permite a las aplicaciones interactuar con datos persistentes. Los ficheros son esenciales para almacenar información que debe conservarse entre ejecuciones de un programa, como **configuraciones**, **datos de usuarios** o **registros de transacciones**. Además, la capacidad de leer y escribir ficheros es crucial para trabajar con formatos comunes como **CSV**, **JSON** o **archivos comprimidos** (ZIP), que son ampliamente utilizados en el mundo real.

En este tema, aprenderemos cómo manejar ficheros en Java, desde operaciones básicas como la creación y eliminación de archivos, hasta técnicas avanzadas como la compresión de datos y la lectura/escritura de ficheros estructurados.

### 1.2. Conceptos básicos: ficheros, directorios y flujos de datos

Antes de profundizar en el código, es importante entender algunos conceptos clave:

- **Ficheros**: Un fichero es una unidad de almacenamiento de datos en un sistema de archivos. Puede contener texto, imágenes, datos binarios, etc.
- **Directorios**: Un directorio es una carpeta que organiza ficheros y otros directorios. Proporciona una estructura jerárquica para almacenar información.
- **Flujos de datos (Streams)**: En Java, los flujos son secuencias de datos que permiten **leer** o **escribir** información. Existen dos tipos principales: flujos de **bytes** (`InputStream`/`OutputStream`) y flujos de **caracteres** (`Reader`/`Writer`).

### 1.3. Fragmentos de código

A lo largo de este tema se presentan diferentes fragmentos de código representativos. Puedes encontrar un proyecto con extractos similares para poder probarlos en este [enlace de Github](https://github.com/danielmartinan/UD8_ficheros/)

## 2. Flujos (Streams) en Java

### 2.1. Concepto de flujo de datos

En Java, un flujo (stream) es una secuencia de datos que puede ser leída o escrita. Los flujos son una abstracción que permite trabajar con diferentes fuentes de datos (ficheros, conexiones de red, entradas de teclado, etc.) de manera uniforme. Existen dos tipos principales de flujos:

1. **Flujos de bytes**: Trabajan con datos en formato binario. Se utilizan para leer y escribir ficheros binarios, como imágenes o archivos comprimidos.
2. **Flujos de caracteres**: Trabajan con datos en formato de texto. Son ideales para manejar ficheros de texto, como archivos CSV o documentos.

Los streams de Java son una forma de trabajar con datos de manera secuencial, permitiendo leer o escribir información de forma continua. Los flujos pueden ser de entrada (input) o de salida (output), dependiendo de si se lee o se escribe información. Además, las clases y métodos que emplearemos serán las mismas independientemente del dispositivo o tipo de fuente con el que estemos trabajando, por ejemplo, un fichero, la entrada estándar o una conexión de red (socket).

#### 2.1.1. Diferencias clave entre Streams de E/S y Streams de Java 8

Es importante diferenciar dos conceptos de "Streams" que existen en Java:

- **Streams de Entrada/Salida** (`java.io` y `java.nio`)
  - Se utilizan para manejar **flujos de bytes o caracteres** en operaciones de lectura y escritura.
  - Ejemplo: FileInputStream, FileReader, BufferedWriter.
- **Streams de Java 8** (`java.util.stream`)
  - Se utilizan en **programación funcional** para procesar colecciones de datos de manera eficiente.
  - Ejemplo: `List<String> nombres = lista.stream().filter(s -> s.startsWith("A")).collect(Collectors.toList());`

### 2.2. Tipos de flujos: bytes vs. caracteres

#### 2.2.1. Flujos de bytes (`InputStream`/`OutputStream`)

- **`InputStream`**: Clase base para leer datos binarios. Ejemplos comunes incluyen `FileInputStream` (para leer ficheros) y `BufferedInputStream` (para mejorar el rendimiento).
- **`OutputStream`**: Clase base para escribir datos binarios. Ejemplos comunes incluyen `FileOutputStream` (para escribir ficheros) y `BufferedOutputStream` (para mejorar el rendimiento).

#### 2.2.2. Flujos de caracteres (`Reader`/`Writer`)

- **`Reader`**: Clase base para leer datos de texto. Ejemplos comunes incluyen `FileReader` (para leer ficheros de texto) y `BufferedReader` (para mejorar el rendimiento).
- **`Writer`**: Clase base para escribir datos de texto. Ejemplos comunes incluyen `FileWriter` (para escribir ficheros de texto) y `BufferedWriter` (para mejorar el rendimiento).

### 2.3. Clases principales de flujos

Java proporciona una jerarquía de clases para trabajar con flujos. Algunas de las más importantes son:

- **`FileInputStream` y `FileOutputStream`**: Para leer y escribir ficheros binarios.
- **`FileReader` y `FileWriter`**: Para leer y escribir ficheros de texto.
- **`BufferedReader` y `BufferedWriter`**: Para mejorar la eficiencia al trabajar con ficheros de texto.
- **`DataInputStream` y `DataOutputStream`**: Para leer y escribir tipos de datos primitivos (como `int`, `double`, etc.).
- **`Scanner`**: Para leer datos de la entrada estándar (teclado).
- **`PrintWriter`**: Para escribir datos en la salida estándar (consola).
- **`ObjectInputStream` y `ObjectOutputStream`**: Para leer y escribir objetos serializados.
- **`StringReader` y `StringWriter`**: Para leer y escribir cadenas de texto en memoria.
- **`StreamTokenizer`**: Para analizar datos en formato de texto.

Puedes encontrar más información sobre las clases `FileReader`, `FileWriter`, `BufferedReader` y `BufferedWriter` y otras clases e interfaces, así como de excepciones, del paquete java.io en la [documentación oficial de Java](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/io/package-summary.html).

A continuación iremos profundizando en los diferentes conceptos relacionados con los flujos de datos en java, así como las clases y métodos empleados.

### 2.4. Excepciones en flujos

Cuando se trabaja con ficheros y flujos de datos en Java, es fundamental manejar correctamente las excepciones para evitar errores como archivos inexistentes, permisos insuficientes o problemas al cerrar recursos.  

#### 2.4.1. Excepción `IOException`

La mayoría de las clases que trabajan con ficheros lanzan una excepción del tipo `IOException`, que indica que ha ocurrido un error de entrada/salida. Algunos de los casos más comunes son:  

- Intentar leer un archivo que no existe.
- No tener permisos para acceder al archivo.
- Un error en el sistema de archivos o en el dispositivo de almacenamiento.

Ejemplo de manejo básico de `IOException`:

```java
import java.io.FileReader;
import java.io.IOException;

public class EjemploIOException {
    public static void main(String[] args) {
        try {
            FileReader lector = new FileReader("archivo.txt");
            lector.close();
        } catch (IOException e) {
            System.out.println("Error al acceder al archivo: " + e.getMessage());
        }
    }
}
```

#### 2.4.2. Problema al no cerrar los recursos

Un error común en la gestión de ficheros es no cerrar correctamente los flujos después de usarlos. Si un flujo de lectura/escritura queda abierto, puede provocar **bloqueos de archivo**, **fugas de memoria** o **corrupción de datos**.

Ejemplo **incorrecto**:

```java
public static void leerArchivo(String nombreArchivo) throws IOException {
    FileReader lector = new FileReader(nombreArchivo);
    int caracter;
    while ((caracter = lector.read()) != -1) {
        System.out.print((char) caracter);
    }
    // ❌ ERROR: El flujo no se cierra si ocurre una excepción
    lector.close();
}
```

Si `read()` lanza una excepción, el `close()` nunca se ejecutará. Esto se soluciona con **`try-with-resources`**.

#### 2.4.3. Uso de `try-with-resources` en flujos de datos  

Desde Java 7, la mejor manera de manejar flujos de datos es mediante **`try-with-resources`**, que se encarga de cerrar automáticamente los recursos al salir del bloque `try`.

🔹 **Ventajas de `try-with-resources`:**  
✔ Evita olvidos al cerrar recursos.  
✔ Reduce la cantidad de código necesario.  
✔ Mejora la legibilidad y mantenibilidad.  

Ejemplo **correcto**:

```java
public static void leerArchivo(String nombreArchivo) {
    try (FileReader lector = new FileReader(nombreArchivo)) {
        int caracter;
        while ((caracter = lector.read()) != -1) {
            System.out.print((char) caracter);
        }
    } catch (IOException e) {
        System.out.println("Error al leer el archivo: " + e.getMessage());
    }
}  
```

**Cómo funciona `try-with-resources`**:

1. Declara el objeto dentro de los paréntesis del `try`.  
2. Java **cierra automáticamente** el recurso cuando se sale del bloque `try`, sin necesidad de llamar a `close()`.  
3. Funciona con cualquier clase que implemente la interfaz **`AutoCloseable`** o **`Closeable`**.

#### 2.4.4. Múltiples recursos en `try-with-resources`

También es posible declarar **varios recursos** en un solo `try`:

```java
try (
    FileReader lector = new FileReader("archivo.txt");
    BufferedReader buffer = new BufferedReader(lector)
) {
    String linea;
    while ((linea = buffer.readLine()) != null) {
        System.out.println(linea);
    }
} catch (IOException e) {
    System.out.println("Error: " + e.getMessage());
}
```

Aquí, tanto `lector` como `buffer` se cerrarán automáticamente al finalizar el `try`.

En los siguientes apartados, en los que profundizaremos en la lectura y escritura de ficheros, veremos ejemplos concretos de cómo trabajar con flujos en Java y cómo manejar las excepciones de forma adecuada en cada caso.

## 3. Manipulación de ficheros y directorios

En este apartado, aprenderemos a realizar operaciones básicas con ficheros y directorios en Java, como la creación, eliminación, renombrado y listado. Estas operaciones son esenciales para gestionar datos persistentes y organizar la información en un sistema de archivos.

### 3.1. Operaciones con ficheros y directorios

#### 3.1.1. Creación de ficheros y directorios

Java proporciona la clase `File` (y, a partir de Java 7, la clase `Path` y `Files`) para trabajar con ficheros y directorios.

##### Clase `File`

La clase `File` representa un fichero o directorio en el sistema de archivos. Algunas operaciones comunes incluyen:

- **Crear un fichero**: `createNewFile()`.
- **Crear un directorio**: `mkdir()`.
- **Eliminar un fichero o directorio**: `delete()`.
- **Renombrar un fichero o directorio**: `renameTo()`.
- **Comprobar si existe un fichero o directorio**: `exists()`.
- **Listar los ficheros de un directorio**: `listFiles()`.
- **Obtener información sobre un fichero o directorio**: `getName()`, `getPath()`, `isFile()`, `isDirectory()`, etc.

##### Clase `Path` y `Files`

A partir de Java 7, se introdujeron las clases `Path` y `Files` para trabajar con rutas de ficheros y realizar operaciones de forma más sencilla y segura.

La clase `Path` representa una ruta de fichero o directorio en el sistema de archivos. Algunas operaciones comunes incluyen:

##### Crear un fichero

Utilizando la clase `File`, podemos crear un fichero de la siguiente manera:

```java
import java.io.File;
import java.io.IOException;

public class CrearFichero {
    public static void main(String[] args) {
        File fichero = new File("archivo.txt"); // Ruta del fichero

        try {
            if (fichero.createNewFile()) {
                System.out.println("Fichero creado correctamente.");
            } else {
                System.out.println("El fichero ya existe.");
            }
        } catch (IOException e) {
            System.err.println("Error al crear el fichero: " + e.getMessage());
        }
    }
}
```

El método `createNewFile()` crea un nuevo fichero en la ruta especificada. Si el fichero ya existe, devuelve `false`.

Como podemos ver, se gestiona la excepción `IOException` para manejar posibles errores durante la creación del fichero.

##### Crear un directorio

Para crear un directorio, utilizamos el método `mkdir()` de la clase `File`:

```java
import java.io.File;

public class CrearDirectorio {
    public static void main(String[] args) {
        File directorio = new File("miDirectorio"); // Ruta del directorio

        if (directorio.mkdir()) {
            System.out.println("Directorio creado correctamente.");
        } else {
            System.out.println("El directorio ya existe o no se pudo crear.");
        }
    }
}
```

Al igual que `createNewFile()`, el método `mkdir()` si el directorio ya existe, devuelve `false`.

En este caso no es necesario gestionar excepciones, ya que el método `mkdir()` no lanza excepciones.

##### Uso de la clase `Files`

A partir de Java 7, se recomienda utilizar la clase `Files` para realizar operaciones de ficheros y directorios de forma más sencilla y segura. Por ejemplo, para crear un fichero:

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.io.IOException;

public class CrearFicheroConFiles {
    public static void main(String[] args) {
        Path rutaFichero = Paths.get("archivo.txt"); // Ruta del fichero

        try {
            Files.createFile(rutaFichero); // Crea el fichero
            System.out.println("Fichero creado correctamente.");
        } catch (IOException e) {
            System.err.println("Error al crear el fichero: " + e.getMessage());
        }

        //Borramos el fichero creado
        try {
            Files.delete(rutaFichero); // Elimina el fichero
            System.out.println("Fichero eliminado correctamente.");
        } catch (IOException e) {
            System.err.println("Error al eliminar el fichero: " + e.getMessage());
        }
    }
}
```

#### 3.1.2. Eliminación de ficheros y directorios

Para eliminar ficheros y directorios, se utiliza el método `delete()` de la clase `File`.

##### Eliminar un fichero

```java
import java.io.File;

public class EliminarFichero {
    public static void main(String[] args) {
        File fichero = new File("archivo.txt"); // Ruta del fichero

        if (fichero.delete()) {
            System.out.println("Fichero eliminado correctamente.");
        } else {
            System.out.println("El fichero no existe o no se pudo eliminar.");
        }
    }
}
```

##### Eliminar un directorio

```java
import java.io.File;

public class EliminarDirectorio {
    public static void main(String[] args) {
        File directorio = new File("miDirectorio"); // Ruta del directorio

        if (directorio.delete()) {
            System.out.println("Directorio eliminado correctamente.");
        } else {
            System.out.println("El directorio no existe o no se pudo eliminar.");
        }
    }
}
```

#### 3.1.3. Renombrado de ficheros y directorios

Para renombrar un fichero o directorio, se utiliza el método `renameTo()` de la clase `File`.

```java
import java.io.File;

public class RenombrarFichero {
    public static void main(String[] args) {
        File ficheroOriginal = new File("archivo.txt"); // Ruta del fichero original
        File ficheroRenombrado = new File("archivo_renombrado.txt"); // Nueva ruta

        if (ficheroOriginal.renameTo(ficheroRenombrado)) {
            System.out.println("Fichero renombrado correctamente.");
        } else {
            System.out.println("No se pudo renombrar el fichero.");
        }
    }
}
```

### 3.2. Apertura y cierre de ficheros

#### 3.2.1. Modos de acceso

Al trabajar con ficheros, es importante especificar el modo de acceso:

- **Lectura**: Solo se permite leer el contenido del fichero.
- **Escritura**: Solo se permite escribir en el fichero (sobrescribe el contenido existente).
- **Append**: Permite añadir contenido al final del fichero sin sobrescribirlo.

En Java, al abrir un fichero para lectura o escritura, podemos especificar el modo de acceso mediante los siguientes constructores:

##### Ejemplo de apertura en modo append

```java
import java.io.FileWriter;
import java.io.IOException;

public class ModoAppend {
    public static void main(String[] args) {
        try (FileWriter fw = new FileWriter("archivo.txt", true)) { // true para modo append
            fw.write("Nueva línea añadida.\n");
            System.out.println("Datos añadidos correctamente.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el fichero: " + e.getMessage());
        }
    }
}
```

### 3.3. Tipos de acceso según el direccionamiento

Otro criterio de clasificación de los ficheros es el **tipo de acceso** que permiten, distinguiendo fundamentalmente entre dos:

- **Acceso secuencial**: Se lee o escribe el fichero de manera secuencial, recorriendo su contenido en orden hasta llegar a la información de interés. Funcionan análogamente como una cinta de casete: para llegar a una parte concreta, hay que avanzar desde el principio. Es como funcionan las estructuras de datos como las **listas enlazadas**.
- **Acceso aleatorio**: Se puede leer o escribir en cualquier posición del fichero, dada dicha posición. Es el modo de funcionamiento de la memoria RAM, donde se puede acceder a cualquier dirección de memoria sin necesidad de recorrerla desde el principio. Es como funcionan las estructuras de datos como **los arrays**.

![alt text](./img/sequential_vs_random_access.png)

## 4. Lectura y escritura de ficheros

En este apartado, profundizaremos en cómo leer y escribir información en ficheros, tanto de texto como binarios. También veremos cómo trabajar con formatos específicos, como ficheros CSV y archivos comprimidos (ZIP).

### 4.1. Ficheros de texto

#### 4.1.1. Lectura de un fichero de texto

Para leer un fichero de texto, se utilizan clases como `FileReader` y `BufferedReader`. Estas clases permiten leer el contenido línea por línea o carácter por carácter.

##### Clase FileReader

La clase `FileReader` se utiliza para leer caracteres de un fichero de texto. Es importante cerrar el flujo de datos al finalizar su uso para liberar los recursos asociados. Para ello, se puede utilizar un bloque `try-with-resources` para asegurarse de que el flujo se cierre automáticamente.

```java
import java.io.FileReader;
import java.io.IOException;

public class LeerFicheroTexto {
    public static void main(String[] args) {
        String rutaFichero = "archivo.txt"; // Ruta del fichero de texto

        try (FileReader fr = new FileReader(rutaFichero)) {
            int caracter;
            while ((caracter = fr.read()) != -1) {
                System.out.print((char) caracter); // Muestra cada carácter leído
            }
        } catch (IOException e) {
            System.err.println("Error al leer el fichero: " + e.getMessage());
        }
    }
}
```

##### Clase BufferedReader

La clase `BufferedReader` se utiliza para leer líneas de texto de un fichero. Proporciona métodos como `readLine()` para leer una línea completa y `read()` para leer caracteres individuales. Al igual que con `FileReader`, es importante cerrar el flujo de datos al finalizar su uso. A diferencia de `FileReader`, `BufferedReader` permite leer líneas completas de texto, y es, en general, más eficiente para leer ficheros de texto.

##### Ejemplo: Lectura línea por línea

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class LeerFicheroTexto {
    public static void main(String[] args) {
        String rutaFichero = "archivo.txt"; // Ruta del fichero de texto

        try (BufferedReader br = new BufferedReader(new FileReader(rutaFichero))) {
            String linea;
            while ((linea = br.readLine()) != null) {
                System.out.println(linea); // Muestra cada línea leída
            }
        } catch (IOException e) {
            System.err.println("Error al leer el fichero: " + e.getMessage());
        }
    }
}
```

Como podemos ver, el constructor de `BufferedReader` recibe un objeto de tipo `FileReader` para leer el fichero de texto. Luego, utilizamos el método `readLine()` para leer cada línea del fichero.

En el ejemplo anterior utilizamos un bloque `try-with-resources` para asegurarnos de que el flujo de datos se cierre correctamente al finalizar la lectura. Si utilizásemos un try-catch tradicional, tendríamos que cerrar el flujo de datos manualmente en el bloque `finally`:

```java
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader(rutaFichero));
    // Leer el fichero
} catch (IOException e) {
    // Manejar la excepción
} finally {
    if (br != null) {
        try {
            br.close();
        } catch (IOException e) {
            // Manejar la excepción
        }
    }
}
```

Otros métodos útiles de `BufferedReader` incluyen `read(char[] cbuf, int off, int len)` para leer una porción de un array de caracteres, y `skip(long n)` para saltar un número específico de caracteres.

#### 4.1.2. Escritura de un fichero de texto

Para escribir en un fichero de texto, se utilizan clases como `FileWriter` y `BufferedWriter`. Estas clases permiten escribir cadenas de texto de manera eficiente.

##### Ejemplo: Escritura de líneas de texto

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class EscribirFicheroTexto {
    public static void main(String[] args) {
        String rutaFichero = "salida.txt"; // Ruta del fichero de texto de salida

        try (BufferedWriter bw = new BufferedWriter(new FileWriter(rutaFichero))) {
            bw.write("Línea 1"); // Escribe una línea
            bw.newLine(); // Añade un salto de línea
            bw.write("Línea 2");
            System.out.println("Datos escritos correctamente.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el fichero: " + e.getMessage());
        }
    }
}
```

Con `BufferedWriter`, podemos escribir líneas de texto en un fichero de manera eficiente. El método `newLine()` se utiliza para añadir un salto de línea al final de cada línea escrita.

Si no utilizásemos un bloque `try-with-resources`, tendríamos que cerrar manualmente el flujo de datos al finalizar la escritura, mediante el método `close()`, al igual que en el caso de la lectura.

Otros métodos útiles de `BufferedWriter` incluyen `write(char[] cbuf, int off, int len)` para escribir una porción de un array de caracteres, y `flush()` para forzar la escritura de los datos almacenados en el búfer.

#### 4.1.3. Ejemplo práctico de lectura y escritura de archivos de texto

A continuación, se muestra un ejemplo práctico que lee un archivo de texto, cuenta las palabras y escribe el conteo en otro archivo.

```java	
import java.io.*;
import java.nio.file.*;
import java.util.*;
import java.util.regex.Pattern;
import java.util.stream.Collectors;

public class ContadorPalabras {
    public static void main(String[] args) {
        String archivoEntrada = "entrada.txt";
        String archivoSalida = "salida.txt";
        
        // Mapa para almacenar las palabras y su frecuencia
        Map<String, Integer> frecuenciaPalabras = new HashMap<>();
        
        try {
            // Leer el archivo línea por línea
            List<String> lineas = Files.readAllLines(Paths.get(archivoEntrada));
            
            // Procesar cada línea
            for (String linea : lineas) {
                // Dividir en palabras, ignorando signos de puntuación y pasando a minúsculas
                String[] palabras = linea.toLowerCase().split("\\W+");

                for (String palabra : palabras) {
                    if (!palabra.isEmpty()) {
                        frecuenciaPalabras.put(palabra, frecuenciaPalabras.getOrDefault(palabra, 0) + 1);
                    }
                }
            }
            
            // Ordenar por frecuencia descendente y por orden alfabético en caso de empate
            List<Map.Entry<String, Integer>> listaOrdenada = frecuenciaPalabras.entrySet()
                    .stream()
                    .sorted(
                            Comparator.comparing(Map.Entry<String, Integer>::getValue).reversed()
                                    .thenComparing(Map.Entry::getKey)
                    )
                    .collect(Collectors.toList());
            
            // Escribir en el archivo de salida
            try (BufferedWriter writer = new BufferedWriter(new FileWriter(archivoSalida))) {
                for (Map.Entry<String, Integer> entry : listaOrdenada) {
                    writer.write(entry.getKey() + ": " + entry.getValue());
                    writer.newLine();
                }
            }
            
            System.out.println("Conteo de palabras completado. Resultado en " + archivoSalida);
            
        } catch (IOException e) {
            System.err.println("Error al procesar el archivo: " + e.getMessage());
        }
    }
}
```

Si creamos un archivo "entrada.txt" con el siguiente contenido:

```plaintext
Este es un ejemplo de texto. Un ejemplo de palabras. Podemos poner todas las palabras que queramos: palabras bonitas, palabras feas, palabras largas y palabras cortas.
```

Al ejecutar el programa, se generará un archivo "salida.txt" con el siguiente contenido:

```plaintext
palabras: 6
de: 2
ejemplo: 2
un: 2
bonitas: 1
cortas: 1
es: 1
este: 1
feas: 1
largas: 1
las: 1
podemos: 1
poner: 1
que: 1
queramos: 1
texto: 1
todas: 1
y: 1
```

Como podemos ver, obtenemos el listado completo de palabras presentes, ordenadas de mayor a menor frecuencia y, en caso de empate, ordenadas alfabéticamente.

#### 4.1.4. Ficheros CSV

Los ficheros CSV (Comma-Separated Values) son un formato común para almacenar datos tabulares. Aunque se pueden manejar manualmente como ficheros de texto (utilizando `BufferedReader` y `BufferedWriter`), es recomendable utilizar librerías como **`OpenCSV`** para simplificar el proceso.

Puedes encontrar toda la documentación sobre OpenCSV en su [página oficial](http://opencsv.sourceforge.net/).

##### Lectura de un fichero CSV con OpenCSV

OpenCSV es una librería de código abierto que facilita la lectura y escritura de ficheros CSV en Java. Java no tiene una API nativa específica para leer archivos CSV, pero puedes usar `BufferedReader` y `String.split(",")` para procesarlos manualmente. Sin embargo, esta solución es limitada porque no maneja correctamente:

✔ Comas dentro de valores entrecomillados ("Hola, mundo", 123).
✔ Líneas con caracteres especiales o codificaciones específicas.
✔ Campos vacíos o valores nulos.

Para un procesamiento más robusto, `OpenCSV` es una mejor opción porque:

✔ Soporta comillas y separadores personalizados.
✔ Permite leer CSV en listas u objetos directamente.
✔ Maneja grandes volúmenes de datos de forma más eficiente.

Para leer un fichero CSV con OpenCSV, se utiliza la clase `CSVReader` [(documentación oficial)](https://opencsv.sourceforge.net/apidocs/com/opencsv/CSVReader.html).

1. Añade la dependencia de OpenCSV en tu proyecto (si usas Maven):

   ```xml
   <dependency>
       <groupId>com.opencsv</groupId>
       <artifactId>opencsv</artifactId>
       <version>5.7.1</version>
   </dependency>
   ```

2. Ejemplo de lectura:

   ```java
   import com.opencsv.CSVReader;
   import java.io.FileReader;
   import java.io.IOException;

   public class LeerCSV {
       public static void main(String[] args) {
           String rutaFichero = "datos.csv"; // Ruta del fichero CSV

           try (CSVReader reader = new CSVReader(new FileReader(rutaFichero))) {
               String[] linea;
               while ((linea = reader.readNext()) != null) {
                   for (String valor : linea) {
                       System.out.print(valor + " ");
                   }
                   System.out.println();
               }
           } catch (IOException e) {
               System.err.println("Error al leer el fichero CSV: " + e.getMessage());
           }
       }
   }
   ```

En este ejemplo, utilizamos un bloque `try-with-resources` para asegurarnos de que el flujo de datos se cierre automáticamente al finalizar la lectura. Luego, leemos cada línea del fichero CSV y mostramos los valores en la consola. Como vemos, `CSVReader` recibe por parámetro un objeto de tipo `FileReader` para leer el fichero CSV.

###### Métodos útiles de CSVReader

- `readNext()`: Lee la siguiente línea del fichero CSV y la devuelve como un array de cadenas.
- `readAll()`: Lee todas las líneas del fichero CSV y las devuelve como una lista de arrays de cadenas.
- `skip(n)`: Salta `n` líneas del fichero CSV.
- `close()`: Cierra el flujo de datos.

##### Escritura de un fichero CSV con OpenCSV

Para escribir un fichero CSV con OpenCSV, se utiliza la clase `CSVWriter` [(documentación oficial)](https://opencsv.sourceforge.net/apidocs/com/opencsv/CSVWriter.html).

```java
import com.opencsv.CSVWriter;
import java.io.FileWriter;
import java.io.IOException;

public class EscribirCSV {
    public static void main(String[] args) {
        String rutaFichero = "salida.csv"; // Ruta del fichero CSV de salida

        try (CSVWriter writer = new CSVWriter(new FileWriter(rutaFichero))) {
            String[] cabecera = { "Nombre", "Edad", "Ciudad" };
            String[] fila1 = { "Juan", "25", "Madrid" };
            String[] fila2 = { "Ana", "30", "Barcelona" };

            writer.writeNext(cabecera);
            writer.writeNext(fila1);
            writer.writeNext(fila2);
            System.out.println("Datos escritos correctamente.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el fichero CSV: " + e.getMessage());
        }
    }
}
```

##### Ejemplo: procesado datos de empleados desde archivo csv

A continuación se presenta un ejemplo de programa en Java en el que se lee un archivo CSV con datos de empleados y se almacenan en una lista de objetos `Empleado`.

```java
import com.opencsv.CSVReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.*;

public class LeerEmpleadosCSV {
    public static void main(String[] args) {
        String archivo = "empleados.csv";
        List<Empleado> empleados = new ArrayList<>();

        try (CSVReader reader = new CSVReader(new FileReader(archivo))) {
            reader.skip(1); // Saltar cabecera
            String[] datos;
            while ((datos = reader.readNext()) != null) {
                empleados.add(new Empleado(
                        Integer.parseInt(datos[0]), 
                        datos[1], 
                        datos[2], 
                        Double.parseDouble(datos[3])
                ));
            }
        } catch (CsvValidationException | IOException e) {
            e.printStackTrace();
        }

        // Mostrar empleados
        empleados.forEach(System.out::println);
    }
}

// Clase Empleado
class Empleado {
    int id;
    String nombre, departamento;
    double salario;

    public Empleado(int id, String nombre, String departamento, double salario) {
        this.id = id;
        this.nombre = nombre;
        this.departamento = departamento;
        this.salario = salario;
    }

    @Override
    public String toString() {
        return id + " - " + nombre + " (" + departamento + ") - Salario: $" + salario;
    }
}
```

Como vemos, la clase CSVReader proporciona un método `readNext()` para leer la siguiente línea del archivo CSV, guardando cada uno de los valores en un array de cadenas. Además, se ha utilizado `reader.skip(1)` para saltar la cabecera del archivo. Tambien dispone de otros métodos como `readAll()` para leer todas las líneas del archivo CSV y devolverlas como una lista de arrays de cadenas.

### 4.2. Ficheros binarios

Los ficheros binarios contienen datos en formato binario, que pueden representar imágenes, vídeos, archivos comprimidos, etc. Para leer y escribir ficheros binarios en Java, se utilizan flujos de bytes como `FileInputStream` y `FileOutputStream`.

#### 4.2.1. Lectura de un fichero binario

Para leer un fichero binario, se utilizan clases como `FileInputStream` y `BufferedInputStream`. Estas clases permiten leer datos en formato binario.

- **`FileInputStream`**: Se utiliza para leer datos de un fichero binario (ver [documentación oficial](https://docs.oracle.com/javase/8/docs/api/java/io/FileInputStream.html)).
- **`BufferedInputStream`**: Se utiliza para mejorar el rendimiento al leer grandes volúmenes de datos de un fichero binario (ver [documentación oficial](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedInputStream.html)).

##### Ejemplo: Lectura de un fichero binario con `FileInputStream`

```java
import java.io.FileInputStream;
import java.io.IOException;

public class LeerFicheroBinario {
    public static void main(String[] args) {
        String rutaFichero = "archivo.bin"; // Ruta del fichero binario

        try (FileInputStream fis = new FileInputStream(rutaFichero)) {
            int byteLeido;
            while ((byteLeido = fis.read()) != -1) {
                System.out.print(byteLeido + " "); // Muestra cada byte leído
            }
        } catch (IOException e) {
            System.err.println("Error al leer el fichero: " + e.getMessage());
        }
    }
}
```

##### Ejemplo: Lectura de un fichero binario con `BufferedInputStream`

```java
import java.io.BufferedInputStream;
import java.io.FileInputStream;
import java.io.IOException;

public class LeerFicheroBinario {
    public static void main(String[] args) {
        String rutaFichero = "archivo.bin"; // Ruta del fichero binario

        try (BufferedInputStream bis = new BufferedInputStream(new FileInputStream(rutaFichero))) {
            int byteLeido;
            while ((byteLeido = bis.read()) != -1) {
                System.out.print(byteLeido + " "); // Muestra cada byte leído
            }
        } catch (IOException e) {
            System.err.println("Error al leer el fichero: " + e.getMessage());
        }
    }
}
```

El método `read()` de `FileInputStream` y `BufferedInputStream` devuelve un byte del fichero binario. Al llegar al final del fichero, devuelve `-1`.

##### ¿Cuándo utilizar `FileInputStream` o `BufferedInputStream`?

- **FileInputStream**
  - Se usa para leer datos directamente desde archivos
  - Lee byte por byte del sistema de archivos
  - No tiene buffer interno, por lo que cada llamada de lectura puede resultar en una operación de I/O del sistema

- **BufferedInputStream**
  - Es un wrapper que añade funcionalidad de buffering
  - No se conecta directamente con archivos, sino que envuelve otro InputStream
  - Mantiene un buffer interno (array de bytes) para reducir las llamadas al sistema subyacente
  - Mejora significativamente el rendimiento al reducir el número de operaciones de I/O

**Cuándo usar cada uno**:

- **Usa FileInputStream cuando:**
  - Necesitas la implementación más simple para leer de un archivo
  - Lo vas a envolver con otro stream (como BufferedInputStream)
  - Estás leyendo archivos muy pequeños donde el buffering no ofrece ventajas

- **Usa BufferedInputStream cuando:**
  - Quieres mejorar el rendimiento de lectura
  - Estás leyendo datos en pequeñas cantidades o frecuentemente
  - Necesitas las operaciones mark() y reset()

En la práctica, para la mayoría de aplicaciones, es recomendable usar BufferedInputStream envolviendo un FileInputStream para obtener mejor rendimiento.

#### 4.2.2. Escritura de un fichero binario

Para escribir en un fichero binario, se utilizan clases como `FileOutputStream` y `BufferedOutputStream`.

- **`FileOutputStream`**: Se utiliza para escribir datos en un fichero binario (ver [documentación oficial](https://docs.oracle.com/javase/8/docs/api/java/io/FileOutputStream.html)).
- **`BufferedOutputStream`**: Se utiliza para mejorar el rendimiento al escribir grandes volúmenes de datos en un fichero binario (ver [documentación oficial](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedOutputStream.html)).

##### Ejemplo: Escritura de datos binarios

```java
import java.io.FileOutputStream;
import java.io.IOException;

public class EscribirFicheroBinario {
    public static void main(String[] args) {
        String rutaFichero = "salida.bin"; // Ruta del fichero binario de salida
        byte[] datos = { 65, 66, 67, 68 }; // Datos binarios (A, B, C, D en ASCII)

        try (FileOutputStream fos = new FileOutputStream(rutaFichero)) {
            fos.write(datos); // Escribe los datos en el fichero
            System.out.println("Datos escritos correctamente.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el fichero: " + e.getMessage());
        }
    }
}
```

En el caso de BufferedOutputStream, es importante recordar que se debe llamar al método `flush()` o `close()` para asegurar que todos los datos en el buffer se escriban al archivo, especialmente si el programa puede terminar antes de que el buffer se llene.

```java
import java.io.BufferedOutputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class EscribirFicheroBinario {
    public static void main(String[] args) {
        String rutaFichero = "salida.bin"; // Ruta del fichero binario de salida
        byte[] datos = { 65, 66, 67, 68 }; // Datos binarios (A, B, C, D en ASCII)

        try (BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(rutaFichero))) {
            bos.write(datos); // Escribe los datos en el fichero
            bos.flush(); // Vacía el buffer
            System.out.println("Datos escritos correctamente.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el fichero: " + e.getMessage());
        }
    }
}
```

Las diferencias y criterio de elección entre una u otra opción son exactamente las mismas que las revisadas para `FileInputStream` y `BufferedInputStream`.

#### 4.2.3. Ejemplo: Copia de una imagen

```java
import java.io.*;

public class CopiarArchivoBinario {
    public static void main(String[] args) {
        // Rutas de ejemplo - ajusta estas rutas según tu sistema
        String archivoOrigen = "imagen_original.jpg";
        String archivoDestino = "imagen_copia.jpg";
        
        // Usando directamente FileInputStream/FileOutputStream (menos eficiente)
        copiarSinBuffer(archivoOrigen, archivoDestino + ".sin_buffer");
        
        // Usando BufferedInputStream/BufferedOutputStream (más eficiente)
        copiarConBuffer(archivoOrigen, archivoDestino + ".con_buffer");
        
        // Comparando rendimiento
        medirRendimiento(archivoOrigen, archivoDestino);
    }
    
    /**
     * Copia un archivo binario sin usar buffers.
     */
    public static void copiarSinBuffer(String origen, String destino) {
        try (FileInputStream fis = new FileInputStream(origen);
             FileOutputStream fos = new FileOutputStream(destino)) {
            
            int byteLeido;
            while ((byteLeido = fis.read()) != -1) {
                fos.write(byteLeido);
            }
            
            System.out.println("Archivo copiado sin buffer: " + destino);
            
        } catch (IOException e) {
            System.err.println("Error al copiar el archivo sin buffer: " + e.getMessage());
        }
    }
    
    /**
     * Copia un archivo binario usando buffers para mejorar el rendimiento.
     */
    public static void copiarConBuffer(String origen, String destino) {
        try (FileInputStream fis = new FileInputStream(origen);
             BufferedInputStream bis = new BufferedInputStream(fis, 8192); // Buffer de 8KB
             FileOutputStream fos = new FileOutputStream(destino);
             BufferedOutputStream bos = new BufferedOutputStream(fos, 8192)) { // Buffer de 8KB
            
            int byteLeido;
            while ((byteLeido = bis.read()) != -1) {
                bos.write(byteLeido);
            }
            
            System.out.println("Archivo copiado con buffer: " + destino);
            
        } catch (IOException e) {
            System.err.println("Error al copiar el archivo con buffer: " + e.getMessage());
        }
    }
    
    /**
     * Versión mejorada que utiliza un array de bytes para leer/escribir múltiples bytes a la vez.
     */
    public static void copiarConBufferYArray(String origen, String destino) {
        try (FileInputStream fis = new FileInputStream(origen);
             BufferedInputStream bis = new BufferedInputStream(fis, 8192);
             FileOutputStream fos = new FileOutputStream(destino);
             BufferedOutputStream bos = new BufferedOutputStream(fos, 8192)) {
            
            byte[] buffer = new byte[4096]; // Buffer de 4KB
            int bytesLeidos;
            
            while ((bytesLeidos = bis.read(buffer)) != -1) {
                bos.write(buffer, 0, bytesLeidos);
            }
            
            System.out.println("Archivo copiado con buffer y array: " + destino);
            
        } catch (IOException e) {
            System.err.println("Error al copiar el archivo: " + e.getMessage());
        }
    }
    
    /**
     * Mide y compara el rendimiento de los diferentes métodos de copia.
     */
    public static void medirRendimiento(String origen, String destino) {
        // Preparar archivos de destino para la prueba
        String destinoSinBuffer = destino + ".test1";
        String destinoConBuffer = destino + ".test2";
        String destinoOptimizado = destino + ".test3";
        
        System.out.println("\n===== COMPARACIÓN DE RENDIMIENTO =====");
        
        // Método 1: Sin buffer
        long inicioSinBuffer = System.currentTimeMillis();
        copiarSinBuffer(origen, destinoSinBuffer);
        long finSinBuffer = System.currentTimeMillis();
        System.out.println("Tiempo sin buffer: " + (finSinBuffer - inicioSinBuffer) + " ms");
        
        // Método 2: Con buffer, byte por byte
        long inicioConBuffer = System.currentTimeMillis();
        copiarConBuffer(origen, destinoConBuffer);
        long finConBuffer = System.currentTimeMillis();
        System.out.println("Tiempo con buffer (byte por byte): " + (finConBuffer - inicioConBuffer) + " ms");
        
        // Método 3: Con buffer y array de bytes (más eficiente)
        long inicioOptimizado = System.currentTimeMillis();
        copiarConBufferYArray(origen, destinoOptimizado);
        long finOptimizado = System.currentTimeMillis();
        System.out.println("Tiempo con buffer y array: " + (finOptimizado - inicioOptimizado) + " ms");
        
        // Limpiar archivos de prueba
        try {
            new File(destinoSinBuffer).delete();
            new File(destinoConBuffer).delete();
            new File(destinoOptimizado).delete();
        } catch (Exception e) {
            // Ignorar errores de limpieza
        }
    }
}
```

### 4.3. Ficheros de acceso aleatorio

Los ficheros de acceso aleatorio son aquellos que permiten acceder a cualquier posición del fichero de forma directa, sin tener que leer todo el fichero desde el principio.

La clase `RandomAccessFile` permite leer y escribir datos en cualquier posición de un archivo, a diferencia de los flujos secuenciales que solo permiten acceso lineal. Esto es útil cuando necesitamos acceder o modificar partes específicas de un archivo sin tener que leerlo completo.

Características principales:

- Permite posicionar el puntero de lectura/escritura en cualquier posición del archivo usando `seek()`
- Soporta lectura y escritura en el mismo objeto
- Trabaja a nivel de bytes, por lo que es ideal para archivos binarios
- Permite tanto lectura como escritura de tipos primitivos

Ejemplo básico de uso:

```java
import java.io.RandomAccessFile;
import java.io.IOException;

public class EjemploRandomAccessFile {
    public static void main(String[] args) {
        String rutaArchivo = "archivo.dat";
        
        try (RandomAccessFile raf = new RandomAccessFile(rutaArchivo, "rw")) {
            // Escribir datos en el archivo     
            raf.writeInt(100); // Escribir un entero
            raf.writeDouble(3.14159); // Escribir un double
            raf.writeUTF("Hola"); // Escribir una cadena
            
            // Leer datos desde el archivo
            raf.seek(0); // Posicionar el puntero al principio
            int entero = raf.readInt();
            double doble = raf.readDouble();
            String cadena = raf.readUTF();
            
            System.out.println("Entero: " + entero);
            System.out.println("Doble: " + doble);
            System.out.println("Cadena: " + cadena);
            
            // Escribir en una posición específica
            raf.seek(8); // Posicionar el puntero a la posición 8
            raf.writeUTF("Mundo");
            
            // Leer desde una posición específica
            raf.seek(8);
            String nuevoTexto = raf.readUTF();
            System.out.println("Nuevo texto: " + nuevoTexto);
            
        } catch (IOException e) {
            System.err.println("Error al trabajar con el archivo: " + e.getMessage());
        }
    }
}
```

En este ejemplo, se crea un archivo de acceso aleatorio llamado `archivo.dat` con el modo `rw` que permite lectura y escritura. Se escriben varios tipos de datos en diferentes posiciones del archivo y se leen de nuevo para verificar que los datos se han escrito y leído correctamente.

### 4.4. Ficheros ZIP

Java proporciona clases como `ZipOutputStream` y `ZipInputStream` para trabajar con archivos comprimidos en formato ZIP.

#### 4.4.1. Compresión de archivos

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.zip.ZipEntry;
import java.util.zip.ZipOutputStream;

public class ComprimirArchivos {
    public static void main(String[] args) {
        String[] ficheros = { "archivo1.txt", "archivo2.txt" }; // Ficheros a comprimir
        String rutaZip = "archivos.zip"; // Ruta del archivo ZIP de salida

        // Si no existen los archivos, los creamos
        for (String fichero : ficheros) {
            File archivo = new File(fichero);
            if (!archivo.exists()) {
                try (BufferedWriter bw = new BufferedWriter(new FileWriter(archivo))) {
                    bw.write("Contenido del archivo " + fichero);
                    System.out.println("Archivo " + fichero + " creado correctamente.");
                } catch (IOException e) {
                    System.err.println("Error al crear el archivo " + fichero + ": " + e.getMessage());
                }
            }
        }

        try (ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(rutaZip))) {
            for (String fichero : ficheros) {
                try (FileInputStream fis = new FileInputStream(fichero)) {
                    ZipEntry entrada = new ZipEntry(fichero);
                    zos.putNextEntry(entrada);

                    byte[] buffer = new byte[1024];
                    int longitud;
                    while ((longitud = fis.read(buffer)) > 0) {
                        zos.write(buffer, 0, longitud);
                    }
                } catch (IOException e) {
                    System.err.println("Error al manejar los archivos a comprimir: " + e.getMessage());
                }
            }
            System.out.println("Archivos comprimidos correctamente.");
        } catch (IOException e) {
            System.err.println("Error al comprimir los archivos: " + e.getMessage());
        }
}
```

#### 4.4.2. Descompresión de archivos

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;

public class DescomprimirArchivos {
    public static void main(String[] args) {
        String rutaZip = "archivos.zip"; // Ruta del archivo ZIP
        String rutaDestino = "destino/"; // Directorio de destino

        File directorio = new File(rutaDestino);
        if (!directorio.exists()) {
            if (directorio.mkdir()) {
                System.out.println("Directorio creado correctamente.");
            } else {
                System.out.println("No se pudo crear el directorio.");
            }
        }

        try (ZipInputStream zis = new ZipInputStream(new FileInputStream(rutaZip))) {
            ZipEntry entrada;
            while ((entrada = zis.getNextEntry()) != null) {
                FileOutputStream fos = new FileOutputStream(rutaDestino + entrada.getName());
                byte[] buffer = new byte[1024];
                int longitud;
                while ((longitud = zis.read(buffer)) > 0) {
                    fos.write(buffer, 0, longitud);
                }
                fos.close();
                zis.closeEntry();
            }
            System.out.println("Archivos descomprimidos correctamente.");
        } catch (IOException e) {
            System.err.println("Error al descomprimir los archivos: " + e.getMessage());
        }
    }
}
```

## 5. Flujos de consola

En Java, la entrada y salida estándar se manejan a través de flujos de datos especiales: `System.in` y `System.out`. Estos flujos permiten leer datos de la consola (entrada estándar) y escribir datos en la consola (salida estándar).

Hemos trabajado con ellos desde el principio del curso, para poder interactuar con nuestros programas, proporcionando datos y recibiéndolos.

A continuación, vamos a profundizar en cómo trabajar con estos flujos y cómo gestionar la entrada y salida de datos en la consola.

### 5.1. Flujos de entrada estándar

Los flujos de entrada estándar son aquellos que permiten leer datos de la consola.

```java
import java.util.Scanner;

public class EjemploFlujoEntrada {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Introduce tu nombre: ");
        String nombre = scanner.nextLine();

        System.out.println("Introduce tu edad: ");
        int edad = scanner.nextInt();

        System.out.println("Introduce tu altura: ");
        double altura = scanner.nextDouble();

        System.out.println("Nombre: " + nombre);
        System.out.println("Edad: " + edad);
        System.out.println("Altura: " + altura);

        scanner.close();
    }
}
```

Podemos leer diferentes tipos de datos de la consola, como `String`, `int`, `double`, `float`, `boolean`, etc.

- `nextLine()`: Lee una línea completa de texto.
- `nextInt()`: Lee un entero.
- `nextDouble()`: Lee un double.
- `nextFloat()`: Lee un float.
- `nextBoolean()`: Lee un boolean.
- `next()`: Lee un String.
- `nextByte()`: Lee un byte.
- `nextShort()`: Lee un short.
- `nextLong()`: Lee un long.

### 5.2. Flujos de salida estándar

Los flujos de salida estándar son aquellos que permiten escribir datos en la consola.

Podemos escribir diferentes tipos de datos en la consola, como `String`, `int`, `double`, `float`, `boolean`, etc.

- `println()`: Escribe una línea completa de texto.
- `print()`: Escribe un String.
- `printf()`: Escribe un String con formato.
- `format()`: Escribe un String con formato.

```java
import java.io.PrintStream;

public class EjemploFlujoSalida {
    public static void main(String[] args) {
        PrintStream out = System.out;

        out.println("Hola");
        out.printf("Hola %s", "Mundo");
        out.format("Hola %s", "Mundo");
    }
}
```

#### 5.2.1. Formato de salida

Podemos formatear la salida de datos con el método `printf()`.

```java
import java.io.PrintStream;

public class EjemploFlujoSalida {
    public static void main(String[] args) {
        PrintStream out = System.out;

        out.printf("Hola %s", "Mundo");
        out.printf("Hola %d", 10);
        out.printf("Hola %.2f", 10.5);
        out.printf("Hola %b", true);
        out.printf("Hola %c", 'a');
    }
}
```

- `%s`: String.
- `%d`: int.
- `%.2f`: double. Podemos indicar el numero de cifras decimales y enteras
- `%10.2f`: double con 2 decimales y 10 caracteres de ancho. Esto significa que el numero ocupara 10 caracteres, 2 de ellos para los decimales y el resto para los enteros.
- `%b`: boolean.
- `%c`: char.

## 6. Flujos de `String`

En Java, los flujos de `String` permiten leer y escribir datos **en memoria** en lugar de interactuar con archivos físicos. Se utilizan principalmente cuando se necesita procesar cadenas de texto sin crear archivos temporales. Los principales flujos de `String` en Java son **`StringReader`** y **`StringWriter`**.

### 6.1. StringReader

`StringReader` es una clase que permite leer caracteres desde un `String` como si fuera un flujo de entrada.

```java
import java.io.StringReader;
import java.io.IOException;

public class StringReaderExample {
    public static void main(String[] args) {
        String data = "Este es un ejemplo de StringReader";
        try (StringReader stringReader = new StringReader(data)) {
            int caracter;
            while ((caracter = stringReader.read()) != -1) {
                System.out.print((char) caracter);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Este código crea un `StringReader` a partir de una cadena y la lee carácter por carácter hasta el final del flujo.

### 6.2. StringWriter

`StringWriter` es una clase que permite escribir caracteres en un `StringBuffer` interno en memoria.

```java
import java.io.StringWriter;
import java.io.IOException;

public class StringWriterExample {
    public static void main(String[] args) {
        try (StringWriter stringWriter = new StringWriter()) {
            stringWriter.write("Ejemplo de StringWriter\n");
            stringWriter.write("Escribiendo en memoria en lugar de un archivo\n");
            
            System.out.println(stringWriter.toString());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Este código utiliza `StringWriter` para almacenar texto en memoria y luego imprimirlo.

### 6.3. Uso de BufferedReader con StringReader

`BufferedReader` se puede usar con `StringReader` para leer líneas completas en lugar de caracteres individuales.

```java
import java.io.StringReader;
import java.io.BufferedReader;
import java.io.IOException;

public class BufferedReaderStringReaderExample {
    public static void main(String[] args) {
        String data = "Línea 1\nLínea 2\nLínea 3";
        try (BufferedReader bufferedReader = new BufferedReader(new StringReader(data))) {
            String linea;
            while ((linea = bufferedReader.readLine()) != null) {
                System.out.println(linea);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Este enfoque es útil cuando se procesan múltiples líneas de texto.

### 6.4. Uso práctico de `StringReader`

Un uso práctico de `StringReader` es el procesamiento de datos en formato CSV o JSON obtenidos de una API o base de datos, sin necesidad de escribirlos en un archivo temporal.  

```java
import java.io.StringReader;
import java.io.BufferedReader;
import java.io.IOException;

public class JsonProcessingExample {
    public static void main(String[] args) {
        String jsonData = """
                {
                    "nombre": "Juan",
                    "edad": 30,
                    "ciudad": "Madrid"
                }
                """;

        try (BufferedReader bufferedReader = new BufferedReader(new StringReader(jsonData))) {
            String linea;
            while ((linea = bufferedReader.readLine()) != null) {
                if (linea.contains("nombre") || linea.contains("edad") || linea.contains("ciudad")) {
                    System.out.println(linea.trim());
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

- Se simula una respuesta JSON en un `String`.
- `StringReader` y `BufferedReader` permiten procesar el texto línea por línea sin escribirlo en un archivo.
- Se filtran las líneas con información clave.  

Este enfoque es útil para manejar respuestas de APIs o datos en memoria sin depender de almacenamiento en disco.

## 7. Flujos tokenizados

Los flujos tokenizados permiten leer datos de un archivo o flujo de entrada dividiéndolos en tokens (unidades lógicas de información) según delimitadores específicos. Java proporciona la clase `StreamTokenizer` para este propósito.

Se puede utilizar tanto con flujos de fiche

### 7.1. La clase `StreamTokenizer`

La clase `StreamTokenizer` lee un flujo de entrada y lo divide en "tokens", que pueden ser:

- Palabras
- Números
- Caracteres individuales
- Cadenas entre comillas

Características principales:

- Ignora espacios en blanco y saltos de línea por defecto
- Reconoce automáticamente números y palabras
- Permite configurar qué caracteres se consideran delimitadores
- Mantiene un contador de líneas

Ejemplo básico de uso:

```java
import java.io.StreamTokenizer;
import java.io.StringReader;

public class EjemploStreamTokenizer {
    public static void main(String[] args) {
        String texto = "Hola mundo, esto es una prueba.";
        StringReader reader = new StringReader(texto);
        StreamTokenizer tokenizer = new StreamTokenizer(reader);

        try {
            while (tokenizer.nextToken() != StreamTokenizer.TT_EOF) {
                if (tokenizer.ttype == StreamTokenizer.TT_WORD) {
                    System.out.println("Palabra: " + tokenizer.sval);
                } else if (tokenizer.ttype == StreamTokenizer.TT_NUMBER) {
                    System.out.println("Número: " + tokenizer.nval);
                }       
            }
        } catch (IOException e) {
            System.err.println("Error al tokenizar el texto: " + e.getMessage());
        }
    }
}
```

Atributos de `StreamTokenizer`:

- `ttype`: Tipo de token.
- `nval`: Valor numérico del token.
- `sval`: Valor de cadena del token.

Métodos de `StreamTokenizer`:

- `nextToken()`: Lee el siguiente token.
- `resetSyntax()`: Restablece la configuración a su estado inicial.
- `wordChars(int low, int high)`: Define el rango de caracteres que se consideran parte de una palabra.
- `whitespaceChars(int low, int high)`: Define el rango de caracteres que se consideran espacios en blanco.

Configuración avanzada de `StreamTokenizer`:

```java
import java.io.StreamTokenizer;
import java.io.StringReader;

public class EjemploStreamTokenizer {
    public static void main(String[] args) {
        String texto = "Hola mundo, esto es una prueba.";
        StringReader reader = new StringReader(texto);
        StreamTokenizer tokenizer = new StreamTokenizer(reader);

        try {
            while (tokenizer.nextToken() != StreamTokenizer.TT_EOF) {
                if (tokenizer.ttype == StreamTokenizer.TT_WORD) {
                    System.out.println("Palabra: " + tokenizer.sval);
                } else if (tokenizer.ttype == StreamTokenizer.TT_NUMBER) {
                    System.out.println("Número: " + tokenizer.nval);
                }       
            }
        } catch (IOException e) {
            System.err.println("Error al tokenizar el texto: " + e.getMessage());
        }
    }
}
```

En este ejemplo, se configura el `StreamTokenizer` para reconocer palabras en inglés y números.

#### 7.1.1. Configuración de `StreamTokenizer`

La clase `StreamTokenizer` ofrece varias opciones de configuración para personalizar cómo se analizan los tokens. Estas son algunas de las configuraciones más importantes:

1. **Configuración de caracteres**:
   - `wordChars(int low, int high)`: Define el rango de caracteres que se consideran parte de una palabra.
   - `whitespaceChars(int low, int high)`: Define el rango de caracteres que se consideran espacios en blanco.
   - `ordinaryChar(int ch)`: Define un carácter como ordinario (será devuelto como un token individual).
   - `ordinaryChars(int low, int high)`: Define un rango de caracteres como ordinarios.
   - `commentChar(int ch)`: Define un carácter que inicia un comentario de línea.
   - `quoteChar(int ch)`: Define un carácter como delimitador de cadenas.

2. **Configuración de números**:
   - `parseNumbers()`: Habilita el reconocimiento de números.
   - `slashStarComments(boolean flag)`: Habilita o deshabilita los comentarios estilo C (`/* ... */`).
   - `slashSlashComments(boolean flag)`: Habilita o deshabilita los comentarios estilo C++ (`// ...`).

3. **Reseteo de configuración**:
   - `resetSyntax()`: Restablece toda la configuración a su estado inicial.

Ejemplo de configuración avanzada:

```java
import java.io.StreamTokenizer;
import java.io.StringReader;

public class EjemploStreamTokenizer {
    public static void main(String[] args) {
        String texto = "Hola mundo, esto es una prueba.";
        StringReader reader = new StringReader(texto);
        StreamTokenizer tokenizer = new StreamTokenizer(reader);

        List<String> palabras = new ArrayList<>();
        List<Double> numeros = new ArrayList<>();

        tokenizer = new StreamTokenizer(reader);
        tokenizer.resetSyntax();
        tokenizer.wordChars('a', 'z');
        tokenizer.wordChars('A', 'Z');
        tokenizer.wordChars('á', 'ú');
        tokenizer.wordChars('Á', 'Ú');
        tokenizer.whitespaceChars(0, ' ');
        tokenizer.ordinaryChar('.');
        tokenizer.ordinaryChar('¡');
        tokenizer.ordinaryChar('!');
        tokenizer.commentChar('/');
        //leer numeros
        tokenizer.parseNumbers();

        try {
            while (tokenizer.nextToken() != StreamTokenizer.TT_EOF) {
                if (tokenizer.ttype == StreamTokenizer.TT_WORD) {
                    System.out.println("Palabra: " + tokenizer.sval);
                    palabras.add(tokenizer.sval);
                } else if (tokenizer.ttype == StreamTokenizer.TT_NUMBER) {
                    System.out.println("Número: " + tokenizer.nval);
                    numeros.add(tokenizer.nval);
                }
            }
        } catch (IOException e) {
            System.err.println("Error al tokenizar el texto: " + e.getMessage());
        }

        System.out.println("Palabras: " + palabras);
        System.out.println("Números: " + numeros);
    }
}
```

En este ejemplo, se configura el `StreamTokenizer` para reconocer palabras y números, controlando los caracteres delimitadores del español.

## 8. Flujos orientados a objetos

En Java, los flujos orientados a objetos permiten leer y escribir objetos de forma sencilla y eficiente. Estos flujos se utilizan para **serializar** y **deserializar** objetos, es decir, convertir objetos en secuencias de bytes y viceversa.

Los flujos orientados a objetos se basan en los flujos de bytes (`ObjectInputStream` y `ObjectOutputStream`) y permiten trabajar con objetos de forma transparente, sin tener que preocuparse por la representación interna de los datos.

En esta sección, veremos cómo utilizar los flujos orientados a objetos para leer y escribir objetos en Java.

### 8.1. Serialización de objetos

Para serializar un objeto en Java, este debe implementar la interfaz `Serializable`. Esta interfaz no tiene métodos y actúa como un marcador para indicar que un objeto puede ser convertido en una secuencia de bytes.

Una vez hemos definido una clase como Serializable, podemos utilizar `ObjectOutputStream` para escribir el objeto en un flujo de salida. Este flujo se encarga de convertir el objeto en una secuencia de bytes que puede ser almacenada en un archivo o transmitida a través de una red.

```java
import java.io.*;

class Persona implements Serializable {
    private static final long serialVersionUID = 1L;
    private String nombre;
    private int edad;
    
    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
    
    @Override
    public String toString() {
        return "Persona{nombre='" + nombre + "', edad=" + edad + "}";
    }
}

public class SerializacionEjemplo {
    public static void main(String[] args) {
        Persona persona = new Persona("Juan", 30);
        
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("persona.dat"))) {
            oos.writeObject(persona);
            System.out.println("Objeto serializado correctamente.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Este código serializa un objeto de la clase `Persona` en un archivo binario llamado `persona.dat`.

### 8.2. Deserialización de objetos

Para deserializar un objeto, se utiliza la clase `ObjectInputStream`.

```java
import java.io.*;

public class DeserializacionEjemplo {
    public static void main(String[] args) {
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("persona.dat"))) {
            Persona persona = (Persona) ois.readObject();
            System.out.println("Objeto deserializado: " + persona);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

Este programa lee el archivo `persona.dat`, reconstruye el objeto `Persona` y lo imprime en consola.

### 8.3. Consideraciones sobre la serialización

El uso de `Serializable` en Java tiene varios aspectos importantes a conocer para aplicarlo correctamente.

#### 8.3.1. Identificador de versión (`serialVersionUID`)

Cada clase `Serializable` debe definir un `serialVersionUID` para garantizar la compatibilidad entre versiones al deserializar objetos.  

```java
private static final long serialVersionUID = 1L;
```  

Si no se define, Java generará uno automáticamente, lo que puede causar problemas si la clase cambia.  

#### 8.3.2. Compatibilidad entre versiones

Si modificas una clase serializable (por ejemplo, agregas o eliminas atributos), es posible que los objetos guardados previamente no sean compatibles con la nueva versión. Definir un `serialVersionUID` ayuda a manejar estos cambios.  

#### 8.3.3. Exclusión de atributos (`transient`)

Si un atributo no debe ser serializado (por ejemplo, datos sensibles o referencias a objetos no serializables), puedes marcarlo con `transient`:  

```java
private transient String password;
```  

#### 8.3.4. Control personalizado con `writeObject` y `readObject`

Cuando una clase implementa Serializable, Java proporciona una forma estándar de serializar los objetos de esa clase, pero también es posible personalizar la serialización mediante *override* de los métodos `writeObject` y `readObject`. Esto permite realizar operaciones adicionales durante la serialización y deserialización, como cifrado o validación de datos:  

```java
private void writeObject(ObjectOutputStream oos) throws IOException {
    oos.defaultWriteObject();
    oos.writeObject(encriptar(password));
}

private void readObject(ObjectInputStream ois) throws IOException, ClassNotFoundException {
    ois.defaultReadObject();
    password = desencriptar((String) ois.readObject());
}
```

#### 8.3.5. Serialización y herencia

Si una clase padre es serializable, sus subclases también lo son. Sin embargo, si la subclase no es serializable, se lanzará una excepción al intentar serializarla. Para evitar esto, asegúrate de que todas las clases en la jerarquía sean serializables o marca los atributos no serializables como `transient`.  

```java
public class Usuario extends Persona {
    private String password;
    
    public Usuario(String nombre, int edad, String password) {
        super(nombre, edad);
        this.password = password;
    }
}
```

En este caso, si `Persona` es serializable, `Usuario` también lo será. Si `password` no es serializable, debes marcarlo como `transient`.

```java
public class Usuario extends Persona {
    private transient String password;
    
    public Usuario(String nombre, int edad, String password) {
        super(nombre, edad);
        this.password = password;
    }
}
```

#### 8.3.6. Serialización de objetos en colecciones

Si una colección contiene objetos serializables, la colección en sí debe ser serializable:  

```java
class Empleado implements Serializable {

  private Long id;
  private String firstName;
  private String lastName;
}

...

ArrayList<Empleado> empleados = new ArrayList<>();

empleados.add(new Empleado(1L, "Alberto", "Díaz"));
empleados.add(new Empleado(2L, "Julia", "Ruipérez"));

try (FileOutputStream fos = new FileOutputStream("employeeData");
    ObjectOutputStream oos = new ObjectOutputStream(fos);) {

  oos.writeObject(empleados);

} catch (FileNotFoundException e) {
  log.error("File not found : ", e);
  throw new RuntimeException(e);
} catch (IOException ioe) {
  log.error("Error while writing data : ", ioe);
  ioe.printStackTrace();
}
```

Como `Empleado` implementa `Serializable`, se pueden serializar listas de Empleados sin problemas. 

#### 8.3.7. Referencias a objetos no serializables

Si un objeto serializable contiene referencias a objetos no serializables, lanzará una excepción `NotSerializableException` a menos que las marquemos como `transient` o las hagamos serializables.

#### 8.3.8. Interfaces relacionadas (`Externalizable`)

La interfaz `Externalizable` proporciona mayor control sobre la serialización, ya que obliga a implementar los métodos `writeExternal` y `readExternal`. Es más eficiente pero requiere más trabajo manual.  

```java
public class Persona implements Externalizable {
    private String nombre;
    
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeUTF(nombre);
    }

    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
        nombre = in.readUTF();
    }
}
```  

### 8.4. ObjectInputStream y ObjectOutputStream

Como hemos visto anteriormente, `ObjectInputStream` y `ObjectOutputStream` son las clases que permiten la serialización y deserialización de objetos en Java. Estas clases son parte del paquete `java.io` y se utilizan para leer y escribir objetos en flujos de entrada y salida. El método `writeObject()` de `ObjectOutputStream` se utiliza para serializar un objeto, mientras que el método `readObject()` de `ObjectInputStream` se utiliza para deserializarlo. Estos métodos manejan automáticamente la conversión de objetos a bytes y viceversa, lo que facilita el proceso de almacenamiento y recuperación de objetos en Java.

Los métodos `writeObject()` y `readObject()` son los métodos principales utilizados para serializar y deserializar objetos en Java. `ObjectInputStream` y `ObjectOutputStream` tienen otros métodos, que puedes consultar en la [documentación oficial de Java](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/io/ObjectOutputStream.html).

Hay que recordar, además, la importancia de cerrar cualquier flujo abierto para liberar recursos del sistema. Esto se puede hacer utilizando bloques `try-with-resources` (cierre automático) o cerrando manualmente los flujos en un bloque `finally` mediante `close()`. En el caso de `ObjectInputStream` y `ObjectOutputStream`, el cierre de los flujos también cierra el flujo subyacente (por ejemplo, un `FileOutputStream` o un `Socket`).

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;

import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;

// ejemplo de uso de close

public class EjemploFlujos {
    public static void main(String[] args) {
        String rutaArchivo = "persona.dat";
        
        // Serializar un objeto
        Persona persona = new Persona("Juan", 30);
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(rutaArchivo))) {
            oos.writeObject(persona);
            System.out.println("Objeto serializado correctamente.");
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // Deserializar un objeto. Cierre manual en finally
        ObjectInputStream ois = null;
        try {
            ois = new ObjectInputStream(new FileInputStream(rutaArchivo));
            Persona personaDeserializada = (Persona) ois.readObject();
            System.out.println("Objeto deserializado: " + personaDeserializada);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (ois != null) {
                try {
                    ois.close(); // Cierre manual del flujo
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

Lo recomendable es utilizar `try-with-resources` para el cierre automático de los flujos, ya que es más limpio y evita errores de cierre manual.

Por último, mencionar la existencia del método `flush()`. Este método se utiliza para vaciar el buffer de salida, asegurando que todos los datos pendientes se escriban en el flujo subyacente. Es útil cuando se trabaja con flujos de salida que utilizan buffers internos, como `BufferedOutputStream` o `ObjectOutputStream`. Al llamar a `flush()`, garantizamos que todos los datos se envíen al destino antes de cerrar el flujo o continuar con otras operaciones. Sin embargo, en la mayoría de los casos, no es necesario llamar a `flush()` explícitamente, ya que el cierre del flujo lo hace automáticamente.

## 9. Procesamiento de JSON en archivos

JSON (JavaScript Object Notation) es un formato de datos ligero y estructurado, ampliamente utilizado para el intercambio de información entre aplicaciones. En Java, existen diversas bibliotecas para trabajar con JSON, como **Jackson** y **Gson**. Esta sección se enfocará en el procesamiento de archivos JSON utilizando estas herramientas.

### 9.1. Lectura de un archivo JSON en Java

Para leer un archivo JSON y convertirlo en un objeto Java, utilizaremos la biblioteca **Jackson**. Es necesario añadir la dependencia de Jackson en el proyecto (si usas Maven):

   ```xml
   ...
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.13.4.2</version>
    </dependency>
   ...
   ```

El siguiente ejemplo muestra cómo leer un archivo JSON y mapear su contenido a una clase Java.

#### 9.1.1. Ejemplo: lectura de un archivo JSON con Jackson

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import java.io.File;
import java.io.IOException;

class Usuario {
    private String nombre;
    private int edad;
    private String email;
    
    // Getters y setters
    public String getNombre() { return nombre; }
    public void setNombre(String nombre) { this.nombre = nombre; }
    public int getEdad() { return edad; }
    public void setEdad(int edad) { this.edad = edad; }
    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }
}

public class LeerJson {
    public static void main(String[] args) {
        ObjectMapper objectMapper = new ObjectMapper();
        try {
            Usuario usuario = objectMapper.readValue(new File("usuario.json"), Usuario.class);
            System.out.println("Nombre: " + usuario.getNombre());
            System.out.println("Edad: " + usuario.getEdad());
            System.out.println("Email: " + usuario.getEmail());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Si el archivo `usuario.json` contiene lo siguiente:

```json
{
    "nombre": "Juan Pérez",
    "edad": 30,
    "email": "juan@example.com"
}
```

El programa imprimirá la información del usuario en la consola.

### 9.2. Escritura de un archivo JSON en Java

Para guardar un objeto Java en un archivo JSON, podemos usar **Jackson** para serializar el objeto y escribirlo en un archivo.

#### 9.2.1. Ejemplo: escritura de un objeto Java en JSON

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import java.io.File;
import java.io.IOException;

public class EscribirJson {
    public static void main(String[] args) {
        Usuario usuario = new Usuario();
        usuario.setNombre("María López");
        usuario.setEdad(28);
        usuario.setEmail("maria@example.com");
        
        ObjectMapper objectMapper = new ObjectMapper();
        try {
            objectMapper.writeValue(new File("nuevo_usuario.json"), usuario);
            System.out.println("Archivo JSON generado correctamente.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Este código generará un archivo `nuevo_usuario.json` con el siguiente contenido:

```json
{
    "nombre": "María López",
    "edad": 28,
    "email": "maria@example.com"
}
```

### 9.3. Procesamiento de JSON como flujo de datos

En lugar de cargar todo el JSON en memoria, podemos procesarlo como un flujo, útil para manejar archivos grandes.

#### 9.3.1. Ejemplo: lectura de un JSON línea por línea

```java
import com.fasterxml.jackson.core.JsonFactory;
import com.fasterxml.jackson.core.JsonParser;
import com.fasterxml.jackson.core.JsonToken;
import java.io.File;
import java.io.IOException;

public class StreamingJson {
    public static void main(String[] args) {
        JsonFactory factory = new JsonFactory();
        try (JsonParser parser = factory.createParser(new File("usuarios.json"))) {
            while (!parser.isClosed()) {
                JsonToken token = parser.nextToken();
                if (token == JsonToken.FIELD_NAME) {
                    String fieldName = parser.getCurrentName();
                    parser.nextToken(); // Mover al valor
                    System.out.println(fieldName + ": " + parser.getText());
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Este método permite leer archivos JSON grandes sin cargarlos completamente en memoria.

### 9.4. Manejo de archivos JSON con colección de datos

Muchas veces, los archivos JSON contienen colecciones de objetos en lugar de una única entidad. Para manejar esto en Java, se pueden utilizar listas (`List<T>`) junto con `Jackson`.

#### 9.4.1. Escritura de una lista de objetos en JSON

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import java.io.File;
import java.io.IOException;
import java.util.Arrays;
import java.util.List;

public class JsonListaEscritura {
    public static void main(String[] args) {
        ObjectMapper objectMapper = new ObjectMapper();
        List<Usuario> usuarios = Arrays.asList(
            new Usuario("Juan", 30),
            new Usuario("Ana", 25),
            new Usuario("Carlos", 35)
        );
        try {
            objectMapper.writeValue(new File("usuarios.json"), usuarios);
            System.out.println("Lista de usuarios guardada en JSON");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### 9.4.2. Lectura de una lista de objetos desde JSON

```java
import com.fasterxml.jackson.core.type.TypeReference;
import com.fasterxml.jackson.databind.ObjectMapper;
import java.io.File;
import java.io.IOException;
import java.util.List;

public class JsonListaLectura {
    public static void main(String[] args) {
        ObjectMapper objectMapper = new ObjectMapper();
        try {
            List<Usuario> usuarios = objectMapper.readValue(new File("usuarios.json"), new TypeReference<List<Usuario>>() {});
            for (Usuario usuario : usuarios) {
                System.out.println("Nombre: " + usuario.nombre + ", Edad: " + usuario.edad);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
