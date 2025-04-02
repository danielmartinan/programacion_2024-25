# Actividad 8.1: Proyecto Gestor de Bibliotecas. Aplicación de gestión de ficheros

## Introducción

En esta práctica, añadirás la posibilidad de gestionar ficheros en la aplicación de gestión de bibliotecas. Con estas funcionalidades, podrás importar y exportar datos de manera masiva, facilitando la gestión de libros y usuarios, la generación de backups o informes de actividad.

## Objetivos

- Practicar el uso de Streams para la gestión de ficheros en Java.
- Implementar la serialización y deserialización de objetos.

## Descripción de la tarea

A continuación se describen las tareas que debes realizar:

### Implementación de clase `GestorFicheros`

Implementar la clase `GestorFicheros` que permita gestionar la lectura y escritura de ficheros de texto y binarios.
La clase debe incluir los siguientes métodos:

- `leerLibrosDeCsv(String nombreFichero)`: Este método debe leer un fichero de texto con formato CSV y devolver una lista de objetos `Libro`.
- `escribirLibrosACsv(String nombreFichero, List<Libro> publicaciones)`: Este método debe escribir una lista de objetos `Libro` en un fichero de texto con formato CSV.

El formato del archivo CSV debe ser el siguiente:

```plaintext
titulo, autor, anioPublicacion, tipoPublicacion, isbn, numeroPaginas
```

El archivo CSV resultante debe incluir en la primera fila las cabeceras de las columnas, y cada fila posterior debe contener los datos de un libro. En caso de que alguna de las filas no contenga todos los campos, se debe omitir esa fila pero debe seguir leyendo el resto del archivo. Se indicará en la salida estándar el número de filas leídas y el número de filas válidas.

- `escribirUsuariosBin(String nombreFichero, List<Usuario> usuarios)`: Este método debe escribir una lista de objetos `Usuario` en un fichero binario. Utilizar la serialización de objetos para guardar los datos.
- `leerUsuariosBin(String nombreFichero)`: Este método debe leer un fichero binario y devolver una lista de objetos `Usuario`. Utilizar la deserialización de objetos para recuperar los datos.

### Modificación de la clase `Usuario`

Para poder serializar la clase `Usuario`, es necesario que implemente la interfaz `Serializable`. Además, se debe añadir un campo `private static final long serialVersionUID` para garantizar la compatibilidad entre versiones de la clase.

### Modificación de la clase Biblioteca

Se debe añadir a la clase `Biblioteca` un método `importarLibros(String nombreFichero)` que permita importar libros desde un fichero CSV. Este método debe utilizar el método `leerLibrosDeCsv` de la clase `GestorFicheros` para leer los libros y añadirlos a la biblioteca. Este método debe devolver el número de libros importados. Si el número de libros es superior a la capacidad de la biblioteca, deben importarse los primeros libros hasta alcanzar el límite de capacidad, e informar al usuario de cuántos libros se han importado y cuántos se han omitido.

Además, se debe añadir un método `exportarLibros(String nombreFichero)` que permita exportar los libros de la biblioteca a un fichero CSV. Este método debe utilizar el método `escribirLibrosACsv` de la clase `GestorFicheros` para escribir los libros. Este método debe devolver el número de libros exportados.

Por otra parte, se debe añadir un método `importarUsuarios(String nombreFichero)` que permita importar usuarios desde un fichero binario. Este método debe utilizar el método `leerUsuariosBin` de la clase `GestorFicheros` para leer los usuarios y añadirlos a la biblioteca. Este método debe devolver el número de usuarios importados.

Por último, se debe añadir un método `exportarUsuarios(String nombreFichero)` que permita exportar los usuarios de la biblioteca a un fichero binario. Este método debe utilizar el método `escribirUsuariosBin` de la clase `GestorFicheros` para escribir los usuarios. Este método debe devolver el número de usuarios exportados.

### Modificación del menú principal

Se debe ampliar el menú principal para añadir las nuevas funcionalidades:

- Importar libros desde un fichero CSV.
- Exportar libros a un fichero CSV.
- Importar usuarios desde un fichero binario.
- Exportar usuarios a un fichero binario.

Desde el menú principal se pedirá al usuario que indique el nombre del archivo, y se llamará a los métodos correspondientes de la clase `Biblioteca` para realizar la importación o exportación. En caso de que el fichero no exista o no se pueda leer, se debe informar al usuario y volver a mostrar el menú.

### Informe de actividad

Deberás crear un informe en formato pdf que incluya las actividades realizadas, las decisiones tomadas y dificultades encontradas en el proceso.

### Entrega

Deberás entregar un archivo comprimido que incluya el proyecto de Intellij IDEA (o IDE alternativo) completo, el informe descrito previamente, y un ejemplo de los archivos csv y binario creados, con el nombre

**apellido1_apellido2_nombre_PROG07_1.zip**

## Calificación

- Implementación de la clase `GestorFicheros` (3.5 puntos)
- Modificación de la clase `Usuario` (0.5 punto)
- Modificación de la clase `Biblioteca` (3 puntos)
- Modificación del menú principal (2.5 puntos)
- Creación del informe (0.5 puntos)
