3. Inside the **home_page.dart** file, replace the `// TODO: #2 note list` with the code below to create a list variable that stores the notes inside.

```dart
var notes = [];
```

4. Replace `// TODO: #3 add note function` with the code below to create a function named **add** that helps us to insert a **note** object into the **notes** list.

```dart
 void addNote() {

    // a
    var note = Note(
      // b
      id: notes.isNotEmpty ? notes[notes.length - 1].id + 1 : 1,
      //c
      title: _titleTextEditingController.text,
      body: _bodyTextEditingController.text,
    );

    // d
    notes.insert(0, note);


    // e
    setState(() {});
  }
```

> > a. We used the **Note** class that we created inside the **models** folder to create a **Note** object.
> > b. We added a condition to check if the list is empty, if so, the id of the new note will be assigned to `1`, otherwise, it will take the id of the last element in the list increased by `1`.
> > c. We assigned the title and body of the note to the **\_titleTextEditingController.text** & **\_bodyTextEditingController.text** value.
> > d. We used the **insert** method which takes two arguments:
> > The first argument is the position of the object inside the **note** list.
> > The second argument is the object that you want to insert into the **notes** list, which is the **note** object that we created before.
> > e. We used the **setState** method that came from the **StatefulWidget** to tell Flutter to rebuild its state.

5. Replace the `// TODO: #4 Add ListView builder` with the code below to display the notes using the **ListView.builder** widget:

```dart
ListView.builder(
              // #a
              itemCount: notes.length,
              itemBuilder: (BuildContext context, int index) {

                // #b
                return NoteListTile(
                  note: notes[index],
                );
              },
            ),
```

> > a. The **ListView.builder** requires two named arguments: The first one is **itemCount** which takes the length of the **notes** list, and the second one is `itemBuilder` which returns a widget.
> > b. The **itemBuilder** returns the **NoteListTile** widget which comes from the **note_list_tile.dart** file and is used to display the values of the **notes** list.

6. Import **note_list_tile.dart**.

   ```dart
   import '../widgets/note_list_tile.dart';
   ```

⚠️ You got an `Exception` because you used the **ListView** widget inside the **Column** widget.

![img](https://lh3.googleusercontent.com/jJ0mvg2hp6Sas7NpTeh72SZxstoXyk7UQXR6RKsAbR4imKbg7LRP9-F-ct7qeuDLLYbteDhrQ1nfCofxeUALpcoACmKB-hznCKfQZL1p-5onJD9ROwAl5CGlU6-pqmjNeupGgehB)

To solve this issue, you have to add the **shrinkWrap** named argument inside the `ListView` widget. This named augment changes the behavior of the `ListView` widget to have a fixed height.

7. Add the **shrinkWrap** named argument inside the `ListView` widget, and set its value to true.
8.

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

8. Add `physics: const NeverScrollableScrollPhysics(),` named argument to disable the scrolling inside the **ListView**.

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

9. Pass the `addNote()` function to the `onPressed` button in the `IconButton`:

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

**Finally!**

![img](https://lh4.googleusercontent.com/VsX1QoUtpmsfmJ4lE1mtxQoRfJBNRYGfMxz1Ad3KUdAQkjq-pZTeezq0Q-RpO9ZTEV4-_ri1o-ayEF2geqYeFiGp8bII8oVnzKzVvcKxIvGiTMahCKXYRFH9ALwLAWqTb_qKlTIm)

**Note: You can find the full source code [here](https://github.com/Northwest-content/flutter_notes_app/tree/main/notes_app).**
