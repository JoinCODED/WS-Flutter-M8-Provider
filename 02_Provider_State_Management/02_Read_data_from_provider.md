# Read the data from the provider

18. Right now, we centered the data top of the tree widget, and to access it we need to use the **provider** package.

Since we are going to use this data inside the **home_page.dart** file, we need to import the **provider** package, and the **NoteProvider**.

Import the **provider** package inside the **home_page.dart** file,

```dart
import 'package:notes_app/providers/note_provider.dart';
import 'package:provider/provider.dart';
```

19. To use the **addNote** function that is inside the **note_provider.dart** file, use the **provider.of** method.

​ Then, go to the **IconButton** widget, and change the **onPressed** named argument to

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

> **Note:** the **Provider.of** method needs a type, which is the provider that you created before and it also takes two arguments, the `context` and an optional boolean argument `listen`, when you are accessing data and do not want the widget to be rerendered you should set `listen` to `false`; then you can access all variables and methods that you created inside the provider file. So, in our case we import the **addNote** method; this method needs two named arguments (**title** & **body**), and we used the **TextEditingController.text** values.
