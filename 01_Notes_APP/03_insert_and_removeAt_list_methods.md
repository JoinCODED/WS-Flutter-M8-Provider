# **insert** & **removeAt** list methods

5. Inside the **home_page.dart**, we will create a notes list that will store our notes inside it. So, replace the `// TODO: #2 note list` with

```dart
var notes = [];
```

6. After we created the **notes** list, we will need to create the **add** function, which will help us to insert a **note** object inside the **notes** list. So, replace the `// TODO: #3 add note function` with

```dart
 void addNote() {

    // 1
    var note = Note(
      id: notes.isNotEmpty ? notes[notes.length - 1].id + 1 : 1,
      title: _titleTextEditingController.text,
      body: _bodyTextEditingController.text,
    );

    // 2
    notes.insert(0, note);


    // 3
    setState(() {});
  }
```

1. First, we need to create a **Note** object, and to do that we used the **Note** class that we created inside the **models** folder. Also, we provided its values by using the **\_titleTextEditingController** value & **\_bodyTextEditingController** value.

We need to generate an **id** for our note, the **id** should be unique for each note object, so we will take the last **id** in our list, then increase it by one, but first we will check if the list is empty, and if so, we will set the **id** to be equal to `1`.

2. Here, we used the **insert** method which takes two arguments, the first argument is the position of the object that you insert inside the **notes** list. The second argument is the object that you want to insert into the **notes** list; and we passed the **note** object that we created before.
3. After we inserted the note object inside the notes list, we need to tell Flutter to rebuild its state, and to do that we used the **setState** method that came from the **StatefulWidget**.

4. After completing the additional logic, we need a way to display the notes; and for that, we will use the **ListView.builder** widget. So, replace the `// TODO: #4 Add ListView builder` with

```dart
ListView.builder(

                  // #1
                  itemCount: notes.length,
                  itemBuilder: (BuildContext context, int index) {

                    // #2
                    return NoteListTile(
                      note: notes[index],
                    );
                  },
                ),
```

1. The **ListView.builder** will need two important named arguments, the first one is **itemCount**, and here we take the length of the notes list since we will use this notes list to display its contents inside the **ListView.builder** widget.
2. Here, we returned the **NoteListTile** widget for the **itemBuilder** method **ListView** widget. We created this tile widget inside the **note_list_tile.dart** file, and we will use it to display the values of the **notes** list.

3. Don’t forget to import **note_list_tile.dart** since we used it inside the **ListView** widget.

   ```dart
   import '../widgets/note_list_tile.dart';
   ```

4. We will get an Exception because we used the **ListView** widget inside the **Column** widget.

   ![img](https://lh3.googleusercontent.com/jJ0mvg2hp6Sas7NpTeh72SZxstoXyk7UQXR6RKsAbR4imKbg7LRP9-F-ct7qeuDLLYbteDhrQ1nfCofxeUALpcoACmKB-hznCKfQZL1p-5onJD9ROwAl5CGlU6-pqmjNeupGgehB)

To solve this issue, add **shrinkWrap** named argument inside the ListView widget, and keep its value to true. This named augment will change the behavior of the ListView widget, so it has a fixed height, and the error will disappear.

```dart
ListView.builder(

                  shrinkWrap: true, // <- here
                  itemCount: notes.length,
                  itemBuilder: (BuildContext context, int index) {
                    return NoteListTile(
                      note: notes[index],
                    );
                  },
                )
```

Also, add `physics: const NeverScrollableScrollPhysics(),` named argument. This named argument will disable the scroll inside the **ListView** because the scroll will come from its parent widget which is the **SingleChildScrollView**.

```dart
 ListView.builder(
                  shrinkWrap: true,
                  physics: const NeverScrollableScrollPhysics(), // <- Here
                  itemCount: notes.length,
                  itemBuilder: (BuildContext context, int index) {
                    return NoteListTile(
                      note: notes[index],
                    );
                  },
                )
```

10. After completing the additional logic, we need to link this additional logic with the add button widget.

    So, change the **onPressed** named argument that inside the **IconButton** with

    ```dart
    IconButton(
                          iconSize: 32,
                          icon: Icon(
                            Icons.add_box,
                            color: Theme.of(context).primaryColor,
                          ),
                          onPressed: () {
                            addNote();  // <- Here
                          },
                        )
    ```

    ![img](https://lh5.googleusercontent.com/JuQllaI9HpwLkjkkAGhz9ua8R3TVA52vS_obpbf3pxpsjtihIsMBSPZFjemyha_0Pkj07cJIoINTKJgft8-xkrRnR46CoMerRi4IUrfqx3T82Zy8nNol2FUXrcZ50Qq891ci7tDd)

**Finally,**

![img](https://lh4.googleusercontent.com/VsX1QoUtpmsfmJ4lE1mtxQoRfJBNRYGfMxz1Ad3KUdAQkjq-pZTeezq0Q-RpO9ZTEV4-_ri1o-ayEF2geqYeFiGp8bII8oVnzKzVvcKxIvGiTMahCKXYRFH9ALwLAWqTb_qKlTIm)

**Note: You can find the full source code.**

> https://github.com/Northwest-content/flutter_notes_app/tree/main/notes_app
