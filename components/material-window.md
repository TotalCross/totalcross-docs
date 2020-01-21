# Material Window

### Overview

Material window is a window with a top bar and a return button that supports slide animations with their entire layout made based on the [Google Material Design](https://blog.totalcross.com/en/material-o-layout-da-google/) specifications.

![](../.gitbook/assets/materialwindow-sample.gif)

{% hint style="info" %}
Because this is a more complex example, they choose to only sample part of the main interface and a call from the Material Window. To see the complete example [click here](https://github.com/TotalCross/TCSample/blob/master/src/main/java/totalcross/sample/components/ui/MaterialWindowSample.java)
{% endhint %}

### Source Code

```java
Button btn1 = new Button("Sign Up");
btn1.setBackForeColors(Colors.P_500, Colors.ON_P_500);
vbox.addControl(btn1);
btn1.addPressListener((e) -> {
    MaterialWindow mw = new MaterialWindow("Sign Up",new Presenter() {
        @Override
        public Container getView() {

            return new Container() {
                @Override
                public void initUI() {
                    //put all the window content here
                }
            };
        }
    });
    mw.popup();
});
Button btn2 = new Button("Sign in");
btn2.setBackForeColors(Colors.P_500, Colors.ON_P_500);
vbox.addControl(btn2);
btn2.addPressListener((e) -> {
    MaterialWindow mw = new MaterialWindow("Sign in",new Presenter() {
        @Override
        public Container getView() {
            return new Container() {
                @Override
                public void initUI() {
                    //put all the window content here 
                    
                }
            };
        }
    });
    mw.popup();
});
```

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | MaterialWindow\(Presenter&lt;Container&gt; provider\) | Creates an MaterialWindow that receives a provider that provides the components to be inserted in the window. |
| **Constructor** | MaterialWindow\(boolean delayInitUI, Presenter&lt;Container&gt; provider\) | Creates an MaterialWindow, that may have a initUI delay, which receives a provider that provides the components to be inserted in the window |
| **Construtor** | MaterialWindow\(String title, boolean delayInitUI, Presenter&lt;Container&gt; provider\) | Creates an MaterialWindow, that may have a initUI delay, with the given title that receives a provider that provides the components to be inserted in the window |
| **void** | setBarFont\(Font f\) | Sets the bar font. |
| **void** | setTitle\(String title\) | Sets the title. |
| **String** | getTitle\(\) | Returns the Title. |
| **void** | unpop\( \) | Unpop the MaterialWindow. |
| **void** | popup\( \) | Popup the MaterialWindow. |

### **References**

* See also our [quick video](https://www.youtube.com/watch?v=NN4qTuvO-tE) tutorial of how a material window
* See the [Label Java Docs ](https://rs.totalcross.com/doc/totalcross/ui/Label.html)for more information.

