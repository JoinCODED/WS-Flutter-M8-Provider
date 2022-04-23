# Read the data & rebuilding the widget tree (Consumer widget)

Because inside the note app, we have used a **ListView** widget and this widget displays the values of the **notes** variable. When the user adds a new note inside the **notes** variable, we need to rebuild the **ListView** widget again. Because of this reason we used the **notifyListeners()** method inside the **addNote** function that is inside the NoteProvider class.

![img](https://lh6.googleusercontent.com/nC3U3-tpn1vQ5ONZgWJulQSRdMaN152lMFyfCaQ_FPN2eNVbLtD7_Yws53gNOPh-FFQoL8Tn6SHDYdeQhkb-xOp2GtAwEEZ80Zi5X7qR800YuEjI0_nvkz6S_2lSoyjydPRW5JCo)


20. Not only, we need to rebuild the widget tree, we also need to access the **notes** variable that is inside the **NoteProvider** class, and use it inside the **ListView** widget. So, the widget which will help us with accessing & rebuilding the widget tree is the **Consumer** widget.

Cut the **ListView.builder**, then use the **Consumer** widget, and inside the builder named argument return & paste the **ListView.builder** that you cut before.

```dart
    Consumer<NoteProvider>(
              builder: (context, notesProvider, child) => ListView.builder(
                shrinkWrap: true,
                physics: const NeverScrollableScrollPhysics(), // <- Here
                itemCount: notes.length,
                itemBuilder: (BuildContext context, int index) {
                  return NoteListTile(
                    note: notes[index],
                  );
                },
              ),
            )
```

21. Since we are using the **notes** variable inside the **ListView** widget, we will use the **notesProvider** argument

```dart
    Consumer<NoteProvider>(
              builder: (context, notesProvider, child) => ListView.builder(
                shrinkWrap: true,
                physics: const NeverScrollableScrollPhysics(), // <- Here
                itemCount: notesProvider.notes.length,
                itemBuilder: (BuildContext context, int index) {
                  return NoteListTile(
                    note: notesProvider.notes[index],
                  );
                },
              ),
            )
```

> **Note:** the **notifyListeners()** method will rebuild the widget tree that the **Consumer** widget returns when it's called.
