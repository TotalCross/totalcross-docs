# Spinner

### Overview

Spinner is a control that shows an image indicating that something is running in the background. It has two styles: **iPhone** and **Android**.

![](https://totalcross.com/documentation/img/samples/spinner-sample.gif)

### Source Code

{% code title="SpinnerSample.java" %}
```java
  //Spinner inside the Bar
Bar bar = new Bar (“text text”);
add(bar, LEFT, TOP, FILL, PREFERRED);
bar.createSpinner(Color.WHITE);
bar.startSpinner;

  //Spinner inside the Loop
Spinner spinner = new Spinner(Spinner.IPHONE);
spinner.setForeColor(Color.WHITE);
add(spinner, CENTER, AFTER,, FONTSIZE + 200, FONTSIZE + 200);

while (Vm.getTimeStamp()  < (Vm.getTimeStamp() + 5000))
{
    spinner.update();
}

  //Spinner inside the ProgressBox
Spinner.spinnerType = Spinner.ANDROID;
ProgressBox pb = new ProgressBox("Alert!", “msg”, null);
pb.setBackColor(Color.getRGB(12, 98, 200));
pb.popupNonBlocking();
```
{% endcode %}

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | Spinner\( \) | Creates a simple Spinner |
| **Constructor** | Spinner\(Image anim\) | Creates a spinner from an animated GIF |
| **Constructor** | Spinner\(int type\) | Creates a spinner of the given type |
| **boolean** | isRunning\( \) | Returns if the spin is running |
| **void** | setImage\(Image anim\) | Changes the gif image of this Spinner |
| **void** | setType\(int t\) | Changes the Spinner to one of the predefined types |
| **void** | start\( \) | Starts the spinning thread |
| **void** | stop\( \) | Stops the spinning thread |
| **void** | update\( \) | Updates the spinner; call this when using the spinner inside a loop |

### **References**

* See also our [quick tutorial video](https://www.youtube.com/watch?v=b19EB2gN80E) showing how to use Spinner.
* See the [JavaDocs](https://rs.totalcross.com/doc/totalcross/ui/Spinner.html) for more information**.**



