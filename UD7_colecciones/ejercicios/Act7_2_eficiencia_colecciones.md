# PROG07_2: Análisis de rendimiento de estructuras de datos en Java

## Objetivos

- Comprender experimentalmente el coste computacional de diferentes operaciones sobre las estructuras de datos más comunes en Java.
- Aprender a interpretar datos empíricos y relacionarlos con la complejidad algorítmica teórica.
- Desarrollar criterios para seleccionar la estructura de datos más adecuada según los requisitos de una aplicación.

## Material proporcionado

Se proporciona un programa Java (`ComparadorEstructuras.java`) que mide el tiempo de ejecución de diversas operaciones sobre las siguientes estructuras de datos:

- ArrayList
- LinkedList
- HashSet
- TreeSet
- HashMap
- TreeMap

Las operaciones evaluadas son:

1. Inserción de elementos
2. Búsqueda de elementos
3. Inserción al inicio (para listas)
4. Ordenación (para estructuras aplicables)
5. Eliminación de elementos

Puedes encontrar el proyecto en el siguiente repositorio de [Github](https://github.com/danielmartinan/PROG7_2_ComparadorEstructuras)

Ten en cuenta que los tiempos de ejecución pueden variar en función de la máquina en la que se ejecute el programa, por lo que es importante realizar varias ejecuciones y calcular la media de los tiempos, y, además, los resultados no serán comparables con los obtenidos en otras máquinas.

## Tareas a realizar

### 1. Análisis del código

Analiza el código proporcionado para entender cómo se realizan las mediciones de tiempo y qué operaciones se están evaluando. Comprende cómo se generan los datos aleatorios y cómo se realizan las operaciones sobre las estructuras de datos.

### 2. Ejecución y recopilación de datos

- Ejecuta el programa proporcionado al menos 5 veces.
- Registra los resultados de cada ejecución en una tabla.
- Calcula la media de los tiempos para cada operación.

Puedes utilizar una hoja de cálculo o una tabla en Markdown para organizar los datos.


| Estructura | Operación | Tiempo (ms) | Tiempo (ms) | Tiempo (ms) | Tiempo (ms) | Tiempo (ms) | Media (ms) |
|------------|-----------|-------------|-------------|-------------|-------------|-------------|------------|
| ArrayList  | Inserción | 100         | 110         | 105         | 95          | 120         | 106        |
| LinkedList | Inserción | 120         | 130         | 125         | 115         | 140         | 126        |
| ...        | ...       | ...         | ...         | ...         | ...         | ...         | ...        |


### 2. Análisis de resultados

Para cada estructura de datos, analiza:

- Comportamiento en operaciones de **inserción**
- Comportamiento en operaciones de **búsqueda**
- Comportamiento en operaciones de **eliminación**
- Comportamiento en **ordenación** (cuando aplique)

Contesta a las siguientes preguntas:

- ¿Qué estructura es más eficiente para búsquedas? ¿Por qué?
- ¿Qué estructura es más eficiente para inserciones? ¿Varía el resultado si la inserción es al inicio o al final?
- ¿Por qué ArrayList es rápido eliminando elementos del final pero extremadamente lento eliminando desde el principio?
- ¿Por qué no es necesario ordenar TreeSet y TreeMap?
- ¿Qué relación existe entre los tiempos obtenidos y la complejidad algorítmica teórica de cada operación?

### 3. Casos de uso

Basándote en tus resultados, indica qué estructura de datos recomendarías para cada uno de los siguientes escenarios:

- Un sistema de gestión de pedidos donde constantemente se consultan pedidos por su ID.
- Un historial de acciones donde se añaden nuevos eventos al principio y rara vez se eliminan.
- Una cola de mensajes donde los elementos se procesan en orden de llegada (FIFO).
- Un diccionario donde se realizan búsquedas por palabras y es importante mantener un orden alfabético.
- Un sistema de gestión de inventario donde se realizan frecuentes inserciones, eliminaciones y búsquedas.

### 4. Implementación

Modifica el código proporcionado para incluir alguna otra operación que consideres interesante de analizar, como:

- Actualización de elementos
- Iterar sobre todos los elementos
- Inserción/eliminación en posiciones aleatorias
