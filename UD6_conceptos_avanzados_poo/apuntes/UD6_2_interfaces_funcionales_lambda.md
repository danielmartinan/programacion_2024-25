# Interfaces funcionales y expresiones Lambda

- [1. Introducción a las Interfaces Funcionales](#1-introducción-a-las-interfaces-funcionales)
- [2. Interfaces Funcionales Predefinidas en Java](#2-interfaces-funcionales-predefinidas-en-java)
- [3. Uso de Expresiones Lambda para Simplificar Código](#3-uso-de-expresiones-lambda-para-simplificar-código)
  - [3.1. Sintaxis de las Expresiones Lambda](#31-sintaxis-de-las-expresiones-lambda)
  - [3.2. Inferencia de Tipos (Type Inference)](#32-inferencia-de-tipos-type-inference)
  - [3.3. Uso de `this` en expresiones lambda](#33-uso-de-this-en-expresiones-lambda)
    - [3.3.1. Ejemplo con una clase normal y una lambda](#331-ejemplo-con-una-clase-normal-y-una-lambda)
  - [3.4. Comparación entre clases anónimas y expresiones lambda](#34-comparación-entre-clases-anónimas-y-expresiones-lambda)
    - [3.4.1. Ejemplo con una clase anónima](#341-ejemplo-con-una-clase-anónima)
    - [3.4.2. El mismo código con una expresión lambda](#342-el-mismo-código-con-una-expresión-lambda)
  - [3.5. Uso de métodos de referencia (`::`)](#35-uso-de-métodos-de-referencia-)
    - [3.5.1. 1️⃣ Referencia a un método estático](#351-1️⃣-referencia-a-un-método-estático)
    - [3.5.2. 2️⃣ Referencia a un método de instancia](#352-2️⃣-referencia-a-un-método-de-instancia)
    - [3.5.3. 3️⃣ Referencia a un método de una instancia arbitraria](#353-3️⃣-referencia-a-un-método-de-una-instancia-arbitraria)
    - [3.5.4. 4️⃣ Referencia a un constructor\*\*](#354-4️⃣-referencia-a-un-constructor)
  - [3.6. Ejemplos simples](#36-ejemplos-simples)
  - [3.7. Ventajas de las Expresiones Lambda](#37-ventajas-de-las-expresiones-lambda)
- [4. Composición de Funciones en Java](#4-composición-de-funciones-en-java)
  - [4.1. `andThen()`: Aplicar funciones en secuencia](#41-andthen-aplicar-funciones-en-secuencia)
  - [4.2. `compose()`: Aplicar funciones en orden inverso](#42-compose-aplicar-funciones-en-orden-inverso)
  - [4.3. Comparación entre `andThen()` y `compose()`](#43-comparación-entre-andthen-y-compose)
  - [4.4. Ejemplo práctico con `String`](#44-ejemplo-práctico-con-string)
- [5. Aplicación en Streams](#5-aplicación-en-streams)
- [6. Ejemplos y Aplicaciones Prácticas](#6-ejemplos-y-aplicaciones-prácticas)
  - [6.1. Filtrado de Elementos con `Predicate`](#61-filtrado-de-elementos-con-predicate)
  - [6.2. Transformación con `Function`](#62-transformación-con-function)
  - [6.3. Iteración con `Consumer`](#63-iteración-con-consumer)
  - [6.4. Suministrar Datos con `Supplier`](#64-suministrar-datos-con-supplier)
  - [6.5. Composición de Funciones](#65-composición-de-funciones)
- [7. Conclusión](#7-conclusión)

Las expresiones lambda, introducidas en **Java 8**, representan un cambio importante en el paradigma de programación del lenguaje, permitiendo escribir código más conciso y funcional. Se utilizan principalmente para implementar interfaces funcionales de forma clara y simplificada.

## 1. Introducción a las Interfaces Funcionales

Una **interfaz funcional** es una interfaz que tiene exactamente **un único método abstracto** (aunque, adicionalmente, puede contener métodos default y static). Este método abstracto representa la funcionalidad que implementará la expresión lambda.  
Las interfaces funcionales pueden tener:

- Un único método abstracto (obligatorio).  
- Métodos `default` y `static` adicionales (sin restricciones en su cantidad).

Se identifican con la anotación `@FunctionalInterface`, que es opcional pero recomendada para evitar errores si accidentalmente se añaden múltiples métodos abstractos.

**Ejemplo de una Interfaz Funcional:**

```java
@FunctionalInterface
public interface Operacion {
    int ejecutar(int a, int b); // Un único método abstracto
}
```

## 2. Interfaces Funcionales Predefinidas en Java

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

- **BiFunction\<T, U, R\>:** Aplica una función que toma dos argumentos y devuelve un resultado.  

    ```java  
    R apply(T t, U u);
    ```

- **BiPredicate\<T, U\>:** Devuelve un valor booleano basado en dos argumentos.  

    ```java
    boolean test(T t, U u);
    ```

- **UnaryOperator\<T\>:** Es una especialización de `Function` que toma un solo argumento del mismo tipo y devuelve un resultado del mismo tipo.

    ```java
    T apply(T t);
    ```

- **BinaryOperator\<T\>:** Es una especialización de `BiFunction` que toma dos argumentos del mismo tipo y devuelve un resultado del mismo tipo.

    ```java
    T apply(T t1, T t2);
    ```

## 3. Uso de Expresiones Lambda para Simplificar Código

### 3.1. Sintaxis de las Expresiones Lambda

La expresión lambda permite definir un comportamiento en una única línea o bloque compacto. Su estructura es:

```java
(parametros) -> { cuerpo };
```

- **Parámetros:** La lista de argumentos que recibe el método. Pueden omitirse los tipos si son inferibles.  
- **Operador `->`:** Separa los parámetros del cuerpo de la función.  
- **Cuerpo:** El bloque de código que implementa la funcionalidad.

### 3.2. Inferencia de Tipos (Type Inference)

En las expresiones lambda, Java puede inferir automáticamente los tipos de los parámetros. Por ejemplo, en el siguiente código, Java sabe que `a` y `b` son enteros:

```java
Operacion suma = (a, b) -> a + b;
```

Sin embargo, si la inferencia no es clara, puede ser necesario especificar los tipos. Si se desea especificar explícitamente los tipos, se puede hacer de la siguiente manera:

```java
Operacion suma = (int a, int b) -> a + b;
```

### 3.3. Uso de `this` en expresiones lambda

En Java, el uso de `this` dentro de una expresión lambda **difiere del uso en clases anónimas**. Para entenderlo bien, hay que recordar que:  

✔️ **Las expresiones lambda NO crean una nueva instancia de clase.**  
✔️ **Las clases anónimas SÍ crean una nueva instancia de clase.**  
✔️ **Dentro de una lambda, `this` hace referencia a la instancia de la clase externa.**  

#### 3.3.1. Ejemplo con una clase normal y una lambda

```java
class MiClase {
    private String nombre = "MiClase";

    void metodo() {
        Runnable r1 = new Runnable() {
            String nombre = "Clase Anónima";

            @Override
            public void run() {
                System.out.println(this.nombre); // "Clase Anónima"
            }
        };

        Runnable r2 = () -> {
            System.out.println(this.nombre); // "MiClase"
        };

        r1.run();
        r2.run();
    }
}

public class EjemploThis {
    public static void main(String[] args) {
        new MiClase().metodo();
    }
}
```

**Explicación:**

- En la **clase anónima**, `this` hace referencia a la instancia de la **clase anónima**.  
- En la **expresión lambda**, `this` hace referencia a la **clase que la contiene (`MiClase`)**.  

✔️ **Regla clave:** **Las lambdas no tienen su propia instancia**, por lo que `this` apunta a la clase envolvente.  

### 3.4. Comparación entre clases anónimas y expresiones lambda

Antes de Java 8, se usaban **clases anónimas** para implementar interfaces con un solo método. Sin embargo, las **expresiones lambda** permiten escribir código más conciso y legible.  

#### 3.4.1. Ejemplo con una clase anónima

```java
interface Operacion {
    int calcular(int a, int b);
}

public class EjemploClaseAnonima {
    public static void main(String[] args) {
        Operacion suma = new Operacion() {
            @Override
            public int calcular(int a, int b) {
                return a + b;
            }
        };

        System.out.println(suma.calcular(5, 3)); // 8
    }
}
```

#### 3.4.2. El mismo código con una expresión lambda

```java
Operacion suma = (a, b) -> a + b;
System.out.println(suma.calcular(5, 3)); // 8
```

✔️ **Diferencias clave:**  

| Característica | Clases anónimas | Lambdas |
|--------------|---------------|---------|
| **Verbosidad** | Código más largo | Código más corto |
| **Instancia propia (`this`)** | ✅ Tiene su propia instancia | ❌ Usa la instancia de la clase externa |
| **Flexibilidad** | Puede tener múltiples métodos y estados | Solo un método funcional |

**Conclusión:** **Usar lambdas siempre que sea posible**, a menos que se necesite mantener estado o implementar múltiples métodos.  

### 3.5. Uso de métodos de referencia (`::`)

Los métodos de referencia (`::`) permiten **reutilizar métodos existentes** en lugar de escribir expresiones lambda completas.  

✔️ **Tipos de métodos de referencia:**  
1️⃣ **Referencia a un método estático** → `Clase::metodoEstatico`  
2️⃣ **Referencia a un método de instancia** → `instancia::metodo`  
3️⃣ **Referencia a un método de una instancia arbitraria** → `Clase::metodo`  
4️⃣ **Referencia a un constructor** → `Clase::new`  

#### 3.5.1. 1️⃣ Referencia a un método estático

```java
import java.util.function.Function;

public class MetodosReferencia {
    static int duplicar(int x) {
        return x * 2;
    }

    public static void main(String[] args) {
        Function<Integer, Integer> f1 = x -> MetodosReferencia.duplicar(x);
        Function<Integer, Integer> f2 = MetodosReferencia::duplicar; // Equivalente

        System.out.println(f1.apply(5)); // 10
        System.out.println(f2.apply(5)); // 10
    }
}
```

**`MetodosReferencia::duplicar` reemplaza la lambda `x -> duplicar(x)`**.  

#### 3.5.2. 2️⃣ Referencia a un método de instancia

```java
class Saludo {
    void decirHola(String nombre) {
        System.out.println("Hola " + nombre);
    }
}

public class EjemploMetodoInstancia {
    public static void main(String[] args) {
        Saludo saludo = new Saludo();
        Runnable r1 = () -> saludo.decirHola("Carlos");
        Runnable r2 = saludo::decirHola; // Equivalente

        r1.run();
        r2.run();
    }
}
```

**`saludo::decirHola` reemplaza la lambda `nombre -> saludo.decirHola(nombre)`**.  

#### 3.5.3. 3️⃣ Referencia a un método de una instancia arbitraria

Cuando se trabaja con Streams, es común referenciar métodos de una clase en lugar de escribir una lambda.  

```java
List<String> nombres = List.of("Ana", "Carlos", "Beatriz");

// Con expresión lambda
nombres.forEach(n -> System.out.println(n));

// Con método de referencia
nombres.forEach(System.out::println);
```

**`System.out::println` reemplaza la lambda `n -> System.out.println(n)`**.  

#### 3.5.4. 4️⃣ Referencia a un constructor**

También se pueden referenciar constructores cuando se necesita crear objetos dentro de un `Stream`.  

```java
import java.util.function.Supplier;

class Persona {
    Persona() {
        System.out.println("Nueva persona creada");
    }
}

public class EjemploConstructor {
    public static void main(String[] args) {
        Supplier<Persona> crearPersona = Persona::new;
        Persona p = crearPersona.get(); // "Nueva persona creada"
    }
}
```

**`Persona::new` reemplaza `() -> new Persona()`**.  

### 3.6. Ejemplos simples

```java
Operacion suma = (a, b) -> a + b;
System.out.println(suma.ejecutar(5, 3)); // Salida: 8
```

En este caso:

- `(a, b)` son los parámetros.  
- `a + b` es la implementación del método `ejecutar`.

A continuación se muestran más ejemplos de expresiones lambda:

```java
// Diferentes formas de escribir una lambda:
Operacion suma1 = (a, b) -> a + b; // Expresión más corta
Operacion suma2 = (int a, int b) -> { return a + b; }; // Uso explícito de tipos y return
Operacion suma3 = (a, b) -> { 
    int resultado = a + b; 
    System.out.println("Resultado: " + resultado);
    return resultado;
}; // Cuerpo con múltiples instrucciones
```

### 3.7. Ventajas de las Expresiones Lambda

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

## 4. Composición de Funciones en Java

La **composición de funciones** es un concepto clave en la programación funcional que permite **encadenar funciones** para realizar transformaciones secuenciales sobre los datos.  

En Java, la interfaz funcional `Function<T, R>` proporciona dos métodos clave para la composición de funciones:  

✔️ **`andThen()`** → Aplica una función y luego otra.  
✔️ **`compose()`** → Aplica una función primero y luego la original.  

Estos métodos permiten encadenar múltiples funciones de manera clara y concisa.  

### 4.1. `andThen()`: Aplicar funciones en secuencia

El método `andThen()` permite **ejecutar primero la función original y luego la función que se le pasa como argumento**.  

**Fórmula:**  

```java
g.andThen(f).apply(x)  // Primero g(x), luego f(g(x))

```

✔️ **Ejemplo: Aplicar dos funciones en orden**

```java
import java.util.function.Function;

public class EjemploAndThen {
    public static void main(String[] args) {
        Function<Integer, Integer> duplicar = x -> x * 2;
        Function<Integer, Integer> sumarTres = x -> x + 3;

        Function<Integer, Integer> operacion = duplicar.andThen(sumarTres);

        System.out.println(operacion.apply(4)); // (4 * 2) + 3 = 11
    }
}
```

**Explicación:**  
1️⃣ Primero se ejecuta `duplicar(4) → 8`.  
2️⃣ Luego `sumarTres(8) → 11`.  

✔️ **Útil cuando se necesita procesar datos en pasos secuenciales.**  

### 4.2. `compose()`: Aplicar funciones en orden inverso

El método `compose()` funciona igual que `andThen()`, pero ejecuta primero la función que recibe como argumento y luego la función original.  

**Fórmula:**

```java
f.compose(g).apply(x)  // Primero g(x), luego f(g(x))
```

✔️ **Ejemplo: Cambiar el orden de ejecución**

```java
Function<Integer, Integer> duplicar = x -> x * 2;
Function<Integer, Integer> sumarTres = x -> x + 3;

Function<Integer, Integer> operacion = duplicar.compose(sumarTres);

System.out.println(operacion.apply(4)); // (4 + 3) * 2 = 14
```

**Explicación:**  
1️⃣ Primero se ejecuta `sumarTres(4) → 7`.  
2️⃣ Luego `duplicar(7) → 14`.  

✔️ **Útil cuando se quiere modificar los datos antes de pasarlos a la función principal.**  

### 4.3. Comparación entre `andThen()` y `compose()`

| Método         | Orden de ejecución | Fórmula |
|---------------|--------------------|---------|
| **`andThen()`** | **Primero la función original, luego la pasada por parámetro** | `f.andThen(g) → g(f(x))` |
| **`compose()`** | **Primero la función pasada por parámetro, luego la original** | `f.compose(g) → f(g(x))` |

✔️ **`andThen()`** → Primero transforma con la función actual, luego con la nueva.  
✔️ **`compose()`** → Primero transforma con la nueva función, luego con la actual.  

### 4.4. Ejemplo práctico con `String`

Imagina que queremos formatear nombres en una base de datos, primero eliminando espacios y luego convirtiendo a mayúsculas.  

```java
import java.util.function.Function;

public class EjemploString {
    public static void main(String[] args) {
        Function<String, String> quitarEspacios = String::trim;
        Function<String, String> aMayusculas = String::toUpperCase;

        Function<String, String> formatoCorrecto = quitarEspacios.andThen(aMayusculas);

        System.out.println(formatoCorrecto.apply("  hola mundo  ")); // "HOLA MUNDO"
    }
}
```

**`andThen()` es ideal cuando queremos aplicar transformaciones en orden lógico.**  

## 5. Aplicación en Streams

También podemos usar `andThen()` en Streams para encadenar transformaciones.  

```java
import java.util.List;
import java.util.function.Function;
import java.util.stream.Collectors;

public class EjemploStream {
    public static void main(String[] args) {
        List<String> nombres = List.of("  ana  ", "carlos", " BEATRIZ ");

        Function<String, String> formatear = ((Function<String, String>) String::trim)
                .andThen(String::toLowerCase)
                .andThen(s -> s.substring(0, 1).toUpperCase() + s.substring(1));

        List<String> nombresFormateados = nombres.stream()
                .map(formatear)
                .collect(Collectors.toList());

        System.out.println(nombresFormateados); // [Ana, Carlos, Beatriz]
    }
}
```

## 6. Ejemplos y Aplicaciones Prácticas

### 6.1. Filtrado de Elementos con `Predicate`

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

### 6.2. Transformación con `Function`

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

### 6.3. Iteración con `Consumer`

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

### 6.4. Suministrar Datos con `Supplier`

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

### 6.5. Composición de Funciones

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

## 7. Conclusión

Las expresiones lambda son una herramienta poderosa para escribir código funcional y conciso en Java. Junto con las interfaces funcionales y las herramientas de la API de streams, permiten manejar colecciones y funciones de una manera más declarativa y legible, mejorando la productividad del desarrollo.

**Siguiente sección:** [Anexo: uso avanzado de enums en Java](./UD6_anexo_enums_avanzados.md)
