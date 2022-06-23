To display a floating button in the home screen, you can use the **FloatingActionButton** widget as shown in the screenshot.

![img](https://lh3.googleusercontent.com/fKdEk6ZavZPBMiIXW4j6Amf5klQpCkq1BdBieGUTwAeEnnwpN-pWKwDTwEXuyx4TWbY1jqqEoTaJbJxiass3zEqaVLeF8nssW72FEh2Wq4KjDCFrYYxLpXoXm7yfIWM-rxnCnF-i)

1. Inside the **home_page.dart** file, add the **floatingActionButton** named argument inside the **Scaffold** widget. This named argument takes a **FloatingActionButton** object.

![img](https://lh5.googleusercontent.com/H5ogw5RLbv-JYe_NcblkOAuczOKV3riBGYfgC7xG04AeIJiEG6bmiA6ewr6920KfvsMaHccaQOFcZxCTJho4gPVuzjddruMiDdx-5uWbZtTfNlFAcdmIdEAjnATzfe1MCJYYi58L)

The **FloatingActionButton** object requires two named arguments:

The first named argument is the **child**, it takes a widget. In our case, pass an **Icon** widget to display the add icon.

![img](https://lh6.googleusercontent.com/_Foqjf7A8bULDRrFuvhLoZgP7USMdUwwnviBso16QiN8F-Ds1vtfSAU_DgJd9Zz51t0yWK_aSx5v6VHcaVTiCJIGNgt8BYU1A4F3naXsG0T-rYf1zwgVpAnbjOWy4c0rnmvi-C8g)

```dart
FloatingActionButton(
          child: Icon(
            size: 30,
          ),
            Icons.add,
        )
```

The second named argument is **onPressed**. It takes a function that is called when the button is tapped.

2. Call the **addNote** function inside the **noteProvider**.

![img](https://lh3.googleusercontent.com/kYgvE5iLhBmlBHh0frEDRQrD8TBKLQFtVdNGNop_9sKl-2Su5NGICn_WyYBqnr3YPnjypdQaZ_BfimDLmr21R0EerCZqzuP6hvAFnuVN604j4L3-3y3uHOCR7a6YCETw9WVHvFCf)

```dart
FloatingActionButton(
          child: Icon(
            Icons.add,
            size: 30,
          ),

          // Here
          onPressed: () {
                      final notesProvider =
              Provider.of<NoteProvider>(context, listen: false);
          notesProvider.addNote(
              title: _titleTextEditingController.text,
              body: _bodyTextEditingController.text);

          },
        )
```

Another argument we can pass to this button is the **backgroundColor**. Set it to **primaryColor**.

```dart
FloatingActionButton(
          child: Icon(
            Icons.add,
            size: 30,
          ),
          backgroundColor: Theme.of(context).primaryColor, // <- Here
          onPressed: () {
          final notesProvider =
              Provider.of<NoteProvider>(context, listen: false);
          notesProvider.addNote(
              title: _titleTextEditingController.text,
              body: _bodyTextEditingController.text);
          },
        )
```

Once you run the app, you will see a floating action button in the home screen. You can use it to add a new note.

![img](https://lh3.googleusercontent.com/vx8kr5agLQcrsL-w6hdpYXHMQOn4-O_SoYaUToPoUgfjgYVNwYP_LsWheiPHE9MJl3R64qz6yr3Y-TA2AtKJQBfrfmbpG1XabNzdMkM1FwMYH_VmIn3rrlp1e1-Qz5LdtKWWY2Yr)

**Note**: You can find the full source code [**here**](https://github.com/JoinCODED/Demo-Flutter-NotesApp-Provider-GoRouter)
