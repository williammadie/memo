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
- [Containers](#containers)
- [Styles](styles)
- [Example](#examples)

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

Important code snippets:

**1. Inside the `start()` function**

Declare the location of the view file
```java
BorderPane root = (BorderPane)FXMLLoader.load(getClass().getResource("my-view1.fxml"));
```

**2. Inside the view file**

Link a controller with a view (the link is done in the **root container**)
```java
<BorderPane prefHeight="600.0" prefWidth="800.0" xmlns:fx="http://programming_languages/javafx.com/fxml/1" xmlns="http://programming_languages/javafx.com/programming_languages/javafx/19" fx:controller="application.SampleController">
```

Building Steps:

1. Create a view with SceneBuilder
2. Create a Java class `MyController`
3. Link the view with the controller (see code above)

React to an event
1. Create a Button with an FxID
```xml
<Button fx:id="btn1" text="Click Me"/>
```

2. In the Controller, declare an attribute for this button
(with the same FxID as the one in the view)
```java
@FXML
private Button btn1;
```

3. Declare an event handler
```java
@FXML
  private void initialize() {
    myButton.setOnAction(new EventHandler<ActionEvent>() {
      @Override
      public void handle(ActionEvent event) {
        // Perform some action when the button is clicked
      }
    });
  }
```

### Procedural Method

This method is based on **Java API**.

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

This graph can be **global** (components on the interface only) or **detailed** (show the inheritance and make mother classes appear)

Here is a global scene graph:

![scene-graph](/programming_languages/javafx/resources/scene-graph.png)

**Additional Note**: JavaFX components are organized on a x,y axis. The default position for a composant is at (0,0).

![javafx-axis](/programming_languages/javafx/resources/javafx-axis.png)

## Containers

All containers inhrerits from the `Node` class. Look at the diagram below:

![javafx-hierarchy](/programming_languages/javafx/resources/javafx.png)

- `VBox`: for grouping elements vertically
- `HBox`: for grouping elements horizontally
- `FlowPane`: for grouping elements horizontally + responsive (same behaviour as a flex container with wrap: true)
- `Group`:
- `TextFlow`: for grouping several `Text` components
- `StackPane`: for reserving a space with a specific shape (cirlce, grid...)
- `GridPane`: for organizing components into a grid (= a two dimensional array)
- `BorderPane`: for setting components at **center**, **top**, **bottom**, **left** and **right** of the window

## Controls

A controlled component is a component which handle an event.

event: action triggered by a user.

Some examples:
- `RadioButton`
- `ImageView`
- `Button`
- `Checkbox`

**Additional Note**: It is possible to add icons to controls:
```java
ImageView iconView = new ImageView(im);
Button myBtn = new Buton("Click here!", iconView);
```

myBtn **is labeled** with the text "Click here"

## Events

Event: Interaction human-machine through a component.

For each event, think of the following points:
- Who will trigger the event?
- How the event will be triggered?
- What happens after the event is triggered?

3 important properties:
- Event Source (where does it come from?) [example: mouse]
- Event Target (on which element of the interface the event happened?) [example: button]
- Event Type (what kind of event happened?) [example: mouse clicked, mouse pressed, mousse released]

(The example above refers to a click on a button)

- `Event` class allows to **handle events**
- `EventHandler` interface is used to  **handle a specific event** (Gestionnaire d'évènements)
- `EventTarget` interface is used to **target a specific Node**
- `EventType` class which represents the **kind of event** (mouse click, key released...)

Events are triggered and then propagated through the `Event Dispatch Chain`. 

In order to handle an event, we need an `Event Listener`. There are 2 options:
- Through an `EventHandler`: 
	- an `ActionEvent` is propagated from the mother class (Stage) to the child element (Button)
- Through an `EventFilter`: 
	- an `ActionEvent` event is propagated from the child element (Button) to the mother class (Stage)
**Keep in mind that you should always use a filter because it is faster for bigger scene graph**

```java
// Creating the mouse event handler 
EventHandler<MouseEvent> eventHandler = new EventHandler<MouseEvent>() { 
   @Override 
   public void handle(MouseEvent e) { 
      System.out.println("Hello World"); 
      circle.setFill(Color.DARKSLATEBLUE);  
   } 
};   
// Adding event Filter (faster than Handler)
Circle.addEventFilter(MouseEvent.MOUSE_CLICKED, eventHandler);

// You use a filter OR a handler (not both at the same time)

// Adding event Handler (slower than Filter)
Circle.addEventHandler(MouseEvent.MOUSE_CLICKED, eventHandler);
```

Another method:
Here we create and add the eventHandler at the same time
```java
circle.setOnMouseClicked(new EventHandler<MouseEvent>() {
    @Override
    public void handle(MouseEvent event) {
        circle.setFill(Color.color(Math.random(), Math.random(), Math.random()));
        //circle.setRadius((int)(Math.random() * 41 + 20));
        title.setText("Ohh !!! my color has changed!!!");
    }
});
```

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

## Design Patterns 

### MVC (Model View Controller)

The Architecture is **theorical**. The MVC Structure is **real**: it is a **design pattern** (=patron de conception [FR]). It relies on different files/servers for each role (Model, View, Controller).

**It's a design pattern that separates application logic into three interconnected components: the Model (data), the View (user interface), and the Controller (intermediary).**

It relies on the Three-Tier Architecture.

- `Model`: Data Management
- `Controller`: Link between Model and View / Event handling (en français: Partie Métier)
- `View`: User Interface

Partie Métier d'une Application: partie chargée d'appliquer les règles applicatives/ de gestion.

![MVC](/programming_languages/javafx/resources/mvc.png)

**Ruby on Rails, ASP.NET, Django** use this design pattern.

### MVP (Model View Presenter)

**MVP (Model-View-Presenter): It's similar to MVC, but the key difference is that the Presenter component acts as a bridge between the Model and View, handling all the presentation logic.**

**Google Webkit Development, some framework in Android Development** use this design pattern.

### MVVM (Model-View ViewModel)

**MVVM (Model-View-ViewModel): It's similar to MVP, but with the added concept of data binding. The ViewModel component is responsible for exposing the data from the Model in a way that can be easily bound to the View, reducing the need for manual coding to update the UI.**

**Angular** uses this architecture in order to use **data binding**.

## Examples

### Login Interface

![Login](/programming_languages/javafx/resources/login.png)

```java
public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {
			StackPane root = new StackPane();
			
			Label emailLabel = new Label("Email");
			emailLabel.getStyleClass().add("label");
			emailLabel.setMinWidth(70);
			TextField emailInput = new TextField();
			emailInput.setMaxSize(150, 20);
			HBox emailContainer = new HBox();
			emailContainer.setAlignment(Pos.CENTER);
			emailContainer.getChildren().addAll(emailLabel, emailInput);
			
			Label pwdLabel = new Label("Password");
			pwdLabel.getStyleClass().add("label");
			pwdLabel.setMinWidth(70);
			
			PasswordField pwdInput = new PasswordField();
			//pwdInput.setMaxSize(150, 20);
			pwdInput.setPromptText("Your password");
			HBox pwdContainer = new HBox();
			pwdContainer.setAlignment(Pos.CENTER);
			pwdContainer.getChildren().addAll(pwdLabel, pwdInput);
			
			HBox formBtnContainer = new HBox();
			Button submitBtn = new Button("Submit");
			submitBtn.getStyleClass().add("btn");
			submitBtn.setMinWidth(50);
			Button clearBtn = new Button("Clear");
			clearBtn.getStyleClass().add("btn");
			clearBtn.setMinWidth(50);
			formBtnContainer.getStyleClass().add("btn");
			formBtnContainer.setAlignment(Pos.CENTER);
			formBtnContainer.getChildren().addAll(submitBtn, clearBtn);
			
			VBox formContainer = new VBox();
			formContainer.setAlignment(Pos.CENTER);
			formContainer.getChildren().addAll(emailContainer, pwdContainer, formBtnContainer);
			
			root.getChildren().add(formContainer);
			root.setId("body");
			Scene scene = new Scene(root,400,400);
			// CSS
			scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());
			primaryStage.setScene(scene);
			primaryStage.setTitle("Authenticaton");
			primaryStage.show();
		} catch(Exception e) {
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		launch(args);
	}
}
```

### Lampbook

![Lampbook](/programming_languages/javafx/resources/lampbook.png)

```java
public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {
			BorderPane root = new BorderPane();
			
			// Header
			Image logo = new Image(getClass().getResource("lampbook.png").toExternalForm());
			ImageView logoView = new ImageView();
			logoView.setImage(logo);
			logoView.setFitWidth(50);
			logoView.setPreserveRatio(true);
			logoView.setSmooth(true);
			logoView.setCache(true);
			logoView.getStyleClass().add("header-logo");
			
			TextField searchBar = new TextField();
			searchBar.setPromptText("Rechercher un article sur les lampadaires");
			searchBar.setPrefWidth(300);
			searchBar.setStyle("-fx-background-radius: 20;");
			searchBar.getStyleClass().add("searchbar");
			
			HBox header = new HBox(logoView, searchBar);
			header.setAlignment(Pos.CENTER);
			header.setSpacing(20);
			header.setPrefHeight(100);
			header.setStyle("-fx-background-color: #949BEE;");
			root.setTop(header);
			
			// Center
			Text article = new Text("Les lampadaires sont des éléments importants dans notre environnement quotidien. Ils nous fournissent de la lumière la nuit, améliorant ainsi notre sécurité et facilitant les déplacements. Les lampadaires modernes sont de plus en plus efficaces en matière d'éclairage et de consommation d'énergie, grâce à l'utilisation de technologies LED avancées.\r\n"
					+ "\r\n"
					+ "Cependant, les lampadaires classiques peuvent consommer beaucoup d'énergie et contribuer à l'empreinte carbone de notre société. Heureusement, les gouvernements et les entreprises sont de plus en plus conscients de l'importance de la transition vers des solutions durables en matière d'éclairage public.\r\n"
					+ "\r\n"
					+ "De nouveaux types de lampadaires, tels que les lampadaires solaires, sont maintenant disponibles sur le marché. Ceux-ci utilisent l'énergie solaire pour produire de la lumière la nuit, réduisant ainsi considérablement les coûts énergétiques et environnementaux.\r\n"
					+ "\r\n"
					+ "En conclusion, les lampadaires jouent un rôle crucial dans notre vie quotidienne et le développement de solutions plus durables est essentiel pour un avenir plus soutenable.");
			article.setWrappingWidth(500);
			
			Image articleImg = new Image(getClass().getResource("lamp.jpg").toExternalForm());
			ImageView articleView = new ImageView();
			articleView.setImage(articleImg);
			articleView.setFitWidth(700);
			articleView.setPreserveRatio(true);
			articleView.setSmooth(true);
			articleView.setCache(true);
			
			SplitPane feed = new SplitPane(article, articleView);
			feed.setMaxWidth(30);
			Label articleTitle = new Label("Les Lampadaires dominent-ils secrètement le monde ?");
			articleTitle.setStyle("-fx-font: 30 roboto;");
			
			Label authorArticle = new Label("Auteur de l'article: William Madié - Lamp Specialist and CEO at RisingLamp&Co");
			authorArticle.setStyle("-fx-font: 15 roboto;");
			authorArticle.setAlignment(Pos.CENTER_RIGHT);
			
			Image likesArticle = new Image(getClass().getResource("love.png").toExternalForm());
			ImageView likesView = new ImageView();
			likesView.setImage(likesArticle);
			likesView.setFitWidth(40);
			likesView.setPreserveRatio(true);
			likesView.setSmooth(true);
			likesView.setCache(true);
			
			Label likeNumber = new Label("5213 personnes aiment cet article");
			
			HBox bottomArticle = new HBox(likesView, likeNumber, authorArticle);
			bottomArticle.setAlignment(Pos.CENTER);
			bottomArticle.setSpacing(30);
			
			VBox articleContainer = new VBox(articleTitle, feed, bottomArticle);
			articleContainer.setAlignment(Pos.CENTER);
			articleContainer.setSpacing(20);
			root.setCenter(articleContainer);
			
			// Left
			Label friendsPanelTitle = new Label("Mes amis");
			friendsPanelTitle.setStyle("-fx-font: 20 roboto;");
			ListView<String> friends = new ListView<String>();
			ObservableList<String> items = FXCollections.observableArrayList("Emma", "Katia", "Simon", "Marius", "Yann", "Aurélie", "Chadi", "Kenz", "Linda", "Noah", "Fabien", "Adrien", "Bilele", "Yewon", "Joseph", "Kévin", "Pascal", "Tefy", "Ramzi", "Louis", "Adam", "Wassim");
			friends.setItems(items);
			
			VBox friendsPanel = new VBox(friendsPanelTitle, friends);
			friendsPanel.setAlignment(Pos.CENTER);
			
			root.setLeft(friendsPanel);
			
			// Right
			Label btnPanelTitle = new Label("Navigation Menu");
			btnPanelTitle.setStyle("-fx-font: 20 roboto;");
			Button btn1 = new Button("Envoyer un message");
			Button btn2 = new Button("Ecrire un article");
			Button btn3 = new Button("Ecrire un article sur les lampadaires");
			Button btn4 = new Button("S'offusquer des lampadaires illégaux");
			btn1.setStyle("-fx-background-radius: 10;");
			btn2.setStyle("-fx-background-radius: 10;");
			btn3.setStyle("-fx-background-radius: 10;");
			btn4.setStyle("-fx-background-radius: 10;");
			VBox btnPanel = new VBox(btnPanelTitle, btn1, btn2, btn3, btn4);
			btnPanel.setAlignment(Pos.CENTER);
			btnPanel.setSpacing(20);

			root.setRight(btnPanel);
			
			// Bottom
			Label connectedAs = new Label("Connecté en tant que William Madié");
			connectedAs.setStyle("-fx-font: 15 roboto;");
			connectedAs.setAlignment(Pos.BOTTOM_RIGHT);
			root.setBottom(connectedAs);
			
			Scene scene = new Scene(root,1700,800);
			// CSS
			scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());
			primaryStage.setScene(scene);
			primaryStage.setTitle("Lampbook - Home");
			primaryStage.show();
		} catch(Exception e) {
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		launch(args);
	}
}
```