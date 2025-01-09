# 1. Interfaces funcionales y expresiones Lambda

Las expresiones lambda, introducidas en **Java 8**, representan un cambio importante en el paradigma de programación del lenguaje, permitiendo escribir código más conciso y funcional. Se utilizan principalmente para implementar interfaces funcionales de forma clara y simplificada.

## 1.1. Introducción a las Interfaces Funcionales

Una **interfaz funcional** es una interfaz que tiene exactamente **un único método abstracto**. Este método abstracto representa la funcionalidad que implementará la expresión lambda.  
Las interfaces funcionales pueden tener:

* Métodos abstractos (uno obligatorio).  
* Métodos por defecto y estáticos adicionales (sin restricciones en su cantidad).

Se identifican con la anotación `@FunctionalInterface` (opcional, pero recomendada).

**Ejemplo de una Interfaz Funcional:**

```java
@FunctionalInterface
public interface Operacion {
    int ejecutar(int a, int b); // Un único método abstracto
}
```

## 1.2. Interfaces Funcionales Predefinidas en Java

Java 8 incluye muchas interfaces funcionales en el paquete `java.util.function`. Algunas de las más comunes son:

- **Predicate\<T\>:** Devuelve un valor booleano basado en una condición.  
  
```java
boolean test(T t);
```

- **Function\<T, R\>:** Aplica una transformación y devuelve un resultado.  
  
```java  
R apply(T t);
```

- **Consumer\<T\>:** Ejecuta una operación sobre un objeto recibido.  

```java
void accept(T t);
```

- **Supplier\<T\>:** Proporciona un resultado sin entrada.  

```java
T get();
```

**BiFunction\<T, U, R\>:** Aplica una función que toma dos argumentos y devuelve un resultado.  

```java  
R apply(T t, U u);
```

## 1.3. Uso de Expresiones Lambda para Simplificar Código

### 1.3.1. Sintaxis de las Expresiones Lambda

La expresión lambda permite definir un comportamiento en una única línea o bloque compacto. Su estructura es:

```java
(parametros) -> { cuerpo };
```

- **Parámetros:** La lista de argumentos que recibe el método. Pueden omitirse los tipos si son inferibles.  
- **Operador `->`:** Separa los parámetros del cuerpo de la función.  
- **Cuerpo:** El bloque de código que implementa la funcionalidad.

### 1.3.2. Ejemplo Simple

```java
Operacion suma = (a, b) -> a + b;
System.out.println(suma.ejecutar(5, 3)); // Salida: 8
```

En este caso:

* `(a, b)` son los parámetros.  
* `a + b` es la implementación del método `ejecutar`.

## 1.4. Ventajas de las Expresiones Lambda

1. **Concisión:** Eliminan la necesidad de clases anónimas para implementar interfaces funcionales.  
2. **Legibilidad:** Reducen el código ceremonial y facilitan la comprensión.  
3. **Flexibilidad:** Permiten combinar programación funcional y orientación a objetos.

**Sin Lambda (Clase Anónima):**

```java

Operacion suma = new Operacion() {
    @Override
    public int ejecutar(int a, int b) {
        return a + b;
    }
};
```

**Con Lambda:**

```java
Operacion suma = (a, b) -> a + b;
```


## 1.5. Ejemplos y Aplicaciones Prácticas

### 1.5.1. Filtrado de Elementos con `Predicate`

Las expresiones lambda son ideales para filtrar colecciones.

**Ejemplo:**

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;

public class Main {
    public static void main(String[] args) {
        List<String> nombres = Arrays.asList("Ana", "Pedro", "Luis", "Marta");

        // Filtrar nombres que comienzan con "M"
        Predicate<String> empiezaConM = nombre -> nombre.startsWith("M");
        nombres.stream().filter(empiezaConM).forEach(System.out::println); 
        // Salida: Marta
    }
}
```

### 1.5.2. Transformación con `Function`

Permiten transformar datos fácilmente.

**Ejemplo:**

```java
import java.util.function.Function;

public class Main {
    public static void main(String[] args) {
        Function<Integer, String> convertir = num -> "Número: " + num;

        System.out.println(convertir.apply(5)); // Salida: Número: 5
    }
}

```

### 1.5.3. Iteración con `Consumer`

Ideal para realizar operaciones sobre cada elemento de una colección.

**Ejemplo:**

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Consumer;

public class Main {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("Manzana", "Pera", "Uva");

        Consumer<String> imprimir = fruta -> System.out.println("Fruta: " + fruta);
        frutas.forEach(imprimir);
        // Salida:
        // Fruta: Manzana
        // Fruta: Pera
        // Fruta: Uva
    }
}
```

### 1.5.4. Suministrar Datos con `Supplier`

Se utilizan para generar datos dinámicamente.

**Ejemplo:**

```java
import java.util.function.Supplier;

public class Main {
    public static void main(String[] args) {
        Supplier<Double> generarAleatorio = () -> Math.random();

        System.out.println("Número aleatorio: " + generarAleatorio.get());
    }
}
```


### 1.5.5. Composición de Funciones

Las expresiones lambda permiten la composición de múltiples operaciones.

**Ejemplo:**

```java
import java.util.function.Function;

public class Main {
    public static void main(String[] args) {
        Function<Integer, Integer> duplicar = x -> x * 2;
        Function<Integer, Integer> sumarTres = x -> x + 3;

        Function<Integer, Integer> combinar = duplicar.andThen(sumarTres);

        System.out.println(combinar.apply(4)); // Salida: 11 (4 * 2 + 3)
    }
}
```

## 1.6. Conclusión

Las expresiones lambda son una herramienta poderosa para escribir código funcional y conciso en Java. Junto con las interfaces funcionales y las herramientas de la API de streams, permiten manejar colecciones y funciones de una manera más declarativa y legible, mejorando la productividad del desarrollo.