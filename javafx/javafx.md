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

## Examples

### Login Interface

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