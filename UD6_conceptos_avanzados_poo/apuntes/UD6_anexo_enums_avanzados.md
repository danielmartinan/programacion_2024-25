# Utilización avanzadas de `enums` en Java

- [1. Introducción](#1-introducción)
- [2. Atributos y métodos en enumeradores](#2-atributos-y-métodos-en-enumeradores)
  - [2.1. Atributos en enumeradores](#21-atributos-en-enumeradores)
  - [2.2. Métodos en enumeradores](#22-métodos-en-enumeradores)
- [3. Métodos estáticos en enumeradores](#3-métodos-estáticos-en-enumeradores)
- [4. Implementación de interfaces en enumeradores](#4-implementación-de-interfaces-en-enumeradores)
- [5. Utilización de enumeradores en estructuras de datos](#5-utilización-de-enumeradores-en-estructuras-de-datos)
- [EnumSet y EnumMap](#enumset-y-enummap)
- [6. Métodos Abstractos en Enums](#6-métodos-abstractos-en-enums)
- [7. Enums en Expresiones `switch`](#7-enums-en-expresiones-switch)
- [8. Enums como Singleton](#8-enums-como-singleton)
- [9. Enums y Serialización](#9-enums-y-serialización)
- [10. Enums y excepciones](#10-enums-y-excepciones)
- [11. Enums y Lambdas](#11-enums-y-lambdas)
- [12. Enums y Reflexión](#12-enums-y-reflexión)
  - [12.1. Nota: ¿qué es la reflexión?](#121-nota-qué-es-la-reflexión)
- [Referencias](#referencias)

## 1. Introducción

En unidades didácticas previas hemos visto el uso habitual de los enumeradores en Java. Los enumeradores son una forma de definir un conjunto de constantes con un tipo de datos específico. En Java, los enumeradores son una clase especial que se puede utilizar para definir un conjunto fijo de constantes.

```java
public enum DiaSemana {
    LUNES, MARTES, MIERCOLES, JUEVES, VIERNES, SABADO, DOMINGO
}
```

Sobre estos enumeradores, disponíamos de métodos como `values()`, `valueOf(String)` y `ordinal()`. Sin embargo, los enumeradores en Java pueden ser mucho más potentes y versátiles de lo que hemos visto hasta ahora.

En este anexo se van a presentar algunos conceptos avanzados relacionados con el uso de enumeradores en Java. Veremos cómo podemos añadir atributos y métodos a los enumeradores, cómo podemos implementar interfaces en los enumeradores y cómo podemos utilizar los enumeradores en estructuras de datos más complejas. Veremos también cómo los enumeradores pueden ser utilizados en expresiones `switch`, con anotaciones, con serialización, con comparaciones, con lambdas y con reflexión, funcionalides avanzadas que a estas alturas del curso aún no hemos visto, pero que ya podremos explotar en el futuro.

## 2. Atributos y métodos en enumeradores

En Java, los enumeradores son una clase especial que se puede utilizar para definir un conjunto fijo de constantes. Aunque los enumeradores son una clase especial, no se pueden instanciar como objetos. Sin embargo, los enumeradores pueden tener atributos y métodos.

### 2.1. Atributos en enumeradores

Los enumeradores en Java pueden tener atributos. Para añadir atributos a un enumerador, se deben declarar los atributos como variables de instancia y añadir un constructor que inicialice los atributos.

```java
public enum DiaSemana {
    LUNES("Lunes", "L", 1),
    MARTES("Martes", "M", 2),
    MIERCOLES("Miércoles", "X", 3),
    JUEVES("Jueves", "J", 4),
    VIERNES("Viernes", "V", 5),
    SABADO("Sábado", "S", 6),
    DOMINGO("Domingo", "D", 7);

    private final String nombre;
    private final String abreviatura;
    private final int numero;

    DiaSemana(String nombre, String abreviatura, int numero) {
        this.nombre = nombre;
        this.abreviatura = abreviatura;
        this.numero = numero;
    }

    public String getNombre() {
        return nombre;
    }

    public String getAbreviatura() {
        return abreviatura;
    }

    public int getNumero() {
        return numero;
    }
}
```

En este ejemplo, el enumerador `DiaSemana` tiene tres atributos: `nombre`, `abreviatura` y `numero`. El enumerador también tiene un constructor que inicializa los atributos. Además, el enumerador tiene métodos para acceder a los atributos. Los atributos son constantes, ya que una vez se inicializa, no se deben modificar sus valores.

### 2.2. Métodos en enumeradores

Los enumeradores en Java también pueden tener métodos. Para añadir métodos a un enumerador, se deben declarar los métodos como métodos de instancia.

```java
public enum DiaSemana {
    LUNES("Lunes", "L", 1),
    MARTES("Martes", "M", 2),
    MIERCOLES("Miércoles", "X", 3),
    JUEVES("Jueves", "J", 4),
    VIERNES("Viernes", "V", 5),
    SABADO("Sábado", "S", 6),
    DOMINGO("Domingo", "D", 7);

    private String nombre;
    private String abreviatura;
    private int numero;

    DiaSemana(String nombre, String abreviatura, int numero) {
        this.nombre = nombre;
        this.abreviatura = abreviatura;
        this.numero = numero;
    }

    public boolean esLaborable() {
        return this != SABADO && this != DOMINGO;
    }
}
```

En este ejemplo, el enumerador `DiaSemana` tiene un método `esLaborable()` que devuelve `true` si el día de la semana es laborable (es decir, no es sábado ni domingo) y `false` en caso contrario. Este método podríamos utilizarlo de la siguiente manera:

```java
DiaSemana dia = DiaSemana.LUNES;
System.out.println(dia.esLaborable()); // Imprime true
```

## 3. Métodos estáticos en enumeradores

Los enumeradores en Java también pueden tener métodos estáticos:

```java
public enum DiaSemana {
    LUNES("Lunes", "L", 1),
    MARTES("Martes", "M", 2),
    MIERCOLES("Miércoles", "X", 3),
    JUEVES("Jueves", "J", 4),
    VIERNES("Viernes", "V", 5),
    SABADO("Sábado", "S", 6),
    DOMINGO("Domingo", "D", 7);

    private String nombre;
    private String abreviatura;
    private int numero;

    DiaSemana(String nombre, String abreviatura, int numero) {
        this.nombre = nombre;
        this.abreviatura = abreviatura;
        this.numero = numero;
    }

    public static boolean abreviaturaValida(String abreviatura) {
        for (DiaSemana dia : DiaSemana.values()) {
            if (dia.abreviatura.equals(abreviatura)) {
                return true;
            }
        }
        return false;
    }
}
```

En este ejemplo, el enumerador `DiaSemana` tiene un método estático `abreviaturaValida(String abreviatura)` que comprueba si una abreviatura dada es válida para un día de la semana. Este método se puede utilizar sin necesidad de instanciar un objeto `DiaSemana`:

```java
System.out.println(DiaSemana.abreviaturaValida("L")); // Imprime true
System.out.println(DiaSemana.abreviaturaValida("X")); // Imprime true
System.out.println(DiaSemana.abreviaturaValida("Z")); // Imprime false
```

## 4. Implementación de interfaces en enumeradores

Los enumeradores en Java pueden implementar interfaces. Para implementar una interfaz en un enumerador, se deben declarar los métodos de la interfaz en el enumerador.

```java
public enum DiaSemana implements Comparable<DiaSemana> {
    LUNES("Lunes", "L", 1),
    MARTES("Martes", "M", 2),
    MIERCOLES("Miércoles", "X", 3),
    JUEVES("Jueves", "J", 4),
    VIERNES("Viernes", "V", 5),
    SABADO("Sábado", "S", 6),
    DOMINGO("Domingo", "D", 7);

    private String nombre;
    private String abreviatura;
    private int numero;

    DiaSemana(String nombre, String abreviatura, int numero) {
        this.nombre = nombre;
        this.abreviatura = abreviatura;
        this.numero = numero;
    }

    ...

    @Override
    public int compareTo(DiaSemana otro) {
        return Integer.compare(this.numero, otro.numero);
    }
}
```

En este ejemplo, el enumerador `DiaSemana` implementa la interfaz `Comparable<DiaSemana>`. El enumerador tiene un método `compareTo(DiaSemana otro)` que compara dos días de la semana por su número. Este método se puede utilizar para ordenar los días de la semana por número:

```java
DiaSemana[] dias = {DiaSemana.MIERCOLES, DiaSemana.LUNES, DiaSemana.VIERNES};
Arrays.sort(dias);
for (DiaSemana dia : dias) {
    System.out.println(dia);
}
```

## 5. Utilización de enumeradores en estructuras de datos

Los enumeradores en Java se pueden utilizar en estructuras de datos más complejas, como listas, conjuntos y mapas. Por ejemplo, se pueden utilizar enumeradores en un mapa para asociar un valor a cada constante del enumerador.

```java
public enum DiaSemana {
    LUNES("Lunes", "L", 1),
    MARTES("Martes", "M", 2),
    MIERCOLES("Miércoles", "X", 3),
    JUEVES("Jueves", "J", 4),
    VIERNES("Viernes", "V", 5),
    SABADO("Sábado", "S", 6),
    DOMINGO("Domingo", "D", 7);

    private String nombre;
    private String abreviatura;
    private int numero;

    DiaSemana(String nombre, String abreviatura, int numero) {
        this.nombre = nombre;
        this.abreviatura = abreviatura;
        this.numero = numero;
    }

    public String getNombre() {
        return nombre;
    }

    public String getAbreviatura() {
        return abreviatura;
    }

    public int getNumero() {
        return numero;
    }

    public static Map<String, DiaSemana> getMapaAbreviaturas() {
        Map<String, DiaSemana> mapa = new HashMap<>();
        for (DiaSemana dia : DiaSemana.values()) {
            mapa.put(dia.abreviatura, dia);
        }
        return mapa;
    }
}
```

En este ejemplo, el enumerador `DiaSemana` tiene un método estático `getMapaAbreviaturas()` que devuelve un mapa que asocia cada abreviatura de día de la semana con el enumerador correspondiente. Este método se puede utilizar para obtener el día de la semana a partir de su abreviatura:

```java
Map<String, DiaSemana> mapa = DiaSemana.getMapaAbreviaturas();
System.out.println(mapa.get("L")); // Imprime LUNES
System.out.println(mapa.get("X")); // Imprime MIERCOLES
System.out.println(mapa.get("Z")); // Imprime null
```

## EnumSet y EnumMap

Java proporciona las clases `EnumSet` y `EnumMap` para trabajar con enumeradores de forma eficiente. `EnumSet` es una implementación especializada de `Set` que solo puede contener elementos de un enumerador dado. `EnumMap` es una implementación especializada de `Map` que asocia claves de un enumerador con valores.

```java
public enum DiaSemana {
    LUNES, MARTES, MIERCOLES, JUEVES, VIERNES, SABADO, DOMINGO;
}

public class EjemploEnumSet {
    public static void main(String[] args) {
        EnumSet<DiaSemana> laborables = EnumSet.range(DiaSemana.LUNES, DiaSemana.VIERNES);
        System.out.println(laborables); // Imprime [LUNES, MARTES, MIERCOLES, JUEVES, VIERNES]
    }
}

// Ejemplo de uso de EnumMap
public class EjemploEnumMap {
    public static void main(String[] args) {
        EnumMap<DiaSemana, String> nombres = new EnumMap<>(DiaSemana.class);
        nombres.put(DiaSemana.LUNES, "Lunes");
        nombres.put(DiaSemana.MARTES, "Martes");
        nombres.put(DiaSemana.MIERCOLES, "Miércoles");
        nombres.put(DiaSemana.JUEVES, "Jueves");
        nombres.put(DiaSemana.VIERNES, "Viernes");
        nombres.put(DiaSemana.SABADO, "Sábado");
        nombres.put(DiaSemana.DOMINGO, "Domingo");
        System.out.println(nombres); // Imprime {LUNES=Lunes, MARTES=Martes, MIERCOLES=Miércoles, JUEVES=Jueves, VIERNES=Viernes, SABADO=Sábado, DOMINGO=Domingo}
    }
}
```

## 6. Métodos Abstractos en Enums

Los `enums` pueden tener métodos abstractos, lo que permite que cada constante del `enum` implemente su propia versión del método. Esto es útil cuando cada constante necesita un comportamiento específico.

```java
public enum Operacion {
    SUMA {
        @Override
        public int aplicar(int a, int b) {
            return a + b;
        }
    },
    RESTA {
        @Override
        public int aplicar(int a, int b) {
            return a - b;
        }
    },
    MULTIPLICACION {
        @Override
        public int aplicar(int a, int b) {
            return a * b;
        }
    };

    public abstract int aplicar(int a, int b);
}
```

En este ejemplo, el `enum` `Operacion` tiene tres constantes (`SUMA`, `RESTA` y `MULTIPLICACION`), cada una de las cuales implementa su propia versión del método `aplicar(int a, int b)`. Esto permite que cada constante realice una operación diferente. El método `aplicar(int a, int b)` se puede utilizar de la siguiente manera:

```java
System.out.println(Operacion.SUMA.aplicar(5, 3)); // Imprime: 8
System.out.println(Operacion.RESTA.aplicar(5, 3)); // Imprime: 2
```

## 7. Enums en Expresiones `switch`

Los `enums` son ideales para usar en expresiones `switch`, ya que proporcionan un conjunto cerrado de valores. Esto hace que el código sea más seguro y legible.

```java
public enum DiaSemana {
    LUNES, MARTES, MIERCOLES, JUEVES, VIERNES, SABADO, DOMINGO;
}

public class EjemploSwitch {
    public static void main(String[] args) {
        DiaSemana dia = DiaSemana.LUNES;

        switch (dia) {
            case LUNES:
                System.out.println("Es lunes, ¡ánimo!");
                break;
            case VIERNES:
                System.out.println("¡Es viernes, fin de semana cerca!");
                break;
            default:
                System.out.println("Día normal...");
        }
    }
}
```

En este ejemplo, el `enum` `DiaSemana` se utiliza en una expresión `switch` para imprimir un mensaje dependiendo del día de la semana. El uso de `enums` en expresiones `switch` hace que el código sea más legible y fácil de mantener.

## 8. Enums como Singleton

Los `enums` en Java se pueden utilizar para implementar el patrón Singleton. Esto garantiza que solo haya una instancia de la clase en todo el programa.

```java
public enum Configuracion {
    INSTANCIA;

    private String servidor;
    private String usuario;
    private String clave;

    public String getServidor() {
        return servidor;
    }

    public void setServidor(String servidor) {
        this.servidor = servidor;
    }

    public String getUsuario() {
        return usuario;
    }

    public void setUsuario(String usuario) {
        this.usuario = usuario;
    }

    public String getClave() {
        return clave;
    }

    public void setClave(String clave) {
        this.clave = clave;
    }
}
```

En este ejemplo, el `enum` `Configuracion` se utiliza como Singleton para almacenar la configuración de la aplicación. La instancia única se puede acceder en cualquier parte del programa:

```java
Configuracion config = Configuracion.INSTANCIA;
config.setServidor("localhost");
config.setUsuario("admin");
config.setClave("12345");
```

Puedes obtener más información sobre el uso de `enums` como Singleton [aquí](https://www.baeldung.com/java-singleton-enum), [aquí](https://dzone.com/articles/java-singletons-using-enum) y [aquí](https://www.geeksforgeeks.org/advantages-and-disadvantages-of-using-enum-as-singleton-in-java/).

Los `enums` pueden ser utilizados en combinación con anotaciones para proporcionar metadatos adicionales. Esto es útil en frameworks como Spring o Hibernate.

```java
public enum TipoUsuario {
    ADMIN,
    USUARIO,
    INVITADO;
}

public @interface Permiso {
    TipoUsuario[] value();
}

@Permiso({TipoUsuario.ADMIN, TipoUsuario.USUARIO})
public class RecursoSeguro {
    // Código de la clase
}
```

## 9. Enums y Serialización

Los `enums` son serializables de forma segura, ya que solo se serializa el nombre de la constante, no su estado interno. Esto los hace ideales para su uso en aplicaciones distribuidas.

```java
public enum EstadoConexion {
    CONECTADO, DESCONECTADO;
}

public class Configuracion implements Serializable {
    private EstadoConexion estado;

    // Getters y setters
}
```

## 10. Enums y excepciones

Los métodos de los enumeradores pueden lanzar excepciones. Esto permite que cada constante del enumerador maneje sus propias excepciones.

```java
public enum Operacion {
    DIVISION {
        @Override
        public int aplicar(int a, int b) {
            if (b == 0) {
                throw new IllegalArgumentException("División por cero");
            }
            return a / b;
        }
    };

    public abstract int aplicar(int a, int b);
}
```

En este ejemplo, la constante `DIVISION` del `enum` `Operacion` lanza una excepción si se intenta dividir por cero. Esto permite que cada constante maneje sus propias excepciones de forma independiente.

## 11. Enums y Lambdas

Los `enums` pueden ser utilizados en combinación con expresiones lambda para proporcionar comportamientos dinámicos.

```java
public enum Operacion {
    SUMA((a, b) -> a + b),
    RESTA((a, b) -> a - b),
    MULTIPLICACION((a, b) -> a * b);

    private final IntBinaryOperator operador;

    Operacion(IntBinaryOperator operador) {
        this.operador = operador;
    }

    public int aplicar(int a, int b) {
        return operador.applyAsInt(a, b);
    }
}
```

En este ejemplo, el `enum` `Operacion` tiene un constructor que toma una expresión lambda como argumento. Esto permite que cada constante del `enum` defina su propio comportamiento dinámico. `IntBinaryOperator` es una interfaz funcional que toma dos enteros y devuelve un entero:


```java
System.out.println(Operacion.SUMA.aplicar(5, 3)); // Imprime: 8
```

## 12. Enums y Reflexión

Los `enums` pueden ser utilizados con reflexión para obtener información sobre sus constantes y métodos.

```java
public enum DiaSemana {
    LUNES, MARTES, MIERCOLES, JUEVES, VIERNES, SABADO, DOMINGO;
}

public class EjemploReflexion {
    public static void main(String[] args) {
        Class<DiaSemana> enumClass = DiaSemana.class;
        System.out.println("Constantes: " + Arrays.toString(enumClass.getEnumConstants()));
    }
}
```

En este ejemplo, se utiliza reflexión para obtener las constantes del `enum` `DiaSemana`. Esto permite obtener información sobre las constantes del `enum` en tiempo de ejecución.

### 12.1. Nota: ¿qué es la reflexión?

La reflexión es una característica de Java que permite a los programas inspeccionar y modificar su propia estructura interna. La reflexión se utiliza para obtener información sobre clases, métodos, campos, constructores, etc., en tiempo de ejecución. La reflexión es una característica avanzada de Java que se utiliza en frameworks y bibliotecas para proporcionar funcionalidades dinámicas y extensibles.

```java
public class EjemploReflexion {
    public static void main(String[] args) {
        Class<?> clase = String.class;
        System.out.println("Nombre de la clase: " + clase.getName());
        System.out.println("Nombre simple de la clase: " + clase.getSimpleName());
        System.out.println("Paquete de la clase: " + clase.getPackage().getName());
        System.out.println("Superclase: " + clase.getSuperclass().getName());
        System.out.println("Interfaces: " + Arrays.toString(clase.getInterfaces()));
        System.out.println("Constructores: " + Arrays.toString(clase.getConstructors()));
        System.out.println("Métodos: " + Arrays.toString(clase.getMethods()));
        System.out.println("Campos: " + Arrays.toString(clase.getFields()));
    }
}
```

Como vemos en el ejemplo anterior, la reflexión se utiliza para obtener información sobre la clase `String`. La reflexión proporciona métodos para obtener el nombre de la clase, el nombre simple de la clase, el paquete de la clase, la superclase, las interfaces, los constructores, los métodos o los campos de la clase.

## Referencias

- [Java Enum Tutorial with Examples](https://www.baeldung.com/a-guide-to-java-enums)
- [Enum in Java](https://www.geeksforgeeks.org/enum-in-java/)
- [Enums in Java](https://www.javatpoint.com/enum-in-java)
- [API de reflexión: reflexión. El lado oscuro de Java](https://codegym.cc/es/groups/posts/es.45.api-de-reflexion-reflexion-el-lado-oscuro-de-java)
