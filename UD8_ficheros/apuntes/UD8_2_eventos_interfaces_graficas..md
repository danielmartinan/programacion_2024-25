# Programación Orientada a Eventos en Java

- [1. Programación Orientada a Eventos](#1-programación-orientada-a-eventos)
  - [1.1. Introducción](#11-introducción)
    - [1.1.1. ¿Qué es la programación orientada a eventos?](#111-qué-es-la-programación-orientada-a-eventos)
    - [1.1.2. Componentes principales del modelo de eventos](#112-componentes-principales-del-modelo-de-eventos)
    - [1.1.3. Programación secuencial vs. Programación orientada a eventos](#113-programación-secuencial-vs-programación-orientada-a-eventos)
    - [1.1.4. El patrón Observer y su relación con los eventos](#114-el-patrón-observer-y-su-relación-con-los-eventos)
  - [1.2. Modelo de Eventos en Java](#12-modelo-de-eventos-en-java)
    - [1.2.1. Arquitectura del modelo de eventos](#121-arquitectura-del-modelo-de-eventos)
    - [1.2.2. Clases e interfaces fundamentales](#122-clases-e-interfaces-fundamentales)
    - [1.2.3. Tipos comunes de eventos en Java](#123-tipos-comunes-de-eventos-en-java)
    - [1.2.4. Ciclo de vida de un evento](#124-ciclo-de-vida-de-un-evento)
    - [1.2.5. Registro y eliminación de oyentes](#125-registro-y-eliminación-de-oyentes)
  - [1.3. Implementación de Oyentes de Eventos](#13-implementación-de-oyentes-de-eventos)
    - [1.3.1. Creación de clases oyentes dedicadas](#131-creación-de-clases-oyentes-dedicadas)
    - [1.3.2. Clases anónimas](#132-clases-anónimas)
    - [1.3.3. Expresiones lambda (Java 8+)](#133-expresiones-lambda-java-8)
    - [1.3.4. Referencias a métodos (Java 8+)](#134-referencias-a-métodos-java-8)
    - [1.3.5. Clases adaptadoras](#135-clases-adaptadoras)
  - [1.4. Buenas prácticas en la gestión de eventos](#14-buenas-prácticas-en-la-gestión-de-eventos)
    - [1.4.1. Mantener el código de manejo de eventos corto y claro](#141-mantener-el-código-de-manejo-de-eventos-corto-y-claro)
    - [1.4.2. Evitar bloqueos en los manejadores de eventos](#142-evitar-bloqueos-en-los-manejadores-de-eventos)
    - [1.4.3. Gestión adecuada de recursos](#143-gestión-adecuada-de-recursos)
    - [1.4.4. Diseño cohesivo de sistemas de eventos](#144-diseño-cohesivo-de-sistemas-de-eventos)
- [2. Introducción a JavaFX](#2-introducción-a-javafx)
  - [2.1. ¿Qué es JavaFX?](#21-qué-es-javafx)
    - [2.1.1. Historia y evolución](#211-historia-y-evolución)
    - [2.1.2. Ventajas de JavaFX sobre Swing](#212-ventajas-de-javafx-sobre-swing)
  - [2.2. Estructura de una aplicación JavaFX](#22-estructura-de-una-aplicación-javafx)
    - [2.2.1. Componentes principales](#221-componentes-principales)
    - [2.2.2. Estructura básica de código](#222-estructura-básica-de-código)
    - [2.2.3. Jerarquía de nodos (Scene Graph)](#223-jerarquía-de-nodos-scene-graph)
  - [2.3. Ciclo de vida de una aplicación JavaFX](#23-ciclo-de-vida-de-una-aplicación-javafx)
    - [2.3.1. Hilos en JavaFX](#231-hilos-en-javafx)
  - [2.4. Layouts y contenedores](#24-layouts-y-contenedores)
    - [2.4.1. Layouts básicos](#241-layouts-básicos)
  - [2.5. FXML y Scene Builder](#25-fxml-y-scene-builder)
    - [2.5.1. ¿Qué es FXML?](#251-qué-es-fxml)
    - [2.5.2. Scene Builder](#252-scene-builder)
    - [2.5.3. Cargando FXML en la aplicación](#253-cargando-fxml-en-la-aplicación)
    - [2.5.4. Controladores FXML](#254-controladores-fxml)
  - [2.6. Configuración del entorno](#26-configuración-del-entorno)
    - [2.6.1. Requisitos](#261-requisitos)
    - [2.6.2. Configuración con Maven](#262-configuración-con-maven)
    - [2.6.3. Configuración con Gradle](#263-configuración-con-gradle)
  - [2.7. Ejemplo completo de una aplicación básica](#27-ejemplo-completo-de-una-aplicación-básica)
- [3. Componentes básicos de JavaFX](#3-componentes-básicos-de-javafx)
  - [3.1. Botones (Button)](#31-botones-button)
    - [3.1.1. Características principales](#311-características-principales)
    - [3.1.2. Ejemplo práctico](#312-ejemplo-práctico)
    - [3.1.3. Variantes](#313-variantes)
  - [3.2. Campos de texto (TextField)](#32-campos-de-texto-textfield)
    - [3.2.1. Características principales](#321-características-principales)
    - [3.2.2. Ejemplo práctico](#322-ejemplo-práctico)
    - [3.2.3. Variantes](#323-variantes)
  - [3.3. Etiquetas (Label)](#33-etiquetas-label)
    - [3.3.1. Características principales](#331-características-principales)
    - [3.3.2. Ejemplo práctico](#332-ejemplo-práctico)
    - [3.3.3. Usos comunes:](#333-usos-comunes)
  - [3.4. Layouts básicos](#34-layouts-básicos)
    - [3.4.1. HBox](#341-hbox)
    - [3.4.2. VBox](#342-vbox)
    - [3.4.3. BorderPane](#343-borderpane)
    - [3.4.4. GridPane](#344-gridpane)
  - [3.5. Otros componentes importantes](#35-otros-componentes-importantes)
- [4. Referencias y recursos adicionales](#4-referencias-y-recursos-adicionales)

## 1. Programación Orientada a Eventos

### 1.1. Introducción

#### 1.1.1. ¿Qué es la programación orientada a eventos?

La **programación orientada a eventos** es un paradigma de programación en el que el flujo de ejecución del programa está determinado por eventos como acciones del usuario, mensajes del sistema o interacciones con otros programas. A diferencia de la programación secuencial tradicional, donde el flujo de ejecución sigue un orden predeterminado (y es el flujo que seguían todos nuestros programas hasta el momento), la programación orientada a eventos responde a estímulos externos que pueden ocurrir en cualquier momento y en cualquier orden.

Un **evento** puede definirse como una acción o ocurrencia reconocida por el software, que puede ser manejada por el programa. Algunos ejemplos de eventos incluyen:

- Un clic de ratón
- Una pulsación de tecla
- La expiración de un temporizador
- La llegada de datos desde la red
- Cambios en el estado de un componente

#### 1.1.2. Componentes principales del modelo de eventos

El modelo de eventos en Java se basa en tres componentes fundamentales:

1. **Fuente del evento (Event Source)**: El objeto que genera o "dispara" el evento. Por ejemplo, un botón, un campo de texto o un temporizador.

2. **Objeto evento (Event Object)**: Contiene información sobre el evento que ha ocurrido, como el tipo de evento, la fuente que lo generó y, dependiendo del tipo de evento, información adicional específica.

3. **Oyente del evento (Event Listener)**: El objeto responsable de recibir y procesar el evento. Implementa una interfaz específica que define los métodos que serán llamados cuando ocurra el evento.

#### 1.1.3. Programación secuencial vs. Programación orientada a eventos

| Programación Secuencial | Programación Orientada a Eventos |
|-------------------------|-----------------------------------|
| El flujo de ejecución sigue un orden predeterminado | El flujo de ejecución depende de los eventos que ocurren |
| El control lo mantiene el programa | El control lo tienen los eventos externos |
| Predecible y determinista | No determinista (los eventos pueden ocurrir en cualquier orden) |
| Más sencilla de entender inicialmente | Requiere comprensión del modelo de eventos y callbacks |
| Adecuada para programas por lotes y aplicaciones de consola | Esencial para interfaces gráficas e interacción con usuarios |

#### 1.1.4. El patrón Observer y su relación con los eventos

El modelo de eventos de Java está basado en el patrón de diseño Observer (Observador), uno de los patrones de comportamiento más utilizados en programación orientada a objetos.

**Estructura del patrón Observer:**

1. **Subject (Sujeto)**: Mantiene una lista de observadores y notifica cambios a todos ellos.
   - En el modelo de eventos de Java: la fuente del evento

2. **Observer (Observador)**: Define una interfaz para recibir notificaciones.
   - En el modelo de eventos de Java: la interfaz del oyente (listener)

3. **ConcreteSubject**: Implementación específica del sujeto que envía notificaciones.
   - En el modelo de eventos de Java: componentes concretos como Button, TextField, etc.

4. **ConcreteObserver**: Implementación específica del observador que responde a las notificaciones.
   - En el modelo de eventos de Java: clases que implementan interfaces listener

**Ejemplo conceptual del patrón Observer en Java:**

```java
// Subject (interfaz)
interface Subject {
    void addObserver(Observer o);
    void removeObserver(Observer o);
    void notifyObservers();
}

// Observer (interfaz)
interface Observer {
    void update(String message);
}

// ConcreteSubject
class ConcreteSubject implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String state;
    
    public void setState(String state) {
        this.state = state;
        notifyObservers();
    }
    
    @Override
    public void addObserver(Observer o) {
        observers.add(o);
    }
    
    @Override
    public void removeObserver(Observer o) {
        observers.remove(o);
    }
    
    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(state);
        }
    }
}

// ConcreteObserver
class ConcreteObserver implements Observer {
    private String name;
    
    public ConcreteObserver(String name) {
        this.name = name;
    }
    
    @Override
    public void update(String message) {
        System.out.println(name + " recibió mensaje: " + message);
    }
}
```

### 1.2. Modelo de Eventos en Java

#### 1.2.1. Arquitectura del modelo de eventos

Java utiliza un modelo de eventos basado en **delegación**. En este modelo:

1. Las fuentes de eventos delegan la gestión de eventos a objetos especiales llamados **oyentes** (listeners).
2. Los oyentes se registran con las fuentes de eventos, indicando su interés en ser notificados.
3. Cuando ocurre un evento, la fuente notifica a todos los oyentes registrados.

Esta arquitectura permite una clara separación entre la generación de eventos y su manejo, facilitando el mantenimiento y la extensibilidad del código.

#### 1.2.2. Clases e interfaces fundamentales

El framework de eventos de Java se organiza en torno a varias clases e interfaces clave:

1. **EventObject**: La clase base para todos los objetos de eventos en Java.

   ```java
   public class EventObject extends Object implements Serializable {
       protected transient Object source;
       // ...
   }
   ```

2. **EventListener**: Una interfaz marcadora que define el patrón básico para todas las interfaces de escucha de eventos.

   ```java
   public interface EventListener {
   }
   ```

3. **Interfaces específicas de oyentes**: Interfaces que extienden EventListener para tipos específicos de eventos.

   ```java
   public interface ActionListener extends EventListener {
       void actionPerformed(ActionEvent e);
   }
   ```

4. **Clases de eventos específicos**: Clases que extienden EventObject para proporcionar información específica del tipo de evento.

   ```java
   public class ActionEvent extends AWTEvent {
       // ...
   }
   ```

#### 1.2.3. Tipos comunes de eventos en Java

Java proporciona una amplia variedad de tipos de eventos predefinidos, especialmente en sus bibliotecas de interfaz gráfica:

1. **ActionEvent**: Generado cuando se realiza una acción sobre un componente (p.ej., hacer clic en un botón).
2. **MouseEvent**: Generado por interacciones del ratón (clic, movimiento, entrada/salida).
3. **KeyEvent**: Generado por interacciones del teclado.
4. **WindowEvent**: Generado por cambios de estado en ventanas.
5. **ItemEvent**: Generado cuando cambia el estado de elementos seleccionables.
6. **TextEvent**: Generado cuando el contenido de componentes de texto cambia.
7. **FocusEvent**: Generado cuando un componente gana o pierde el foco.
8. **ComponentEvent**: Generado cuando un componente cambia de tamaño, posición o visibilidad.

#### 1.2.4. Ciclo de vida de un evento

El ciclo de vida típico de un evento en Java sigue estos pasos:

1. **Creación**: Un evento es creado por una fuente de eventos como respuesta a una acción (p.ej., un clic del usuario).
2. **Distribución**: La fuente del evento notifica a todos los oyentes registrados.
3. **Manejo**: Los oyentes ejecutan código específico en respuesta al evento.
4. **Finalización**: Una vez que todos los oyentes han procesado el evento, éste es descartado.

#### 1.2.5. Registro y eliminación de oyentes

Para recibir notificaciones de eventos, un oyente debe registrarse con la fuente de eventos correspondiente:

```java
// Registrar un oyente
button.addActionListener(new MiActionListener());

// Eliminar un oyente
button.removeActionListener(miActionListener);
```

Los métodos de registro típicamente siguen el patrón `add<TipoEvento>Listener()`.

### 1.3. Implementación de Oyentes de Eventos

#### 1.3.1. Creación de clases oyentes dedicadas

Una forma de implementar oyentes es crear clases específicas que implementen la interfaz correspondiente:

```java
// Clase oyente dedicada
public class MiActionListener implements ActionListener {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("Botón pulsado");
    }
}

// Uso
button.addActionListener(new MiActionListener());
```

#### 1.3.2. Clases anónimas

Las clases anónimas permiten definir e instanciar un oyente en el mismo lugar donde se registra:

```java
button.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("Botón pulsado");
    }
});
```

#### 1.3.3. Expresiones lambda (Java 8+)

Las expresiones lambda proporcionan una sintaxis más concisa para oyentes con una única función abstracta:

```java
button.addActionListener(e -> System.out.println("Botón pulsado"));
```

#### 1.3.4. Referencias a métodos (Java 8+)

Las referencias a métodos permiten utilizar métodos existentes como manejadores de eventos:

```java
// Método en la clase actual
private void manejarClick(ActionEvent e) {
    System.out.println("Botón pulsado");
}

// Registrar usando referencia a método
button.addActionListener(this::manejarClick);
```

#### 1.3.5. Clases adaptadoras

Para simplificar la implementación de oyentes con múltiples métodos, Java proporciona clases adaptadoras:

```java
// Sin adaptador - requiere implementar todos los métodos
button.addMouseListener(new MouseListener() {
    @Override public void mouseClicked(MouseEvent e) { /* ... */ }
    @Override public void mousePressed(MouseEvent e) { /* ... */ }
    @Override public void mouseReleased(MouseEvent e) { /* ... */ }
    @Override public void mouseEntered(MouseEvent e) { /* ... */ }
    @Override public void mouseExited(MouseEvent e) { /* ... */ }
});

// Con adaptador - solo se implementan los métodos necesarios
button.addMouseListener(new MouseAdapter() {
    @Override
    public void mouseClicked(MouseEvent e) {
        System.out.println("Ratón clicado");
    }
});
```

### 1.4. Buenas prácticas en la gestión de eventos

#### 1.4.1. Mantener el código de manejo de eventos corto y claro

Los manejadores de eventos deben ser **concisos** y enfocados en una **tarea específica**. Si el código es complejo, es mejor **delegarlo a métodos separados**:

```java
// Mal ejemplo: código extenso directamente en el manejador
button.addActionListener(e -> {
    // Muchas líneas de código aquí...
});

// Buen ejemplo: delegación a un método específico
button.addActionListener(e -> procesarDatos());

private void procesarDatos() {
    // Implementación del procesamiento
}
```

#### 1.4.2. Evitar bloqueos en los manejadores de eventos

Los manejadores de eventos se ejecutan en el hilo de la interfaz de usuario. Si realizan operaciones largas, pueden **bloquear** la interfaz:

```java
// Mal ejemplo: bloquea la interfaz
button.addActionListener(e -> {
    try {
        Thread.sleep(5000); // Operación que bloquea por 5 segundos
    } catch (InterruptedException ex) {
        ex.printStackTrace();
    }
});

// Buen ejemplo: uso de hilos separados
button.addActionListener(e -> {
    new Thread(() -> {
        // Operación larga aquí
    }).start();
});
```

#### 1.4.3. Gestión adecuada de recursos

Es importante **desregistrar** los oyentes cuando ya no son necesarios para evitar fugas de memoria:

```java
// Registrar
button.addActionListener(miListener);

// Importante: desregistrar cuando ya no se necesita
button.removeActionListener(miListener);
```

#### 1.4.4. Diseño cohesivo de sistemas de eventos

Al diseñar sistemas basados en eventos:

1. **Granularidad adecuada**: Define eventos ni demasiado genéricos ni demasiado específicos.
2. **Consistencia**: Utiliza patrones coherentes para eventos similares.
3. **Acoplamiento débil**: Minimiza las dependencias entre generadores y receptores de eventos.
4. **Documentación clara**: Documenta el propósito y el comportamiento esperado de cada evento.

## 2. Introducción a JavaFX

### 2.1. ¿Qué es JavaFX?

JavaFX es una plataforma de software diseñada para **crear aplicaciones de escritorio**, aplicaciones web ricas (RIAs) y aplicaciones móviles. Desarrollada como el **sucesor de Swing**, JavaFX ofrece una moderna API de Java para construir interfaces gráficas de usuario (GUI) con capacidades avanzadas de multimedia, gráficos vectoriales, animaciones y efectos visuales.

#### 2.1.1. Historia y evolución

- **JavaFX 1.0** (2008): Inicialmente se introdujo con un lenguaje de script declarativo llamado JavaFX Script.
- **JavaFX 2.0** (2011): Reescrito completamente como una biblioteca Java, abandonando el lenguaje de script.
- **JavaFX 8** (2014): Integrado directamente en el JDK 8 como parte de la plataforma Java SE.
- **JavaFX 11+** (2018 en adelante): Separado del JDK como un módulo independiente, siguiendo lanzamientos cada 6 meses.

#### 2.1.2. Ventajas de JavaFX sobre Swing

| Característica | JavaFX | Swing |
|----------------|--------|-------|
| Arquitectura | Moderna, basada en escena | Más antigua, basada en componentes |
| Separación de UI/lógica | FXML para separación clara | Mezcla de UI y lógica de negocio |
| Estilos | CSS para estilizar componentes | Look and Feel personalizado (más complejo) |
| Efectos visuales | Soporte nativo para efectos, animaciones | Limitado, requiere código adicional |
| Gráficos | Gráficos vectoriales, 3D | Principalmente bitmap, 2D |
| Multimedia | Soporte para audio/video | Limitado, requiere bibliotecas externas |
| Responsive Design | Layout managers modernos | Layouts menos flexibles |
| Hilos | Hilo dedicado para la interfaz (JavaFX Application Thread) | Event Dispatch Thread (EDT) |

### 2.2. Estructura de una aplicación JavaFX

#### 2.2.1. Componentes principales

Una aplicación JavaFX se basa en tres componentes fundamentales:

1. **Stage (Escenario)**: El contenedor de nivel superior, representa la ventana de la aplicación.
2. **Scene (Escena)**: El contenedor para todos los elementos de la interfaz de usuario.
3. **Nodes (Nodos)**: Los elementos individuales de la interfaz (controles, formas, etc.).

![Estructura JavaFX](https://ejemplo-imagen-estructura-javafx.jpg)

#### 2.2.2. Estructura básica de código

Toda aplicación JavaFX extiende la clase `javafx.application.Application` e implementa el método `start()`:

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.layout.StackPane;
import javafx.stage.Stage;

public class HolaMundoApp extends Application {
    
    @Override
    public void start(Stage primaryStage) {
        // 1. Crear elementos de la interfaz
        Label etiqueta = new Label("¡Hola Mundo con JavaFX!");
        
        // 2. Crear un layout (contenedor de nodos)
        StackPane root = new StackPane();
        root.getChildren().add(etiqueta);
        
        // 3. Crear una escena con el layout
        Scene escena = new Scene(root, 300, 200);
        
        // 4. Configurar y mostrar el escenario
        primaryStage.setTitle("Mi Primera Aplicación");
        primaryStage.setScene(escena);
        primaryStage.show();
    }
    
    public static void main(String[] args) {
        // 5. Lanzar la aplicación
        launch(args);
    }
}
```

#### 2.2.3. Jerarquía de nodos (Scene Graph)

JavaFX utiliza un modelo de grafo de escena (Scene Graph) para representar todos los elementos visuales de la aplicación:

- Es una estructura de árbol donde cada nodo tiene un único padre (excepto el nodo raíz)
- Los nodos padres pueden tener múltiples nodos hijos
- Los cambios en un nodo padre afectan a todos sus hijos
- Facilita la gestión de transformaciones, efectos y eventos

```plaintext
                 Stage
                   │
                 Scene
                   │
                 Root Node (Pane)
                 /      \
         Button         VBox
                        / \
                    Label  TextField
```

### 2.3. Ciclo de vida de una aplicación JavaFX

El ciclo de vida de una aplicación JavaFX está definido por varios métodos que se invocan automáticamente:

1. **init()**: Llamado después del constructor pero antes de `start()`. Puede utilizarse para inicializar recursos.
2. **start(Stage primaryStage)**: El método principal donde se configura la interfaz. Recibe el escenario principal como parámetro.
3. **stop()**: Llamado cuando la aplicación se detiene. Ideal para liberar recursos y guardar datos.

```java
public class CicloVidaApp extends Application {
    
    @Override
    public void init() throws Exception {
        System.out.println("1. Método init() - Inicialización");
        // Inicializar recursos, cargar configuraciones
    }
    
    @Override
    public void start(Stage primaryStage) {
        System.out.println("2. Método start() - Construyendo la UI");
        
        // Configuración de la interfaz
        StackPane root = new StackPane();
        Scene scene = new Scene(root, 300, 200);
        primaryStage.setScene(scene);
        primaryStage.setTitle("Ciclo de Vida");
        primaryStage.show();
    }
    
    @Override
    public void stop() throws Exception {
        System.out.println("3. Método stop() - Finalizando");
        // Guardar datos, cerrar conexiones, liberar recursos
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

#### 2.3.1. Hilos en JavaFX

JavaFX utiliza un hilo dedicado llamado **JavaFX Application Thread** para manejar la interfaz de usuario:

- Todas las operaciones que afectan a la interfaz deben ejecutarse en este hilo
- Las tareas largas deben ejecutarse en hilos separados para evitar bloquear la interfaz
- Se pueden utilizar `Task` y `Service` para ejecutar operaciones en segundo plano
- `Platform.runLater()` permite ejecutar código en el hilo de la interfaz desde otros hilos

```java
// Tarea en segundo plano
new Thread(() -> {
    // Código que puede tardar en completarse
    
    // Actualizar la UI desde el hilo de JavaFX
    Platform.runLater(() -> {
        label.setText("Tarea completada");
    });
}).start();
```

### 2.4. Layouts y contenedores

Los layouts en JavaFX son contenedores que organizan y posicionan los nodos hijos según diferentes estrategias.

#### 2.4.1. Layouts básicos

1. **StackPane**: Apila los elementos uno encima del otro (en el eje Z).

   ```java
   StackPane stack = new StackPane();
   stack.getChildren().addAll(rectanguloFondo, texto);
   ```

2. **HBox**: Organiza los elementos horizontalmente en una fila.

   ```java
   HBox hbox = new HBox(10); // 10px de espacio entre elementos
   hbox.getChildren().addAll(boton1, boton2, boton3);
   ```

3. **VBox**: Organiza los elementos verticalmente en una columna.

    ```java
   VBox vbox = new VBox(5); // 5px de espacio entre elementos
   vbox.getChildren().addAll(etiqueta, campoTexto, botonEnviar);
   ```

4. **BorderPane**: Divide el espacio en cinco áreas: top, right, bottom, left y center.

    ```java
   BorderPane border = new BorderPane();
   border.setTop(menuBar);
   border.setCenter(contenidoPrincipal);
   border.setBottom(barraEstado);
   ```

5. **GridPane**: Organiza los elementos en una cuadrícula flexible de filas y columnas.

   ```java
   GridPane grid = new GridPane();
   grid.add(labelNombre, 0, 0);      // columna 0, fila 0
   grid.add(textoNombre, 1, 0);      // columna 1, fila 0
   grid.add(labelApellido, 0, 1);    // columna 0, fila 1
   grid.add(textoApellido, 1, 1);    // columna 1, fila 1
   ```

6. **FlowPane**: Organiza los elementos en filas o columnas, ajustándolos cuando no hay espacio.

   ```java
   FlowPane flow = new FlowPane(Orientation.HORIZONTAL, 5, 5); // espacio H, espacio V
   flow.getChildren().addAll(botones);
   ```

7. **TilePane**: Similar a FlowPane, pero cada elemento ocupa el mismo espacio.

   ```java
   TilePane tile = new TilePane(Orientation.HORIZONTAL);
   tile.setPrefColumns(4); // 4 columnas
   tile.getChildren().addAll(imagenes);
   ```

8. **AnchorPane**: Permite fijar los nodos a los bordes del contenedor.

   ```java
   AnchorPane anchor = new AnchorPane();
   AnchorPane.setTopAnchor(boton, 10.0); // 10px desde arriba
   AnchorPane.setRightAnchor(boton, 10.0); // 10px desde la derecha
   anchor.getChildren().add(boton);
   ```

### 2.5. FXML y Scene Builder

#### 2.5.1. ¿Qué es FXML?

FXML es un lenguaje de marcado basado en XML que permite definir interfaces de usuario JavaFX de forma declarativa, separando la UI de la lógica de la aplicación.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<?import javafx.scene.control.*?>
<?import javafx.scene.layout.*?>

<VBox xmlns="http://javafx.com/javafx"
      xmlns:fx="http://javafx.com/fxml"
      fx:controller="com.ejemplo.MiControlador"
      spacing="10" alignment="CENTER">
    <Label text="Introduce tu nombre:"/>
    <TextField fx:id="campoNombre"/>
    <Button text="Saludar" onAction="#onBotonClick"/>
</VBox>
```

#### 2.5.2. Scene Builder

Scene Builder es una herramienta visual para crear interfaces FXML mediante arrastrar y soltar, sin necesidad de escribir código XML manualmente.

#### 2.5.3. Cargando FXML en la aplicación

```java
public class AplicacionFXML extends Application {
    
    @Override
    public void start(Stage primaryStage) throws Exception {
        // Cargar el archivo FXML
        FXMLLoader loader = new FXMLLoader(getClass().getResource("interfaz.fxml"));
        Parent root = loader.load();
        
        // Crear la escena
        Scene scene = new Scene(root);
        
        // Configurar y mostrar el escenario
        primaryStage.setTitle("Aplicación FXML");
        primaryStage.setScene(scene);
        primaryStage.show();
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

#### 2.5.4. Controladores FXML

Los controladores conectan la interfaz FXML con la lógica de la aplicación:

```java
public class MiControlador implements Initializable {
    
    @FXML
    private TextField campoNombre;
    
    @FXML
    private void onBotonClick(ActionEvent event) {
        String nombre = campoNombre.getText();
        System.out.println("Hola, " + nombre);
    }
    
    @Override
    public void initialize(URL location, ResourceBundle resources) {
        // Inicialización del controlador
    }
}
```

### 2.6. Configuración del entorno

#### 2.6.1. Requisitos

- JDK 11 o superior
- JavaFX SDK (a partir de Java 11 es un módulo separado)
- IDE (Eclipse, IntelliJ IDEA, NetBeans)
- Scene Builder (opcional, para diseño visual)

#### 2.6.2. Configuración con Maven

El archivo `pom.xml` para un proyecto JavaFX con Maven:

```xml
<dependencies>
    <dependency>
        <groupId>org.openjfx</groupId>
        <artifactId>javafx-controls</artifactId>
        <version>17.0.1</version>
    </dependency>
    <dependency>
        <groupId>org.openjfx</groupId>
        <artifactId>javafx-fxml</artifactId>
        <version>17.0.1</version>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-maven-plugin</artifactId>
            <version>0.0.8</version>
            <configuration>
                <mainClass>com.ejemplo.MiAplicacion</mainClass>
            </configuration>
        </plugin>
    </plugins>
</build>
```

#### 2.6.3. Configuración con Gradle

El archivo `build.gradle` para un proyecto JavaFX con Gradle:

```gradle
plugins {
    id 'java'
    id 'application'
    id 'org.openjfx.javafxplugin' version '0.0.10'
}

javafx {
    version = "17.0.1"
    modules = [ 'javafx.controls', 'javafx.fxml' ]
}

mainClassName = 'com.ejemplo.MiAplicacion'
```

### 2.7. Ejemplo completo de una aplicación básica

A continuación se presenta un ejemplo completo de una aplicación JavaFX básica que muestra varios conceptos:

```java
import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class EjemploCompleto extends Application {
    
    // Componentes de la interfaz
    private TextField campoNombre;
    private Label etiquetaSaludo;
    private Button botonSaludar;
    
    @Override
    public void start(Stage primaryStage) {
        // Crear componentes
        Label etiquetaInstruccion = new Label("Introduce tu nombre:");
        campoNombre = new TextField();
        campoNombre.setPromptText("Nombre"); // Texto de ayuda
        
        botonSaludar = new Button("Saludar");
        botonSaludar.setDefaultButton(true); // Se activa con Enter
        
        etiquetaSaludo = new Label();
        etiquetaSaludo.setStyle("-fx-font-size: 16px; -fx-font-weight: bold;");
        
        // Configurar evento del botón
        botonSaludar.setOnAction(e -> saludar());
        
        // Crear layout y añadir componentes
        VBox root = new VBox(10); // 10px de espacio vertical
        root.setPadding(new Insets(20)); // 20px de padding
        root.setAlignment(Pos.CENTER);
        root.getChildren().addAll(
            etiquetaInstruccion, 
            campoNombre, 
            botonSaludar,
            etiquetaSaludo
        );
        
        // Crear escena
        Scene scene = new Scene(root, 300, 200);
        
        // Configurar y mostrar el escenario
        primaryStage.setTitle("Saludador JavaFX");
        primaryStage.setScene(scene);
        primaryStage.show();
    }
    
    // Método para manejar el saludo
    private void saludar() {
        String nombre = campoNombre.getText().trim();
        
        if (nombre.isEmpty()) {
            etiquetaSaludo.setText("Por favor, introduce un nombre");
            etiquetaSaludo.setStyle("-fx-text-fill: red; -fx-font-size: 16px;");
        } else {
            etiquetaSaludo.setText("¡Hola, " + nombre + "!");
            etiquetaSaludo.setStyle("-fx-text-fill: green; -fx-font-size: 16px;");
        }
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

## 3. Componentes básicos de JavaFX

JavaFX proporciona una amplia variedad de componentes gráficos (también llamados controles) para construir interfaces de usuario interactivas. Estos componentes son esenciales para la interacción con el usuario y permiten crear aplicaciones visualmente atractivas y funcionales. A continuación se detallan los componentes más utilizados:

### 3.1. Botones (Button)

Los botones son componentes fundamentales que permiten al usuario ejecutar acciones cuando son presionados. 

#### 3.1.1. Características principales

- **Creación básica**: `Button button = new Button("Texto del botón");`
- **Establecer acción**: Se asocian eventos mediante el método `setOnAction()`
- **Personalización**: Permiten añadir iconos, establecer estilos y efectos

#### 3.1.2. Ejemplo práctico

```java
Button btnAceptar = new Button("Aceptar");
btnAceptar.setOnAction(event -> {
    System.out.println("Botón pulsado");
    // Código para manejar la acción
});

// Personalización
btnAceptar.setStyle("-fx-background-color: #4CAF50; -fx-text-fill: white;");
```

#### 3.1.3. Variantes

- **CheckBox**: Botón que puede estar marcado o desmarcado
- **RadioButton**: Botones que funcionan en grupo donde solo uno puede estar seleccionado
- **ToggleButton**: Botón que puede mantener su estado de pulsado

### 3.2. Campos de texto (TextField)

Los campos de texto permiten al usuario introducir datos textuales y son esenciales para formularios y entrada de datos.

#### 3.2.1. Características principales

- **Creación básica**: `TextField textField = new TextField();`
- **Valor inicial**: `TextField textField = new TextField("Texto inicial");`
- **Obtener texto**: `String texto = textField.getText();`
- **Establecer texto**: `textField.setText("Nuevo texto");`

#### 3.2.2. Ejemplo práctico

```java
TextField tfNombre = new TextField();
tfNombre.setPromptText("Introduce tu nombre"); // Texto de ayuda

Button btnSaludar = new Button("Saludar");
btnSaludar.setOnAction(e -> {
    if (!tfNombre.getText().isEmpty()) {
        System.out.println("Hola, " + tfNombre.getText());
    }
});
```

#### 3.2.3. Variantes

- **PasswordField**: Campo de texto que oculta los caracteres introducidos
- **TextArea**: Campo para texto multilínea
- **Spinner**: Campo numérico con botones para incrementar/decrementar

### 3.3. Etiquetas (Label)

Las etiquetas se utilizan para mostrar texto no editable en la interfaz, proporcionando información al usuario.

#### 3.3.1. Características principales

- **Creación básica**: `Label label = new Label("Texto de la etiqueta");`
- **Asociar a otros controles**: Facilitan la accesibilidad asociándolas a campos de entrada
- **Personalización**: Permiten usar diferentes fuentes, colores y estilos

#### 3.3.2. Ejemplo práctico

```java
Label lblTitulo = new Label("Formulario de registro");
lblTitulo.setStyle("-fx-font-size: 16pt; -fx-font-weight: bold;");

Label lblNombre = new Label("Nombre:");
TextField tfNombre = new TextField();
// Asociar etiqueta con campo
lblNombre.setLabelFor(tfNombre);
```

#### 3.3.3. Usos comunes:

- Títulos y subtítulos
- Descripción de campos de entrada
- Mostrar información o resultados
- Mensajes de estado

### 3.4. Layouts básicos

Los layouts son contenedores que organizan y posicionan los componentes en la interfaz. JavaFX proporciona varios tipos de layouts para diferentes necesidades.

#### 3.4.1. HBox

HBox organiza los componentes en una fila horizontal.

##### Características

- **Creación**: `HBox hbox = new HBox(10);` (el parámetro es el espacio entre componentes)
- **Añadir componentes**: `hbox.getChildren().addAll(componente1, componente2);`
- **Alineación**: `hbox.setAlignment(Pos.CENTER);`

##### Ejemplo

```java
HBox hbox = new HBox(10); // 10px de separación
hbox.setPadding(new Insets(15)); // Margen interior
hbox.setAlignment(Pos.CENTER_LEFT);
hbox.getChildren().addAll(new Label("Nombre:"), new TextField());
```

#### 3.4.2. VBox

VBox organiza los componentes en una columna vertical.

##### Características

- **Creación**: `VBox vbox = new VBox(10);`
- **Añadir componentes**: Similar a HBox
- **Alineación**: Similar a HBox

##### Ejemplo

```java
VBox vbox = new VBox(15);
vbox.setPadding(new Insets(10));
vbox.getChildren().addAll(
    new Label("Formulario"),
    new TextField(),
    new Button("Enviar")
);
```

#### 3.4.3. BorderPane

BorderPane divide el espacio en cinco regiones: top, bottom, left, right y center.

##### Características

- **Creación**: `BorderPane borderPane = new BorderPane();`
- **Posicionar componentes**: `borderPane.setTop(componente);`, `borderPane.setCenter(componente);`, etc.

##### Ejemplo

```java
BorderPane root = new BorderPane();
root.setTop(new Label("Aplicación JavaFX"));
root.setCenter(new TextArea("Área principal"));
root.setBottom(new HBox(10, new Button("Aceptar"), new Button("Cancelar")));
```

#### 3.4.4. GridPane

GridPane organiza los componentes en una cuadrícula flexible de filas y columnas.

##### Características

- **Creación**: `GridPane grid = new GridPane();`
- **Añadir componentes**: `grid.add(componente, columna, fila);`
- **Espaciado**: `grid.setHgap(10);` y `grid.setVgap(10);`

##### Ejemplo

```java
GridPane grid = new GridPane();
grid.setPadding(new Insets(10));
grid.setHgap(10); // Espacio horizontal
grid.setVgap(10); // Espacio vertical

// Añadir componentes especificando columna y fila
grid.add(new Label("Usuario:"), 0, 0);
grid.add(new TextField(), 1, 0);
grid.add(new Label("Contraseña:"), 0, 1);
grid.add(new PasswordField(), 1, 1);
grid.add(new Button("Iniciar sesión"), 1, 2);
```

### 3.5. Otros componentes importantes

Aunque no se incluyen en los componentes básicos del índice, es útil conocer estos otros controles comunes:

- **ComboBox**: Lista desplegable para seleccionar opciones
- **ListView**: Lista de elementos seleccionables
- **TableView**: Tabla para mostrar datos en filas y columnas
- **DatePicker**: Selector de fecha
- **ProgressBar/ProgressIndicator**: Indicadores de progreso
- **Slider**: Control deslizante para seleccionar valores en un rango
- **MenuBar**: Barra de menú con opciones desplegables

## 4. Referencias y recursos adicionales

- Documentación oficial de Java: [java.util.EventObject](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/EventObject.html)
- Libro: "Effective Java" de Joshua Bloch (capítulos sobre lambdas y clases internas)
- Tutorial sobre el patrón Observer: [Refactoring Guru - Observer Pattern](https://refactoring.guru/design-patterns/observer)
- [Documentación oficial de JavaFX](https://openjfx.io/javadoc/17/)
- [Tutorial de JavaFX en Oracle](https://docs.oracle.com/javase/8/javafx/get-started-tutorial/jfx-overview.htm)
- [Scene Builder](https://gluonhq.com/products/scene-builder/)
- [Ejemplos de código JavaFX](https://github.com/openjfx/samples)
