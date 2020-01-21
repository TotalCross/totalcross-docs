# Dynamic Scroll

### Overview <a id="overview"></a>

Scroll is a specialized type of Scroll Container intended for high performance where hundreds or thousands of views need to be displayed in a scrollable list.​

{% hint style="info" %}
In Totalcross this component is called **`DynamicScrollContainer`**
{% endhint %}

![](../.gitbook/assets/dynamicscrollcontainer-sample.gif)

{% hint style="info" %}
Because it is a more complex example, which does not only involve the creation of the interface, we have a simpler and more direct example. To access the complete example, just go to our [github](https://github.com/TotalCross/TCSample/blob/master/src/main/java/totalcross/sample/components/ui/DynScrollContainerSample.java).
{% endhint %}

### Source Code <a id="source-code"></a>

{% code title="DynScrollContainerSample.java" %}
```java
// Creating and positioning the DynamicScrollContainer
vsc = new DynamicScrollContainer();
vsc.setBackColor(Color.WHITE);
vsc.setBorderStyle(BORDER_SIMPLE);
add(vsc, LEFT + gap, AFTER + gap*2, FILL - gap, FILL - gap*2);
// Adding views to the DynamicScrollContainer
DynSCTestView view = new DynSCTestView(array[i], font);
view.height = Settings.screenHeight / 20;
datasource.addView(view);
```
{% endcode %}

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | DynamicScrollContainer\( \) | Creates a empty DynamicScrollContainer. |
| **Constructor** | DynamicScrollContainer\(DynamicScrollContainer.DataSource datasource\) | Creates a DynamicScrollContainer that sets the referred datasource |
| **DynamicScrollContainer.AbstractView** | getTopMostVisibleView\( \) | Return the top most visible view |
| **Boolean** | isViewVisible\(DynamicScrollContainer.AbstractView view\) | Return true if the view is visible |
| **Boolean** | scrollContent\(int dx, int dy, boolean fromFlick\) | Scroll the DynamicScrollContainer to the referred position. If the boolean is true, it does a flick animation |
| **void** | scrollToView\(DynamicScrollContainer.AbstractView view\) | Scroll the DynamicScrollContainer to the view |
| **void** | setDataSource\(DynamicScrollContainer.DataSource datasource\) | Set the DataSource |
| **void** | stopFlick\(\) | Stops any flick animation |

