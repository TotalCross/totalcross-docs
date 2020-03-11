---
description: See the basics of how to work with TotalCross SDK
---

# 4. Write your first app

## Introduction

How about writing your first TotalCross code? In the next sections, you will need to

* Download images for the implementation [**link**](https://github.com/TotalCross/my-first-app-medium/tree/master/src/main/resources/images)_._
* Inspect full code here: [**link**](https://github.com/TotalCross/my-first-app-medium).

## Guide

### **Step 1**

Create a new project called _MyFirstApp_ and go to `MyFirstApp > src > main > java > com > totalcross` , the file `MyFirstApp.java` it will be where you will build the code. Remove these lines of the project, before init next Steps:

```java
Label helloWord = new Label('Hello World!');
add(helloWord, CENTER, CENTER);
```

### **Step 2**

In folder ****`myfirstapp > src > main` create the `resources` folder and `images` folder inside now paste the images for this folder.

### **Step 3**

Scroll Container is a component used to add components at points that do not fit naturally on the screen, which need to go down or go to the sides.

First, you have to import the library to create the object, line 5 from the code below, these steps were repeated for all objects that will be used, then name and define your initial variables in the constructor method, inline 21 in the code below were set to false and true, thus disabling the horizontal scroll. If you want the scroll to be possible for both situations you must keep the method empty.

Next, you have to add the screen using the add method, which has to be configured with the object to be inserted on the screen and the position variables respectively, **object, horizontal position, vertical position, width, height**, as shown on line 22.

```java
package com.totalcross;
// Import libraries
import totalcross.ui.MainWindow;
import totalcross.ui.ScrollContainer;
import totalcross.sys.Settings;

public class MyFirstApp extends MainWindow {
    // Declaring variable
    private ScrollContainer sc;
    
    public myfirstapp() {   
        setUIStyle(Settings.MATERIAL_UI);
    }
    
    @Override
    public void initUI() {
        try {
            // Defining characteristics
            ScrollContainer scrollContainer = new ScrollContainer(false,true);
            // Adding to the application screen
            add(scrollContainer, LEFT, TOP, FILL, FILL); 
        }
        catch (Throwable error) {
            error.printStackTrace();
        }
    }
}
```

With the created container you can add the objects in it using the add method as follows:

```java
scrollContainer.add(object, horizontalPosition, verticalPosition, width, height);
```

### **Step 4**

Two images will be added, one to be the background of the app and the other one logo. How the previous object must add the library before it can be used.

```java
import totalcross.ui.image.Image;
```

Then he had created the objects to receive the images.

```java
private Image imgBack, imgLogo;
```

You should now import the image using the builder.

```java
imgBack = new Image('images/imagem-template-01.png');
imgLogo = new Image('images/logo-branca.png');
```

To be able to change the image parameters, it is necessary to use another `ImageControl` object adding its library.

```java
import totalcross.ui.ImageControl;
```

Instantiating objects.

```java
private ImageControl background, logo;
```

Defining characteristics.

```java
background = new ImageControl(imgBack);
// Maintains the proportion
background.scaleToFit = true;
// Allows you to resize
background.strechImage = true; 

logo = new ImageControl(imgLogo);
logo.scaleToFit = true;
logo.strechImage = true;
// Make transparent background
logo.transparentBackground = true;
// Scale image
logo.tempHwScale = 0.6; 
```

Add in the container.

```java
scrollContainer.add(background, LEFT, TOP);
scrollContainer.add(logo, CENTER , TOP-15);
```

### **Step 5** 

Label is the object you can use to add text to the application.

Two labels will be used, one to title the application and the other to title a questionnaire.

```java
// Import library
import totalcross.ui.Label;

...

// Declaring variable
private Label Title, Gender;
```

As the background is a predominantly red image, it is necessary to change the color of some objects, for this, you can use the `Color` library.

```java
// Import library
import totalcross.ui.gfx.Color;

...

// Defining characteristics
Title = new Label('Registration Form');
Title.transparentBackground = true; 
// Make background transparent
Title.setForeColor(Color.WHITE); 

// Changes the color of the object
Gender = new Label('Gender');
Gender.transparentBackground = true;
Gender.setForeColor(Color.WHITE);

// Including in the container
scrollContainer.add(Title, CENTER, TOP);
scrollContainer.add(Gender, CENTER, AFTER+15);
```

### **Step 6**

This an input component used to receive text and date, it has a method that allows you to receive dates by default, `setMode` must have as input `Edit.DATE, true` for that to be possible.

```java
// Import library
import totalcross.ui.Edit;

...

// Declaring variable
private Edit FullName, Date;

// Defining characteristics
FullName = new Edit();
FullName.caption = 'Full Name';
// Changes what is written in the capture state
FullName.captionColor = Color.WHITE; 
// Changes the object’s color in the capture state
FullName.transparentBackground = true;
FullName.setForeColor(Color.WHITE);

Date = new Edit();
Date.caption = 'Birth Day';
Date.captionColor = Color.WHITE;
Date.setMode(Edit.DATE, true); 
// Change capture mode to date
Date.transparentBackground = true;
Date.setForeColor(Color.WHITE);

// Including in the container
scrollContainer.add(FullName, CENTER, AFTER+125 );
scrollContainer.add(Gender, CENTER, AFTER+20 );
```

### **Step 7**

Check is an input with a checkbox that indicates when it was clicked. In this case, it will be used so that the user can define his gender in the form. For that, it will be necessary to use 3 objects.

```java
// Import library
import totalcross.ui.Check;
// Declaring variable
private Check subject1, subject2, subject3;
```

When clicked, the check generates a wave that propagates from the clicked point to fill the entire object, in this case, this damages the aesthetics, to remove the `effect` _****_method must be null.

```java
// Defining characteristics
subject1 = new Check('Male');
subject1.transparentBackground = true;
subject1.setForeColor(Color.WHITE);
subject1.effect = null; 

// Turn off click effect
subject2 = new Check('Female');
subject2.transparentBackground = true;
subject2.setForeColor(Color.WHITE);
subject2.effect = null;

subject3 = new Check('Other');
subject3.transparentBackground = true;
subject3.setForeColor(Color.WHITE);
subject3.effect = null;
```

When you add `PREFERRED` __in the `add` method, the object’s borders will be the size that accommodates only the checkbox and the text.

```java
// Including in the container
scrollContainer.add(subject1, LEFT+15, AFTER-5 , PREFERRED, PREFERRED+25);
scrollContainer.add(subject2, LEFT+15, AFTER-5 , PREFERRED, PREFERRED+25);
scrollContainer.add(subject3, LEFT+15, AFTER-5 , PREFERRED, PREFERRED+25);
```

### **Step 8**

The buttons will be used to complete the registration or to clear the added information.

```java
import totalcross.ui.Check;

...

private Button Finish,Clear;
```

The colors of the buttons will be changed to contrast with the red background.

```java
Finish = new Button('Submit');
Finish.setForeColor(Color.WHITE);
Finish.borderColor = Color.WHITE; 
// Changes the border color
Finish.transparentBackground = true;

Clear = new Button('Clear');
Clear.setForeColor(Color.WHITE);
Clear.borderColor = Color.WHITE;
Clear.transparentBackground = true;

scrollContainer.add(Finish, CENTER-60, AFTER+25, 100, 50);
scrollContainer.add(Clear, CENTER+60, SAME, 100, 50);
```

## **See more**

Troubles? Inspect full code here: [**link**](https://github.com/TotalCross/my-first-app-medium). Now with the finished project, we have a front end of forms with some of the most used objects, with that it is possible to see the functionality and the use of these, from that point on the functionality of the app is in charge of the developer! 

