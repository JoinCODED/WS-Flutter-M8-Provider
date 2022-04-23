Install the `go_router` package and initiate your routes like we learned before:

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

22. Now we will learn how to use the route params mainly for the usage of flutter web.

In your second route, `/note` add a param to the route by using a colon and the param that will help us identify each note object, we can use the **id** since it's a unique value!

```dart
      GoRoute(
        path: '/note/:noteId',
        builder: (context, state) => NotePage();
      ),
```

23. The param will always be of type `String`, we need to parse it to an `int` to be able to use it.

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

We accessed the param using the `state.params` object and then pass the param name `noteId`.

Now we need to create a function in our provider that takes an `id` and returns a note object:

In your `note_provider.dart`:

```dart
  Note getNote({required int id}) {
    return notes.firstWhere((note) => note.id == id);
  }
```

Back to your `main.dart` file, call our provider and call this function and pass the `id` to it:

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

Then like we learned before, we will create a variable in our `note_page` and generate a constructor:

```dart
  final Note note;
  const NotePage({Key? key, required this.note}) : super(key: key);
```

And we will pass the note object to our page:

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

Finally, in your `note_list_tile.dart` wrap your widget in an `InkWell` widget to get the `onTap` method and push the user to the `NotePage` and don't forget to include the **id** because it's our way of identifying which note the user wants!

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

Open the app in your browser using the following command:

```dart
flutter run -d chrome
```

And add 3 notes then try to access them using the url by going to:

`/note/1`
`/note/2`
`/note/3`

![img](https://lh6.googleusercontent.com/L3bE8f6cnDg7_8l84y4L2htEF6njv3GjgAA7EIgWdCNGmFavvkDSvVCadR7Q8j8_DqecmzYtE3QsboME_y-qdQwzJtDbhmiIvWY-NlyINJbmhYk7ilBFDfBiiPbXW518rURggRRz)

![img](https://lh6.googleusercontent.com/-3urOR1FVaBWCyVe5MkximX1SMUWaqt5XQ8kDabiVg3l5XvTqPpMkGME3mPmbGjv4IZlxXTPQ10x81_tv0Kd7CErUL8xjC8uzAS9jRofYcPrDifemnDTPbEljLQ53dPsM5QsOjJY) -->
