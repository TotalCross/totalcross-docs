# Spin List

### Overview

Spin list is a control that has two arrows \(up and down\) to navigate between the information contained in the control, it is possible to navigate by clicking or holding the arrows or navigating the keyboard arrows.

### Source Code

{% code title="SpinList Sample" %}
```java
import totalcross.sys.InvalidNumberException;
import totalcross.sys.Settings;
import totalcross.ui.Container;
import totalcross.ui.MainWindow;
import totalcross.ui.SpinList;
import totalcross.ui.gfx.Color;
import totalcross.util.UnitsConverter;

public class SpinListSample extends MainWindow {

    int gap = UnitsConverter.toPixels(DP + 8);

    public SpinListSample(){
        setUIStyle(Settings.MATERIAL_UI);
    }

    @Override
    public void initUI() {
        try {
            SpinList sl = new SpinList(new String[]{"Blue", "Orange","Yelow", "Red"});
            sl.allowsNoneSelected = true;
            add(sl, LEFT + gap, TOP + gap, FILL, PREFERRED);

            Container paintContainer = new Container();
            add(paintContainer, SAME, AFTER + gap, FILL - gap, FILL - gap);


            sl.addPressListener(e -> {
                switch (sl.getSelectedIndex()){
                    case -1:
                        paintContainer.setBackColor(Color.WHITE);
                        break;
                    case 0:
                        paintContainer.setBackColor(Color.BLUE);
                        break;
                    case 1:
                        paintContainer.setBackColor(Color.ORANGE);
                        break;
                    case 2:
                        paintContainer.setBackColor(Color.YELLOW);
                        break;
                    case 3:
                        paintContainer.setBackColor(Color.RED);
                        break;
                }
            });

        } catch (InvalidNumberException e) {
            e.printStackTrace();
        }
    }
}
```
{% endcode %}

### 

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **boolean** | isVertical | Set to true if there are only numbers in the SpinList and you want to open a NumericBox |
| **boolean** | useNumericBox | Set to true if there are only numbers in the SpinList and you want to open a NumericBox |
| **boolean** | useCalculatorBox | Set to false to disallow the wrap around that happens when the user is at the first or last items. |
| **boolean** | wrapAround | By default, equals the choices' length. You can define its length and then create a single array shared  by a set of SpinLists with different lengths on each SpinList |
| **boolean** | allowsNoneSelected | Allows -1 as selected index |

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | SpinList\(String\[\] choices\) | Constructs a vertical SpinList with the given choices, selecting index 0 by default. |
| **Constructor** | SpinList\(String\[\] choices, boolean isVertical\) | Constructs a SpinList with the given choices, selecting index 0 by default and can be vertical or not. |
| **int** | getPreferredWidth\(\) | Return the width. |
| **int** | getPreferredHeight\(\) | Return the Height. |
| **void** | setChoices\(String\[\] choices\)  | Sets the choices to the given ones |
| **void** | replaceChoices\(String\[\] choices\) | Just replaces the choices array. |
| **int** | getSelectedIndex\(\) | Returns the selected index. |
| **String** | getSelectedItem\(\) | Returns the selected item. |

## References

* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/SpinList.html) for more information.

