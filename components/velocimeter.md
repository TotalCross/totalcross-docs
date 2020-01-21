# Velocimeter

### Overview

The Velocimeter represents a velocimeter gauge. The background and pointer can be customized. The text, max and min values can be drawn or not. The pointer's color can be changed

![](https://totalcross.com/documentation/img/samples/velocimeter-sample.gif)

{% code title="VelocimeterSample.java" %}
```java
  // Adds a timer
tt = addTimer(50);

  // Creates a simple Velocimeter
vel = new Velocimeter();
vel.value = -20;
vel.max = 40;
vel.pointerColor = Color.GREEN;
add(vel, CENTER, CENTER, PARENTSIZE + 50, PARENTSIZE + 50);

// Generates an event from the timer
@Override
public void onEvent(Event e)
{
	if (e.type == TimerEvent.TRIGGERED && tt.triggered)
	{
		vel.value++;
		if (vel.value > vel.max + 20)
		{
			vel.value = vel.min - 20;
		}
		repaint();
	}
}
```
{% endcode %}

{% hint style="info" %}
To view the full code, [click here](https://github.com/TotalCross/TCSample/blob/master/src/main/java/totalcross/sample/components/ui/VelocimeterSample.java).
{% endhint %}

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **boolean** | drawMax | Set to false to don't draw the max value's text |
| **boolean** | drawMin | Set to false to don't draw the min value's text |
| **boolean** | drawValue | Set to false to don't draw the value's text. |
| **int** | max | The maximum value; defaults to 100. |
| **int** | maxAngle | The maximum angle value; defaults to 270 degrees for the default gauge |
| **int** | min | The minimum value; defaults to 0 |
| **int** | pointerColor | The pointer's color |
| **int** | value | The current value |
| **int** | valueColor | The value's color. |

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | Velocimeter\( \) | Constructs a velocimeter using the default gauge and pointer images |
| **Constructor** | Velocimeter\(String gaugeImagePath, String pointerImagePath\) | Constructs a velocimeter using the given images |

### **References**

See the [JavaDocs](https://rs.totalcross.com/doc/totalcross/ui/chart/Velocimeter.html) for more information.

