# Label

### Overview

This control is used to display static text or a marquee. The label in TotalCross can also display multiple lines of text, separated by the character. A label never receives focus neither dispatches events

### Source Code

```java
import totalcross.sys.Settings;
import totalcross.ui.Label;
import totalcross.ui.MainWindow;

public class LabelSample extends MainWindow {

	public LabelSample() {
		setUIStyle(Settings.MATERIAL_UI);
		Settings.uiAdjustmentsBasedOnFontHeight = true;
	}

	public void initUI() {
		Label lb1, lb2, lb3, lb4;

		lb1 = new Label("This is a Simple Label", CENTER);
		lb1.setBackForeColors(0x2979ff, 0xEEEEEE);
		add(lb1, CENTER, CENTER, PARENTSIZE + 70, PREFERRED + 20);

		lb2 = new Label("This is a 3D Label", CENTER);
		lb2.setBackForeColors(0x2979ff, 0xEEEEEE);
		lb2.set3d(true);
		add(lb2, CENTER, AFTER + 20, SAME, SAME);

		lb3 = new Label("This is a Inverted Label", CENTER);
		lb3.setBackForeColors(0x2979ff, 0xEEEEEE);
		lb3.setInvert(true);
		add(lb3, CENTER, AFTER + 20, SAME, SAME);

		lb4 = new Label("This is a Label with a large text and line break", CENTER);
		lb4.autoSplit = true;
		lb4.setBackForeColors(0x2979ff, 0xEEEEEE);
		add(lb4, CENTER, AFTER + 20, SAME, SAME);
	}
}
```

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **int** | Align | Sets the text align as LEFT, RIGHT, CENTER and FILL\(justified\) |
| **boolean** | autoSplit | Set to true to let the label split its text based on the width every time its width changes |

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | Label\( \) | Creates an empty label, using FILL as the preferred width |
| **Constructor** | Label\(String text\) | Creates a label displaying the given text \(that may be changed at runtime\) using left alignment. Supports inverted text, multiple lines and is scrollable by default |
| **Constructor** | Label\(String text, int align\) | Like the above, but you can also set the horizontal alignment using one of the constants LEFT, CENTER, RIGHT, or FILL \(justified\) |
| **void** | setInvert\( \) | Inverts the back and fore colors |
| **void** | setHighlighted\( \) | Highlights the text by painting the text in all directions with a brighter color, then centered, with the foreground color. |
| **void** | setHighlightedColor\( \) | Sets the color used when highlighting is on |
| **void** | set3d\(boolean on\) | Draws the label with a 3d effect |

### **References**

* See the [Label Java Docs ](https://rs.totalcross.com/doc/totalcross/ui/Label.html)for more information.

