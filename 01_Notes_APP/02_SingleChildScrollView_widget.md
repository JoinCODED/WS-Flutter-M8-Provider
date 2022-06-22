In the `HomePage` widget, you will add two sections:
The first section will be at the top of the page and will contain two `TextField` widgets, the title of the note, and the body of the note. Both `TextField` widgets will be used to take inputs from the user.
The second section is **ListView**, which will be placed at the bottom of the page, and will display the notes:

![img](https://lh4.googleusercontent.com/eyARO3vkpJNBOpdcv1paNuO0L6XhGOiG6lopxz1aSAXwnbuWoFq1X32fRcGzEpoeidrXLxoJe1Kgz55YR6v5dtudyYMDops-aiyvnKx25dDNT0EMc59rzXNyXDVJChqfZ7vgEl9s)

2. Add the code below in the `home_page.dart` file to add the first section:

```dart
// #a
SingleChildScrollView(
          child: Column(
            children: [

              Container(
                padding: EdgeInsets.all(20),
		// #b
                child: Card(
                  elevation: 10,

				  // #c
                  child: ListTile(
                    title: Column(
                      children: [

						// #d
                        TextField(
                          controller: _titleTextEditingController,
                          decoration: InputDecoration(
                            hintText: 'Title',
                            border: InputBorder.none,
                          ),
                        ),

						// #e
                        TextField(
                          controller: _bodyTextEditingController,
                          decoration: InputDecoration(
                            hintText: 'Body',
                            border: InputBorder.none,
                          ),
                        ),
                      ],
                    ),

					// #f
                    trailing: IconButton(
                      iconSize: 32,
                      icon: Icon(
                        Icons.add_box,
                        color: Theme.of(context).primaryColor,
                      ),
                      onPressed: () {},
                    ),
                  ),
                ),
              ),

              // TODO: #4 Add ListView builder
            ],
          ),
        )
```

> > We used:
> > a. The **Column** widget and wrapped it with the **SingleChildScrollView**, which converts the **Column** widget to a scrolled widget.
> > b. A **Card** widget to style the top section of the page (the title and the body textfields).
> > c. The **ListTile** to help us organize and align the two **TextField** widgets and the **Add button**.
> > d. The **TextField** widget for the Title of the note.
> > e. The **TextField** widget for the Body of the note.
> > f. The **IconButton** widget to help the user add a new note.
