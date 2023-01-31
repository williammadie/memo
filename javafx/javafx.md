# JavaFX

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Alternatives](#alternatives)
- [XML VS HTML](#xml-vs-html)
- [Approaches](#approaches)
    - [Declarative Method](#declarative-method)
    - [Procedural Method](#procedural-method)
- [Interface](#interface)
    - [Mandatory Methods](#mandatory-methods)
- [Scene Graph](#scene-graph)

## Introduction

JavaFX was released in 2008. It is a **Java framework** used to build UI for Java Programs.

Quick reminder: a framework is **an overlayer built on top of a programming language. It can include support programs, compilers, code libraries, toolsets, and APIs to develop software and create systems.**. 

Today, JavaFX is still used. However, it is **rarely part** of the **main enterprise app**. it is mainly used to create tools to manage/configure the main enterprise app.

It is used by IT schools in order to learn UI creation.

## Prerequisites

- JVM
- JDK
- JavaFX

## Alternatives

- AWT (Abstract Window Toolkit):
    - heavy components
    - do not handle well cross-platform
- Swing:
    - light components
    - No UI Building Tool
- JavaFX:
    - SceneBuilder: UI Building Tool

## XML VS HTML

JavaFX uses a custom variant of the **XML language** called the **FXML language**.

What is the difference with the HTML language?

|    **Language Name**   |                                                                         **HTML**                                                                        |                                                                            **XML**                                                                           |
|:----------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| **Language Full Name** |                                                                HyperText Markup Language                                                                |                                                                  Extensible Markup Language                                                                  |
|        **Goals**       |                                                        Creation of Web Pages and Web Applications                                                       |                                                  Creation of Human and Machine readable documents/softwares                                                  |
|    **Specificities**   | - has predefined tags - some tags do not have a closing tag - case insensitive - focus on displaying data - helps to develop the structure of web pages | - allows its own set of tags - mandatory to close tags - case sensitive - focus on carrying information - helps to exchange data between different platforms |

## Approaches

We can use two methods to build a JavaFX application:
- **Declarative Method** (Java, SceneBuilder, FXML, MVC architecture (= mandatory 3-Tier Architecture))
- **Procedural Method** (Java API for building UI with code)

### Declarative Method

More intuitive because we use SceneBuilder. It generates the FXML code for us.

### Procedural Method

A bit more complicative because we have to know how components work, how they can be set and what do they allow.

The example below is a simple JavaFX application which count from 0 to infinity. The value is changed when the user clicks on the button.
Everything is written without using a FXML file. It is the **procedural method**.
```java
public class App extends Application {

    @Override
    public void start(Stage primaryStage) throws IOException {
        StackPane root = new StackPane();

        Scene scene = new Scene(root, 400, 400);
        scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());

        // Create a component
        Text counter = new Text();
        // Define an Id for the stylesheets
        counter.setId("counterTitle");
        counter.setText("0");

        // Create another component
        Button btn = new Button();
        btn.setText("Click to count!!");
        btn.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                int currentValue = Integer.valueOf(counter.getText());
                System.out.println(currentValue);
                counter.setText(String.valueOf(++currentValue));
            }
        });

        // Create a container
        VBox line = new VBox();
        line.setAlignment(Pos.CENTER);
        // Add the components to the container
        line.getChildren().addAll(btn, counter);
        // Add the container to the root container
        root.getChildren().add(line);

        primaryStage.setTitle("Welcome folks!");
        primaryStage.setHeight(500);
        primaryStage.setWidth(800);
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }

}
```

## Interface

An Interface is always composed of 3 things:
1. a **Window** with associated parameters (width, height)
2. an **Interface**
3. a **Container** (GridPane, AnchorPane, Pane, VBox, HBox...). It is a space containing a bunch of components/nested components.

Some vocabulary:
Stage = Window
Scene = Interface
Node = Component

A **stage** is composed of a **scene**.
A **scene** is composed of **nodes**.

A Node can be:
- **invisible** (container)
- **visible** (Components like Button, TextBox...)

In JavaFX, all objects are inherited from `Application`. By default, the minimal JavaFX application looks like:
```java
public class App extends Application {

    // JavaFX Launch Point
    @Override
    public void start(Stage primaryStage) throws IOException {
        TextFlow root = new TextFlow();
        Scene scene = new Scene(root, 400, 400);
        scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());
        
        Text welcome = new Text();
        welcome.setText("Welcome folks!");
        root.getChildren().add(welcome);

        primaryStage.setScene(scene);
        primaryStage.show();
    }

    // Java Entry Point
    public static void main(String[] args) {
        launch(args);
    }

}
```


### Mandatory methods

Start the Java Program
```java
public static void main(String[] args) { ... }
```

Launch the JavaFX application
```java
public void start(Stage stage) throws IOException { ... }
```

## Scene Graph

It is a representation of the tree structure of a JavaFX UI.
It always has:
- **a root**
- **middle nodes** (generally invisible structural nodes)
- **leaves** (generally visible components/nodes)

This graph can be global (generic names) or detailed (specific class names)

## Containers

All containers inhrerits from the `Node` class. Look at the diagram below:

![javafx-hierarchy](/javafx/resources/javafx.png)

## Styles

Set the style directly in a java file
```java
btn1.setStyle("-fx-background-color: red;");
```

Use a CSS file:
```java
scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());

//...

counter.setId("counterTitle");  // Set a #class for CSS identifying
```

```css
#counterTitle {
    -fx-font: 18px Tahoma;
    -fx-fill: red;
    -fx-stroke: red;
    -fx-stroke-width: 1;
}
```