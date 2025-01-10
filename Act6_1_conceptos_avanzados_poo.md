# Actividad 6.1: Proyecto Gestor de Bibliotecas. Relaciones entre Clases, Herencia e Interfaces

## Introducción

En esta práctica, extenderás la funcionalidad del proyecto de la biblioteca introduciendo jerarquías de clases con herencia, interfaces y relaciones avanzadas entre clases. Sustituiremos la clase `Libro` por una clase más general, `Publicacion`, y crearemos diferentes tipos de publicaciones. Además, aplicaremos encapsulamiento, validaciones y un diseño orientado a interfaces para mejorar la modularidad del proyecto.

## Relaciones entre Clases

### Herencia

1. Crea una clase abstracta `Publicacion`, que será la clase base para todo tipo de publicaciones. Esta clase tendrá:  
   * **Atributos**:  
     * `titulo` (String)  
     * `autor` (String)  
     * `anioPublicacion` (int)  
   * **Métodos**:  
     * `mostrarInfo()` (abstracto): Método que será implementado por las subclases.  
     * Métodos para la **validación** de atributos:

        ```java
        public static void validarTitulo(String titulo) { ... }
        ```

     * Getters y setters con **validaciones**.
2. Crea las siguientes subclases:  
   * **`Libro`** (esta clase ya existe, pero tendrás que modificarla para que herede de `Publicacion`):  
     * Atributos adicionales:  
       * `ISBN` (String)  
       * `numeroPaginas` (int)  
     * Implementa mostrarInfo() para mostrar toda la información del libro.
     * Métodos para la validación de atributos.
     * Getters y setters con validaciones.  
   * **`Revista`**:  
     * Atributos adicionales:  
       * `numeroEdicion` (int)  
       * `mesPublicacion` (enum Mes, que tendrás que crear)  
       * `categoría` (enum `CategoriaRevista`, que tendrás que crear; añade las categorías que creas convenientes: Prensa Rosa, Economía, Motor, Tecnología, Videojuegos...)  
       * `ISSN` (String)
        _Nota: busca el significado del ISSN y su formato adecuado._
     * Implementa `mostrarInfo()` para mostrar toda la información de la revista.  
     * Métodos para la **validación** de atributos.
     * Getters y setters con **validaciones**.
   * **`Audiolibro`**:  
     * Atributos adicionales:  
       * `duracion` (double): Duración en segundos.  
       * `narrador` (String)
       * `formatoAudio`(enum FormatoAudio, que tendrás que crear; añade algunas categorías: .mp3, .wav, .aac, .aa, ...)
       * `idioma`(String)
     * Implementa `mostrarInfo()`, Métodos para la **validación** de atributos y getters y setters con **validaciones**.

### Interfaces

1. Crea una interfaz `Prestable`:
   1. Estas interfaz debe contar con los métodos:  
      * `prestar()`  
      * `devolver()`  
      * `isPrestado()`: Devuelve un boolean indicando si la publicación está prestada.  
   2. Haz que **`Libro`** implemente `Prestable`.  
         * Actualiza la clase para llevar un estado interno (`prestado`) que indique si el libro está prestado o disponible. Es decir, añade un atributo booleano donde se almacene si el Libro está prestado o no.
         * Añade también dos atributos de tipo `LocalDate` para registrar la fecha de préstamo y la de devolución, teniendo en cuenta que cuando se invoque el método `prestar()`, deberá registrarse la fecha actual como fecha de préstamo, y la fecha 14 días posterior a la actual como fecha de devolución. Cuando se invoque a `devolver()`, ambas fechas se pondran a ``null`.
2. Añade una nueva interfaz `Multimedia` para publicaciones digitales o audiovisuales.  
     1. Métodos:  
        * `descargar()`  
        * `obtenerFormato()` (String)  
     2. Haz que **`Audiolibro`** implemente esta interfaz.

### Encapsulamiento

Refactoriza todas las clases para:

* Hacer que los atributos sean **privados**.  
* Implementar **getters** y **setters** con validaciones:  
  * Validar que el título y el autor no estén vacíos.  
  * Validar que el año de publicación no sea mayor al año actual.  
  * Validar que valores como `ISBN`, `numeroPaginas` o `duracion` sean válidos (no vacíos o positivos).
  * Haz uso de las **Excepciones personalizadas** creadas en la UD anterior para implementar dichas validaciones e implementa las nuevas excepciones que consideres necesarias.

## Modificaciones en la Clase Biblioteca

* Sustituye el **array** de `Libro` por un **array** de `Publicacion` (no utilices colecciones como `List`, `ArrayList`...).
* Ajusta los métodos existentes (`agregarLibro`, `listarLibros`, etc.) para que funcionen con `Publicacion`. Cambia los nombres de los métodos para reflejar el cambio general a publicaciones.
* Agrega validaciones para asegurarte de que no se supere la capacidad del array.
* Agrega métodos para listar tipos específicos de Publicaciones: `listarLibros`, `listarRevistas`... Haz uso del operador `instanceof` si es necesario.
* Agrega métodos para buscar tipos específicos de Publicaciones: `buscarLibro`, `buscarRevista`... Haz uso del operador `instanceof` si es necesario.
* Agrega los métodos necesarios para gestionar los préstamos y devoluciones de publicaciones prestables.
* Agrega los metodos necesarios para gestionar las publicaciones multimedia

Recuerda que, desde el menú principal, no se podrá instanciar ninguna otra clase que no sea la `Biblioteca`.

## Modificación del Menú Principal

Amplía el menú con opciones que reflejen las nuevas funcionalidades:

**Nuevas Opciones:**

1. **Gestión de Publicaciones**:  
   * Crear una nueva publicación:  
     * Permitir al usuario elegir entre `Libro`, `Revista` y `Audiolibro`.  
     * Solicitar los datos específicos según el tipo de publicación.  
   * Listar todas las publicaciones.
   * Listar por tipo de publicación.  
   * Buscar una publicación por título o autor.  
2. **Préstamos**:  
   * Prestar una publicación (solo aplicable a publicaciones que implementen `Prestable`).  
   * Devolver una publicación.  
3. **Operaciones Multimedia**:  
   * Descargar un `Audiolibro`.  
   * Mostrar el formato de un `Audiolibro`.

**Ejemplo de Menú:**

```plaintext
Menú de Biblioteca:
1. Agregar una publicación
2. Listar todas las publicaciones
3. Listar libros
4. Listar revistas
5. Listar audiolibros
6. Buscar un libro por ISBN
7. Buscar una revista por número de edición
8. Buscar un audiolibro por narrador
9. Prestar un libro
10. Devolver un Libro
11. Descargar un audiolibro
12. Comprobar formato de un audiolibro
13. Salir
Opción:
```

## Calificación

* **Herencia e Interfaces (3.5 puntos)**
  * Implementación de la clase `Publicacion` y subclases: 2 puntos.  
  * Implementación de interfaces (`Prestable`, `Multimedia`): 1.5 punto
* **Encapsulamiento (1.5 puntos)**
  * Uso adecuado de getters/setters y validaciones.
* **Menú Principal (4 puntos)**
  * Correcta actualización del menú y manejo de opciones nuevas.
* **Memoria y Documentación (0.5 punto)**
  * Explicación clara de la implementación.
* **Otros Aspectos (0.5 punto)**
  * Calidad del código (nombres, indentado, comentarios).
