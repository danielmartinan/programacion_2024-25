# Actividad 6.1: Proyecto Gestor de Bibliotecas. Relaciones entre Clases, Herencia e Interfaces

## Introducción

En esta práctica, extenderás la funcionalidad del proyecto de la biblioteca introduciendo jerarquías de clases con herencia, interfaces y relaciones avanzadas entre clases. Sustituiremos la clase `Libro` por una clase más general, `Publicacion`, y crearemos diferentes tipos de publicaciones. Además, aplicaremos encapsulamiento, validaciones y un diseño orientado a interfaces para mejorar la modularidad del proyecto.


## Relaciones entre Clases

### Herencia

1. Sustituye la clase `Libro` por una clase abstracta `Publicacion`.  
   * **Atributos**:  
     * `titulo` (String)  
     * `autor` (String)  
     * `anioPublicacion` (int)  
   * **Métodos**:  
     * `mostrarInfo()` (abstracto): Método que será implementado por las subclases.  
     * Getters y setters con validaciones.  
2. Crea las siguientes subclases:  
   * **`Libro`**:  
     * Atributos adicionales:  
       * `ISBN` (String)  
       * `numeroPaginas` (int)  
     * Implementa `mostrarInfo()` para mostrar toda la información del libro.  
   * **`Revista`**:  
     * Atributos adicionales:  
       * `numeroEdicion` (int)  
       * `mesPublicacion` (String)  
     * Implementa `mostrarInfo()` para mostrar toda la información de la revista.  
   * **`Audiolibro`**:  
     * Atributos adicionales:  
       * `duracion` (double): Duración en horas.  
       * `narrador` (String)  
     * Implementa `mostrarInfo()`.

---

### Interfaces

1. Crea una interfaz `Prestable` con los métodos:  
   * `prestar()`  
   * `devolver()`  
   * `isPrestado()`: Devuelve un boolean indicando si la publicación está prestada.  
2. Haz que **`Libro`** implemente `Prestable`.  
   * Actualiza la clase para llevar un estado interno (`prestado`) que indique si el libro está prestado o disponible.  
3. Añade una nueva interfaz `Multimedia` para publicaciones digitales o audiovisuales.  
   * Métodos:  
     * `descargar()`  
     * `obtenerFormato()` (String)  
   * Haz que **`Audiolibro`** implemente esta interfaz.

### Encapsulamiento

1. Refactoriza todas las clases para:  
   * Hacer que los atributos sean privados.  
   * Implementar getters y setters con validaciones:  
     * Validar que el título y el autor no estén vacíos.  
     * Validar que el año de publicación no sea mayor al año actual.  
     * Validar que valores como `ISBN`, `numeroPaginas` o `duracion` sean válidos (no vacíos o positivos).

## Modificación del Menú Principal

Amplía el menú con opciones que reflejen las nuevas funcionalidades:

**Nuevas Opciones:**

1. **Gestión de Publicaciones**:  
   * Crear una nueva publicación:  
     * Permitir al usuario elegir entre `Libro`, `Revista` y `Audiolibro`.  
     * Solicitar los datos específicos según el tipo de publicación.  
   * Listar todas las publicaciones.  
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
1. Crear una publicación
2. Listar todas las publicaciones
3. Buscar una publicación
4. Prestar una publicación
5. Devolver una publicación
6. Descargar un audiolibro
7. Mostrar formato de un audiolibro
8. Salir
Opción:
``` 

## Calificación

- **Herencia e Interfaces (3 puntos)**
  - Implementación de la clase `Publicacion` y subclases: 2 puntos.  
  - Implementación de interfaces (`Prestable`, `Multimedia`): 1 punto 
- **Encapsulamiento (2 puntos)**
  - Uso adecuado de getters/setters y validaciones.
- **Menú Principal (3 puntos)**
  - Correcta actualización del menú y manejo de opciones nuevas.
- **Memoria y Documentación (1 punto)**
  - Explicación clara de la implementación.
- **Otros Aspectos (1 punto)**
  - Calidad del código (nombres, indentado, comentarios).