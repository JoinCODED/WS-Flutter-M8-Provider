# **SingleChildScrollView** widget





4. Inside our app, we will have two areas in the HomePage widget, the first area that on the top will have two **TextField** widgets (**Title** of the note & **Body** of the note), and we will use these **TextField** widgets to take input from the user. The second area on the bottom will have a **ListView** widget to display the notes.

<img src="https://lh4.googleusercontent.com/eyARO3vkpJNBOpdcv1paNuO0L6XhGOiG6lopxz1aSAXwnbuWoFq1X32fRcGzEpoeidrXLxoJe1Kgz55YR6v5dtudyYMDops-aiyvnKx25dDNT0EMc59rzXNyXDVJChqfZ7vgEl9s" alt="img" style="zoom:67%;" />



First, we will add the first area that on the top, replace 

```dart
// TODO: #1 Textfields
        body: Container(),
```

with

```dart
// #1
SingleChildScrollView(
          child: Column(
            children: [
				
              Container(
                padding: EdgeInsets.all(20),
		// #2
                child: Card(
                  elevation: 10,
				  
				  // #3
                  child: ListTile(
                    title: Column(
                      children: [
					  
						// #4
                        TextField(
                          controller: _titleTextEditingController,
                          decoration: InputDecoration(
                            hintText: 'Title',
                            border: InputBorder.none,
                          ),
                        ),
						
						// #5
                        TextField(
                          controller: _bodyTextEditingController,
                          decoration: InputDecoration(
                            hintText: 'Body',
                            border: InputBorder.none,
                          ),
                        ),
                      ],
                    ),
					
					// #6
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

1. First, we used the **Column** widget. we wrapped it with the **SingleChildScrollView**, and this widget will convert the **Column** widget to be a scrolled widget. So, when you want to add a **ListView** widget inside the **Column** widget, wrap the **Column** widget with the **SingleChildScrollView.**
2. Here, we used a **Card** widget to style the top area that we have.
3. We used the **ListTile** to help us to organize and align the two **TextField** widgets and **Add button**.
4. **TextField** for the Title of note.
5. **TextField** for the Body of note.
6. Here, we used the **IconButton** widget; we will use it later to help the user to add a new note.









































































