# Slider

### Overview

A Slider is a component that allows the user to slide a bar to pick a value between a range

![](https://totalcross.com/documentation/img/samples/slider-sample.gif)

{% code title="SliderSample.java" %}
```java
import totalcross.sys.Settings;
import totalcross.ui.Container;
import totalcross.ui.Label;
import totalcross.ui.ScrollBar;
import totalcross.ui.Slider;
import totalcross.ui.dialog.MessageBox;
import totalcross.ui.event.ControlEvent;
import totalcross.ui.event.Event;
import totalcross.ui.font.Font;
import totalcross.ui.gfx.Color;
import totalcross.ui.ScrollContainer;


public class SliderSample extends ScrollContainer {
  private Label l;
  private ScrollContainer sc;
  
  @Override
  public void initUI() {
    try {
      super.initUI();
      setScrollBars(false, true);
      
      add(l = new Label("", CENTER), LEFT, TOP);

      Slider sl;
      sl = new Slider(ScrollBar.HORIZONTAL);
      sl.setFont(Font.getFont(false, Font.NORMAL_SIZE));
      sl.appId = 1;
      sl.setLiveScrolling(true);
      sl.setBackColor(Color.getRGB(158, 197, 244));
      sl.sliderColor = Color.getRGB(12, 98, 200);
      sl.setValue(10);
      add(sl,CENTER, TOP + fmH * 2 + 150, (Settings.screenWidth - ((Settings.screenWidth)/10)*2), PREFERRED);
      
      
      
      sl = new Slider(ScrollBar.HORIZONTAL);
      sl.setFont(Font.getFont(false, Font.NORMAL_SIZE / 2 * 3));
      sl.appId = 2;
      sl.setUnitIncrement(5);
      sl.drawTicks = false;
      sl.setBackColor(Color.getRGB(255, 234, 157));
      sl.sliderColor = Color.getRGB(255, 199, 0);
      
      sl.setValue(30);
      add(sl, CENTER, AFTER + fmH + 100, (Settings.screenWidth - ((Settings.screenWidth)/10)*2), PREFERRED);

      sl = new Slider(ScrollBar.HORIZONTAL);
      sl.setFont(Font.getFont(false, Font.NORMAL_SIZE / 2 * 4));
      sl.appId = 3;
      sl.invertDirection = true;
      sl.setBackColor(Color.getRGB(255, 192, 157));
      sl.sliderColor = Color.getRGB(255, 92, 0);
      sl.setValue(50);
      add(sl, CENTER, AFTER + fmH + 50, (Settings.screenWidth - ((Settings.screenWidth)/10)*2), PREFERRED);

      sl = new Slider(ScrollBar.VERTICAL);
      sl.setFont(Font.getFont(false, Font.NORMAL_SIZE));
      sl.appId = 4;
      sl.setLiveScrolling(true);
      sl.setBackColor(Color.getRGB(149, 243, 230));
      sl.sliderColor = Color.getRGB(0, 195, 168);
      sl.setValue(70);
      add(sl, BEFORE + 200 , AFTER + fmH + 200, PREFERRED, Settings.screenHeight/3);

      sl = new Slider(ScrollBar.VERTICAL);
      sl.setFont(Font.getFont(false, Font.NORMAL_SIZE / 2 * 3));
      sl.appId = 5;
      sl.setLiveScrolling(true);
      sl.setBackColor(Color.getRGB(255, 220, 157));
      sl.sliderColor = Color.getRGB(255, 164, 0);
      sl.setValue(90);
      add(sl, CENTER , SAME, PREFERRED, Settings.screenHeight/3);

      sl = new Slider(ScrollBar.VERTICAL);
      sl.setFont(Font.getFont(false, Font.NORMAL_SIZE / 2 * 4));
      sl.appId = 6;
      sl.invertDirection = true;
      sl.setBackColor(Color.getRGB(254, 156, 165));
      sl.sliderColor = Color.getRGB(255, 0, 24);
      sl.setValue(50);
      add(sl,AFTER + 200, SAME, PREFERRED, Settings.screenHeight/3);
    } catch (Exception ee) {
      MessageBox.showException(ee, true);
    }
  }

  @Override
  public void onEvent(Event e) {
    if (e.type == ControlEvent.PRESSED && e.target instanceof Slider) {
      Slider s = (Slider) e.target;
    }
  }
}
```
{% endcode %}

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **boolean** | drawFilledArea | Setting to false does not draw the filled line\* of the Slider |
| **boolean** | drawTicks | Defining as true, ticks will be drawn along the Slider to indicate all the possible points where the Slider may be. By default, the number of ticks to be drawn are the same as the maximum slider value, \(SeeMethods bellow\), but this value can be modified by setting a different value for setUnitIncrement\(int i\) |
| **boolean** | invertDirection | Setting to True causes the filled area of the Slider to be the rightmost part of the scroll circle, which by default is the leftmost |
| **int** | sliderColor | Changing this attribute value colors the circle and the filled line\* of the Slider |

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | Slider\( \) | Cria um Slider **na posição horizontal** com o limite mínimo e máximo de 0 e 100, respectivamente |
| **Constructor** | Slider\(byte orientation\) | Cria um Slider **na posição desejada** com o limite mínimo e máximo de 0 e 100, respectivamente, |
| **void** | setMinimum\(int i\) | Sets the minimum value of the bar limit |
| **void** | setMaximum\(int i\) | Sets the maximum value of the bar limit |
| **void** | setUnitIncrement\(int i\) | Sets the value that will be incremented or decremented to the Slider while using a PenDrag event |
| **void** | setValue\(int i\) | Sets the starting value for the Slider to begin with. If this initial value is greater than the maximum value, then it will be limited to the maximum |

### **References**

See the [JavaDocs](https://rs.totalcross.com/doc/totalcross/ui/Slider.html) for more information

