# **FloatingActionButton** widget

To display a floating button on the home screen, we can use the **FloatingActionButton** widget as the screenshot below shows.

![img](https://lh3.googleusercontent.com/fKdEk6ZavZPBMiIXW4j6Amf5klQpCkq1BdBieGUTwAeEnnwpN-pWKwDTwEXuyx4TWbY1jqqEoTaJbJxiass3zEqaVLeF8nssW72FEh2Wq4KjDCFrYYxLpXoXm7yfIWM-rxnCnF-i)

1. Go to the **home_page.dart** file
2. Use the **floatingActionButton** named argument inside the **Scaffold** widget.
3. This named argument takes a widget, so we will use the **FloatingActionButton** widget which will help us to display this named argument.

![img](https://lh5.googleusercontent.com/H5ogw5RLbv-JYe_NcblkOAuczOKV3riBGYfgC7xG04AeIJiEG6bmiA6ewr6920KfvsMaHccaQOFcZxCTJho4gPVuzjddruMiDdx-5uWbZtTfNlFAcdmIdEAjnATzfe1MCJYYi58L)

4. This widget takes two named arguments

The first named argument is the **child**, and it takes a widget. This widget will display inside the Floating action button. So, we will pass an icon widget.

![img](https://lh6.googleusercontent.com/_Foqjf7A8bULDRrFuvhLoZgP7USMdUwwnviBso16QiN8F-Ds1vtfSAU_DgJd9Zz51t0yWK_aSx5v6VHcaVTiCJIGNgt8BYU1A4F3naXsG0T-rYf1zwgVpAnbjOWy4c0rnmvi-C8g)

```dart
FloatingActionButton(
          child: Icon(
            Icons.add,
            size: 30,
          ),
        )
```

The second named argument is **onPressed**, this named argument will take a function that is called when the button is tapped. Also, don’t forget to call the **addNote** function inside the noteProvider.

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

The last argument we will use is **backgroundColor**, The FloatingActionButton's background color. We will use the **primaryColor** that we set before inside the **main.dart** file.

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

5. After you run the app, you will see a floating action button on the home screen, and you can use it to add a new note.

   ![img](https://lh3.googleusercontent.com/vx8kr5agLQcrsL-w6hdpYXHMQOn4-O_SoYaUToPoUgfjgYVNwYP_LsWheiPHE9MJl3R64qz6yr3Y-TA2AtKJQBfrfmbpG1XabNzdMkM1FwMYH_VmIn3rrlp1e1-Qz5LdtKWWY2Yr)

**Note: You can find the full source code**[ **here**](https://github.com/JoinCODED/Demo-Flutter-NotesApp-Provider-GoRouter)**.**
