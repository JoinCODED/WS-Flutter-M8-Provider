12. Install the `go_router` package and initiate your routes:

```dart
void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => NoteProvider(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      routeInformationParser: _router.routeInformationParser,
      routerDelegate: _router.routerDelegate,
    );
  }

  final _router = GoRouter(
    routes: [
      GoRoute(
        path: '/',
        builder: (context, state) => HomePage(),
      ),
      GoRoute(
        path: '/note',
        builder: (context, state) => NotePage();
      ),
    ],
  );
}
```

Now, we will learn how to use the route params mainly for the usage of flutter web.

13. In your second route `/note`, add a param by using a colon and the param that helps us identify each note object. You can use the **id** since it is a unique value!

```dart
      GoRoute(
        path: '/note/:noteId',
        builder: (context, state) => NotePage();
      ),
```

The param is always of type `String`, that is why we need to parse it to an `int` to be able to use it.

```dart
      GoRoute(
        path: '/note/:noteId',
        builder: (context, state) {
            // 1
          final id = int.parse(state.params["noteId"] ?? "");
          return NotePage();
        },
      ),
```

We accessed the param using the `state.params` object and passed the param named `noteId`.

14. In the `note_provider.dart` file, create a function in the that takes an `id` and returns a note object.

```dart
  Note getNote({required int id}) {
    return notes.firstWhere((note) => note.id == id);
  }
```

15. Call the provider and `getNote` function, and pass the `id` to it:

```dart
      GoRoute(
        path: '/note/:noteId',
        builder: (context, state) {
          final id = int.parse(state.params["noteId"] ?? "");
          final note =
              Provider.of<NoteProvider>(context, listen: false).getNote(id: id);
          return NotePage();
        },
      ),
```

16. Create a variable in the `note_page` and generate a constructor:

```dart
  final Note note;
  const NotePage({Key? key, required this.note}) : super(key: key);
```

17. Pass the note object to the `note_page` page:

```dart
      GoRoute(
        path: '/note/:noteId',
        builder: (context, state) {
          final id = int.parse(state.params["noteId"] ?? "");
          final note =
              Provider.of<NoteProvider>(context, listen: false).getNote(id: id);
          return NotePage(note: note);
        },
      ),
```

18. In your `note_list_tile.dart` file, wrap the widget in an `InkWell` to get the `onTap` method, push the user to the `NotePage`, and don't forget to include the **id**.

```dart
class NoteListTile extends StatelessWidget {
  final Note note;
  const NoteListTile({Key? key, required Note this.note}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Card(
      child: InkWell(
        onTap: () => GoRouter.of(context).push('/note/${note.id}'),
        child: ListTile(
          title: Text(note.title),
          leading: Icon(
            Icons.sticky_note_2_outlined,
            color: Colors.yellow.shade600,
          ),
        ),
      ),
    );
  }
}
```

19. Open the app in your browser using the following command:

```dart
flutter run -d chrome
```

20. Add 3 notes and try to access them using the url as shown below:

`/note/1`
`/note/2`
`/note/3`

![img](https://lh6.googleusercontent.com/L3bE8f6cnDg7_8l84y4L2htEF6njv3GjgAA7EIgWdCNGmFavvkDSvVCadR7Q8j8_DqecmzYtE3QsboME_y-qdQwzJtDbhmiIvWY-NlyINJbmhYk7ilBFDfBiiPbXW518rURggRRz)

