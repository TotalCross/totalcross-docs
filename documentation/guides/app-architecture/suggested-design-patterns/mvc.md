# MVC Architecture Pattern

This architecture pattern will assign and separate the objects into responsibilities: **Model**, **View** and **Controller**

* **Model:** will represent an object, such as a person.
* **View:** The view will represent the model data.
* **Controller:** It controls the data of the model object and controls the visualization.

### Structures

{% code title="Structures" %}
```text
└── src
    └── main
        └── java
            └── com.your_company_name.your_name_app
                └── model
                    └── Person
                └── view
                    └── HomeView
                └── controller
                    └── HomePresenter
```
{% endcode %}

{% tabs %}
{% tab title="Person - Model" %}
```java
package com.totalcross.mvc.model;

public class Person {
    private String name;
    private String gender;

    public Person(String name, String gender) {
        this.name = name;
        this.gender = gender;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    @Override
    public String toString() {
        return "n: " + name + " g: " + gender;
    }
}

```
{% endtab %}

{% tab title="HomeScreeen - View" %}
```java
package com.totalcross.mvc.view;

import com.totalcross.mvc.controller.HomePresenter;
import com.totalcross.mvc.model.Person;
import totalcross.ui.Button;
import totalcross.ui.Edit;
import totalcross.ui.Label;
import totalcross.ui.MainWindow;

public class HomeScreen extends MainWindow {

   //Create a variable to store the interface of the class.
    Presenter presenter;

    Person person [] = new Person[5];
    private int gap = 15;

/*
The constructor will be responsible for instantiating the HomePresenter class 
which will link the presenter of the interface with the controller
*/
    public HomeScreen(){
        new HomePresenter(this);
    }

    @Override
    public void initUI() {

        Label lbl = new Label("Person");
        add(lbl, CENTER, TOP + gap);

        Edit editName = new Edit();
        editName.caption = "Insert your name here";
        add(editName, LEFT, AFTER + gap);

        Edit editGender = new Edit();
        editGender.caption = "Insert your gender here";
        add(editGender, LEFT, AFTER + gap);

        Button btn = new Button("Create Person");
        //Assigning the onCreate method to the btn button
        btn.addPressListener( e -> presenter.onCreate(person, editName, editGender));
        add(btn, RIGHT, AFTER + gap);
    }

    //Creating the interface and the methods that will be used on this screen
    public interface Presenter{
        void onCreate(Person[] person, Edit name, Edit gender);
    }

    //Method that allows you to add the Controller Presenter in the view
    public void addListener(Presenter presenter) {
        this.presenter = presenter;
    }


}


```
{% endtab %}

{% tab title="HomePresenter  - Controller" %}
```java
package com.totalcross.mvc.controller;

import com.totalcross.mvc.model.Person;
import com.totalcross.mvc.view.HomeScreen;
import totalcross.ui.Edit;
import totalcross.ui.Toast;

public class HomePresenter implements HomeScreen.Presenter {
/*
    In the constructor the Presenter link of the controller is realized 
    with the view.
*/
    public HomePresenter(HomeScreen home){
        home.addListener(this);
    }
    
    //The method that will be used on the button is implemented.
    @Override
    public void onCreate(Person[] person, Edit name, Edit gender) {
        for (int i = 0; i < person.length; i++) {
            if (person[i] == null){
                person[i] = new Person(name.getText(), gender.getText());
                break;
            }
        }

        String persons = "";
        for (Person p: person) {
            persons += p + " / ";
        }
        Toast.show(persons,2000);
        System.out.println(persons);
    }
}

```
{% endtab %}
{% endtabs %}





## Referencies

* See more about MVC in [Geeks for Geeks](https://www.geeksforgeeks.org/mvc-design-pattern/). 

