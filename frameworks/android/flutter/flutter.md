# Flutter

## Table of Contents

- [Introduction](#introduction)
- [The Dart Language](#why-does-flutter-use-the-dart-language)
- [Flutter Basics](#flutter-basics)
    - [Flutter CLI](#flutter-cli)
    - [Flutter Project Structure](#flutter-project-structure)
    - [Main.dart](#maindart)
- [Flutter Principles](#flutter-principles)
    - [Widgets](#widgets)
    - [Stateless VS Stateful Widgets](#stateless-vs-stateful-widgets)
    - [Isolates](#isolates)
- [Type Specificities](#type-specificities)
- [Assets](#assets)

## Introduction

Flutter is a framework based on the Dart language. It is a rising language used for building mobile, desktop and web applications from a single code base.

Flutter offers a productive development:

- it allows to quickly reload and see new changes as we code.
- it provides static analysis to find errors without even executing code

## Why does Flutter use the Dart Language

- Dart supports **asynchronous operations** (the computer is able to complete work while waiting for another operation to finish)
    - Fetching data
    - Writing to a database
    - Reading data from a file
- Dart does not use shared-memory threads. Instead it uses **isolates** which are less likely to introduce new errors due to shared-state concurrency.
- Dart is optimized for building UI for each platform
- Dart allows to customize everything

## Flutter Basics

### Flutter CLI

The Flutter CLI is an unavoidable development tool. It helps the developer to set up his environment easily, to use the hot reload function, to connect a mobile device for development needs, to quickly see what dependency is missing and more.

Here are the essential commands:

Analyse and show problems in current development environment
```bash
flutter doctor

# Output:

Doctor summary (to see all details, run flutter doctor -v):
[√] Flutter (Channel stable, 3.7.0, on Microsoft Windows [version 10.0.22000.1455], locale fr-FR)
[X] Windows Version (Unable to confirm if installed Windows version is 10 or greater)
[√] Android toolchain - develop for Android devices (Android SDK version 33.0.1)
[√] Chrome - develop for the web
[√] Visual Studio - develop for Windows (Visual Studio Build Tools 2019 16.11.15)
[√] Android Studio (version 2022.1)
[√] IntelliJ IDEA Ultimate Edition (version 2021.3)
[√] VS Code
[√] VS Code, 64-bit edition (version 1.71.2)
[√] Connected device (4 available)
[√] HTTP Host Availability

! Doctor found issues in 1 category.
```

Create a new project
```bash
flutter create
```

Run the Flutter app on an attached device
```bash
flutter run
```

Run Flutter unit tests
```bash
flutter test
```

List all connected devices
```bash
flutter devices
```

### Flutter Project Structure

![project-structure](/frameworks/android/flutter/resources/flutter-structure.png)
    
- `lib`: contains the main source code for the project
    - `main.dart`: the entry point of the Flutter Application
- `assets`: includes any static files used in the project, such as images, fonts, and others
- `test`: holds test cases for the project
- `build`: stores generated build artifacts
- `ios` and `android`: platform-specific code and configuration files for building on iOS and Android platforms respectively.
- `pubspec.yaml`: the main configuration file for the Flutter project, specifying dependencies, assets, and other information.

### Main.dart

The `main.dart` file is known as the entry point of the Flutter application. It contains the main widget of the Flutter Application:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  MyApp({super.key});

  // Root Widget
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Application',
      theme: ThemeData(
        primarySwatch: Colors.orange,
      ),
      home: const MyHomePage(title: 'Flutter App Home Page'),
    );
  }
}

// The Home Page Configuration for the State
class HomePage extends StatefulWidget {
  const HomePage({super.key});

  // Fields in a Widget subclass are always marked "final"
  final String title;

  @override
  State<HomePage> createState() => _HomePageState();
}

// State Object (Fields affect the way the widget looks)
class _HomePageState extends State<HomePage> {
  // A private attribute/field starts with "_"
  int _counter = 0;

  // A method which increments "_counter" and re-render the Widget
  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  // Method used to re-render the Widget (for example when setState() is called)
  @override
  Widget build(BuildContext context) {
    return Scaffold();
  }
}
```

## Flutter Principles

### Isolates

**isolate**: thread that has an event loop that continuously processes events in its own memory space.

### Widgets

In Flutter, everything is a **Widget**. There are **14 different categories of Widgets**:
1. **Layout**: Container used to display other Widgets such as `Column()`, `Center()`
2. **Assets, Images, Icons**: Assets-related Widgets which handle **images** and **icons**.
3. **Painting and Effects**: Set of Widgets that apply visual changes (=filters) to their child Widgets.
4. **Text**: Widget which display a text
5. **Styling**: Widget which handle the theme, responsiveness and sizing of the app.
6. **Animation and Motion**: Widgets that add animation to other widgets.
7. **Scrolling**: Widget that make another Widget scrollable even if it is not by default.
8. **Material Component**: Set of Widgets following Android design guidelines by Google.
9. **Cupertino**: iOS designed Widgets.
10. **Async**: Async Functionality in the Flutter App.
11. **Basics**: Necessary Widgets for the development of any Flutter App.
12. **Input**: Input Functionality in the Flutter App.
13. **Accessibility**: Set of Widgets that make a Flutter App more easily accessible.
14. **Interaction Models**: Widgets that handle touch events

### Stateless VS Stateful Widgets

A widget is either **stateful** or **stateless**. 

- On the one hand, if a widget can change (when the user interacts with it, for instance), then it is **stateful**. (`Checkbox`, `Radio`, `Slider`, `TextField`)
- On the other hand, a **stateless** widget never changes (`Icon`, `IconButton`, `Text`...)

But how does Flutter know when a widget has changed?

A widget has a **state** which is stored in a **State** object. So the widget is composed of two separated elements:
- a State (a bunch of values which can change)
- an Appearance

When a widget's state changes, the State object calls `setState()`. This function tells the framework to redraw the widget:

![appearance-state](/frameworks/android/flutter/resources/appearance-state.png)

An example of action that needs to use `setState()`:
Here we have a Switch Button that once activated changes the value of a boolean. We change this value inside `setState()` so that Flutter knows it has to redraw the widget
```dart
Switch(
    value: isSwitched,
    onChanged: (bool newBoolean) {
      setState(() {
        isSwitched = newBoolean;
      });
    }),
```

### Basic Stateless Widget

An example for a file called `profile_page.dart`
```dart
import 'package:flutter/material.dart';

class ProfilePage extends StatelessWidget {
  const ProfilePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

### Scaffold

It is the main container of a page. It has three main attributes:
- appBar
- body
- navigationBar

## Type Specificities

- **Nullable value**: `bool?` means that a function can take `true`, `false` or `null`

## Assets

In order to use assets in our Flutter project, we need to tell Flutter where our assets are located. We do that by removing comments in the `pubspec.yml` file (see below):
```yaml
assets:
    - images/
```

## Styles

Make a Container take all available width:
```dart
width: double.infinity,
```

Center a Text (VSCode shortcut): `right click` on the `Text` element. Select **refactor** and then **Wrap with Center**.