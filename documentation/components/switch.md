# Switch

### Overview

Switch is a element that chooses between two proportions

{% code title="SwitchSample.java" %}
```java
 // Instance a simple switch
subtitles = new Switch();

 // Set the colors up
subtitles.colorBallOn = Color.getRGB(0,150,136);
subtitles.colorBarOn = Colors.P_700;
subtitles.colorBallOn = Color.getRGB(241,241,241);
subtitles.colorBarOff = Colors.P_200;

 // Positions the switch 
add(subtitles, RIGHT-hGap, SAME+lsfx.getHeight()/2, PREFERRED, PREFERRED);
```
{% endcode %}

{% hint style="info" %}
This sample code is only from the Switch, to see the complete sample, including the Slider, go to [github](https://github.com/TotalCross/TCSample/blob/master/src/main/java/totalcross/sample/components/ui/SliderSwitchSample.java)
{% endhint %}

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **boolean** | centerText | Boolean that center the text instead of move from left to right |
| **int** | colorBackOff | Background color for off switch |
| **int** | colorBackOn | Background color for on switch |
| **int** | colorForeOff | Foreground color for off switch |
| **int** | colorForeOn | Foreground color for on switch |
| **String** | textBackOff | Background text for off switch |
| **String** | textBackOn | Background text for on switch |
| **String** | textForeOff | Foreground text for off switch |
| **String** | textForeOn | Foreground text for on switch |

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | Switch\( \) | Creates a simple switch |
| **int** | getPreferredHeight\( \) | Returns the switch minimum height |
| **int** | getPreferredWidth\( \) | Returns the switch minimum width |
| **boolean** | isOn\( \) | Return true if the switch is on |
| **void** | moveSwitch\(boolean toLeft\) | If true, move the switch to left |
| **void** | setOn\(boolean b\) | If true, turn on the switch |
| **void** | setPos\(int x, int y\) | Set the Switch´s x and y position |

### **References**

* See the [JavaDocs](https://rs.totalcross.com/doc/totalcross/ui/Switch.html) for more information.

