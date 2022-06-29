What do the terms **state** and **state management** mean?

- **State** is the data that can be read synchronously when the widget is built. It might change overtime during the widget lifecycle. To change your widget, you need to update the state object using the **setState()** function available for stateful widgets. **setState()** sets properties of the state object, which triggers the update to the UI.
- **State management** is the process that helps you to share your application state between screens across the app. In simpler words, it is responsible for managing the application state.

Why are we not able to fully depend on the **setState()** function?

- We used to share data between pages using the constructor, but the bigger the application gets, the harder and more complicated this process becomes.
- Using **setState()** everywhere causes unnecessary rerendering, once **setState()** is triggered from the parent, it renders all its children, their sub-children, and so on.
- You cannot specifically render a particular child or children, if there are two siblings that belong to a parent, it is impossible to render one child from another until the parent is involved which in turn renders both children.
- **State management** helps you to keep your code well-structured, and it becomes easy to read and maintain.

1. Fork and clone the project from [GitHub](https://github.com/Northwest-content/flutter_notes_app/tree/main/notes_app), or continue working on the previous project if you already have it.

2. Add the **Provider** package in the **pubspec.yaml** file below the **dependencies**:

   ```yaml
   dependencies:
     flutter:
       sdk: flutter
     provider: ^6.0.2
   ```

**Good practice:** To build a large scalable application, it is better to separate the logic from the UI.

3. In the **lib** folder, create another folder called "**providers**" , which contains the files that are responsible for the app logic.

![img](https://lh3.googleusercontent.com/7L9CGiSic-kMyLUdwJDsoirvZLazTh_7O9k68pIJ7mtLr2tc9qKKAlblvkYnC95csBXbMrnVIaz-OEu1hPYLPYHbsUnr-03SZSNma3liqNz7QBJFmHucSrV-Dv-ZfWXofyCca0xl)

Let's first figure out where the logic of our app is right now.

![img](https://lh4.googleusercontent.com/eUjukQxmaBESf-CA_VmTNEJAc9D-Ppd5RpctRoWQLOTnTDm2yNBR4TdhaZvrMjv2ISgZ77u55Ja8iUMos7O-cD_UadiymORDR4Jg6Kxj4b1GrbtoSAEcvzqEy9AGoTXmpNYWxNhu)

You will find the logic processes we developed before placed in the **home_page.dart** file.

4. Inside the **providers** folder, create a new file named **note_provider.dart**.
5. Inside the **note_provider.dart** file, create a new class named **NoteProvider**, extend the **ChangeNotifier** class, and do not forget to import the **flutter/material.dart** file

```dart
import 'package:flutter/material.dart';


class NoteProvider extends ChangeNotifier {

}
```

6. Inside the **home_page.dart** file, cut the **addNote()** function, which represents the logic, paste it inside the **NoteProvider** class, and do not forget to import all the necessary files.

![img](https://lh5.googleusercontent.com/yPb_FTtGX7F8nrAAldRmMOKq4OG0vo333f8YmOYZXtGjkbzsNdxVI1XYdVHEqq5Luv2rYau3AfwsyN7sh7af2KCacrsjCwMLui6GLftqfhNbNQ9kFzgBzqO2nJ9LzQMyW6quXFPH)

With the previous approach, we used to call the **setState()** method to notify the **StateFulWidget** to rebuild the state, but with the **state management** (provider), there is another way to do that, which is using the **notifyListeners** method that comes from the **ChangeNotifier** class.

7. Replace the **setState** method inside the **addNote** function with the **notifyListeners**.

```dart
void addNote() {
    var note = Note(
      id: notes.isNotEmpty ? notes[notes.length - 1].id + 1 : 1,
      title: _titleTextEditingController.text,
      body: _bodyTextEditingController.text,
    );

    notes.insert(0, note);

    notifyListeners(); // <- Here
  }
```

To get the value of both, the title and the body, you need to pass them as arguments to the **addNote()** function.

8. Pass the two named arguments (**title** & **body**) to the **addNote** function, and assign them to the title and body properties in the note object:

   ```dart
    void addNote({required String title, required String body}) {
       var note = Note(
         id: notes.isNotEmpty ? notes[notes.length - 1].id + 1 : 1,
         title: title,
         body: body,
       );

       notes.insert(0, note);

       notifyListeners();
   ```

   > Note: **String** type

After that, we have to use `ChangeNotifierProvider` which is the widget that provides an instance of a `ChangeNotifier` to its descendants, and we have to place it above the widgets that need to access it. In our case, the `home_page.dart` file needs access, which means `ChangeNotifierProvider` needs to be placed somewhere above that file, and the only widget that is above the home page is `MyApp`.

9.  In the `main.dart` file, import the `provider` package and the `NoteProvider` that we created, and wrap the `MyApp` with `ChangeNotifierProvider` that has a `create` property which creates a new instance when the widget is first built, as well as a `child` property that returns our main app:

```dart
import 'package:provider/provider.dart';
import 'package:flutter_notes_app_starter/providers/note_provider.dart';



void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => NoteProvider(),
      child: MyApp(),
    ),
  );
}
```
