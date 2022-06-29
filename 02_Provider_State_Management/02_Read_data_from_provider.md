To use these data inside the **home_page.dart** file, you need to import the **provider** package, and the **NoteProvider**.

```dart
import 'package:flutter_notes_app_starter/providers/note_provider.dart';
import 'package:provider/provider.dart';
```

10. Use the **provider.of** method in the **home_page.dart** file to call the **addNote** function from the **note_provider.dart** file:

```dart
IconButton(
          iconSize: 32,
          icon: Icon(
            Icons.add_box,
            color: Theme.of(context).primaryColor,
          ),
          onPressed: () {

      // Here
      final notesProvider = Provider.of<NoteProvider>(context, listen: false);
            notesProvider.addNote(
                  title: _titleTextEditingController.text,
                  body: _bodyTextEditingController.text,
                );
          },
        ),
```

> **Note:** The **Provider.of** method needs a type, which is the provider that you created before. It takes two arguments: The `context` and an optional boolean argument `listen`.
> If you assign the `listen` to false, it helps you to access the methods and variables inside the provider file without causing the widget to rerender.
> In our case, we want to access the title and body variables, but at the same time, we do not want this widget to rerender every time the user types something, therefore we set listen to false.

Alternatively, you can use `context.read` to access the provider and call the function:

```dart
    context.read<NoteProvider>().addNote(
      title: _titleTextEditingController.text,
      body: _bodyTextEditingController.text,
    );
```

Which is equivalent to:

```dart
    Provider.of<NoteProvider>(context, listen: false).addNote(
      title: _titleTextEditingController.text,
      body: _bodyTextEditingController.text,
    );
```
