Since the **ListView** widget is used inside the note app to display the values of the **notes** variable, this widget has to rebuild itself every time the user adds a new note inside the **notes** variable. That is why we used the **notifyListeners()** method inside the **addNote** function in the **NoteProvider** class.

![img](https://lh6.googleusercontent.com/nC3U3-tpn1vQ5ONZgWJulQSRdMaN152lMFyfCaQ_FPN2eNVbLtD7_Yws53gNOPh-FFQoL8Tn6SHDYdeQhkb-xOp2GtAwEEZ80Zi5X7qR800YuEjI0_nvkz6S_2lSoyjydPRW5JCo)

In addition to that, we need to access the **notes** variable that is inside the **NoteProvider** class, and use it inside the **ListView** widget.

11. Cut the **ListView.builder**, then use the **Consumer** widget, and inside the builder named argument return & paste the **ListView.builder** that you cut before.

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

> **Note:** The **notifyListeners()** method will rebuild the widget tree that the **Consumer** returns when it is called.

Alternatively, you can use `context.watch` to access the provider, and watch the changes:

```dart
    context.watch<NoteProvider>().notes
```

So our code will look like this:

```dart
    ListView.builder(
                shrinkWrap: true,
                physics: const NeverScrollableScrollPhysics(), // <- Here
                itemCount: context.watch<NoteProvider>().notes.length,
                itemBuilder: (BuildContext context, int index) {
                  return NoteListTile(
                    note: context.watch<NoteProvider>().notes[index],
                  );
                },
              )

```
