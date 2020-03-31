# Accordion

### Overview

Accordions are used to show and hide text through user interaction.

{% hint style="info" %}
In Totalcross this component is called **`AccordionContainer`**
{% endhint %}

![](../../.gitbook/assets/accordion-sample.gif.pagespeed.ce.wfbmtgt3hy.gif)

### Source Code

{% code title="AccordionSample.java" %}
```java
import totalcross.sys.Settings;
import totalcross.ui.AccordionContainer;
import totalcross.ui.MainWindow;
import totalcross.ui.MultiEdit;
import totalcross.ui.font.Font;
import totalcross.ui.gfx.Color;

public class AccordionSample extends MainWindow {

	public AccordionSample() {
		setUIStyle(Settings.MATERIAL_UI);
		Settings.uiAdjustmentsBasedOnFontHeight = true;
	}

	public void initUI() {
		int gap = (int) (Settings.screenDensity * 20);

		AccordionContainer.Group gr = new AccordionContainer.Group();
		AccordionContainer ac[] = new AccordionContainer[5];
		MultiEdit me[] = new MultiEdit[5];

		for (int i = 0; i < ac.length; i++) {
			ac[i] = new AccordionContainer(gr);
			ac[i].setFont(font.asBold());
			me[i] = new MultiEdit(50, gap / 4);
			me[i].setText("Type here!");
		}

		add(ac[0], CENTER, AFTER + gap * 2, SCREENSIZE + 85, PREFERRED);
		ac[0].setBackForeColors(0xBFDCF7, Color.BLACK);
		ac[0].add(ac[0].new Caption("...the biggest state?"), LEFT, TOP, FILL, PREFERRED);
		ac[0].add(me[0], LEFT + gap * 4, AFTER + gap, FILL, FONTSIZE + 600);
		me[0].transparentBackground = true;
		me[0].setFont(Font.getFont(false, this.getFont().size));

		for (int i = 1; i < ac.length; i++) {
			add(ac[i], CENTER, AFTER + gap / 2, SCREENSIZE + 85, PREFERRED);
			ac[i].setBackForeColors(0xBFDCF7, Color.BLACK);

			switch (i) {
			case 1:
				ac[i].add(ac[i].new Caption("...the most famous forest?"), LEFT, TOP, FILL, PREFERRED);
				break;
			case 2:
				ac[i].add(ac[i].new Caption("...the current president?"), LEFT, TOP, FILL, PREFERRED);
				break;
			case 3:
				ac[i].add(ac[i].new Caption("...the most famous river?"), LEFT, TOP, FILL, PREFERRED);
				break;
			case 4:
				ac[i].add(ac[i].new Caption("...the most famous statue?"), LEFT, TOP, FILL, PREFERRED);
				break;
			}
			ac[i].add(me[i], LEFT + gap * 4, AFTER + gap, FILL, FONTSIZE + 600);
			me[i].setFont(Font.getFont(false, ac[i].getFont().size));
			me[i].transparentBackground = true;
		}
	}

	public int getScreenWidth() {
		return Settings.screenWidth;
	}
}
```
{% endcode %}

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **int** | **minH** | Minimum height of the closed accordion |

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | AccordionContainer\( \) | Creates a empty accordion |
| **Constructor** | AccordionContainer\(AccordionContainer.Group g\) | Creates a list of accordions from the accordion group. |
| **void** | collapse\( \) | Closes the accordion |
| **void** | collapse\(boolean showAnimation\) | Closes the accordion with animation\(depending on the parameter\) |
| **void** | expand\( \) | Open the accordion |
| **void** | expand\(boolean showAnimation\) | Open the accordion with animation\(depending on the parameter\) |
| **int** | getPreferredHeight\( \) | Returns the accordion´s minimum height |
| **boolean** | isExpanded\( \) | Retorna true if the accordion is open |
| **void** | onAnimationFinished\(ControlAnimation anim\) | This method is called after the animation is finished |
| **void** | setPos\(int x, int y\) | Set the accordion´s x and y position |

### References

* See also our [quick video tutorial](https://www.youtube.com/watch?v=7fl1GfuKSOw) on how to add other components within an accordion.
* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/Button.html) for more information.

