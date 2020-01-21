# ComboBox

### Overview

It is a compressed checkbox that, when clicked, expands, allowing the user to choose an item from several possible options

![](../.gitbook/assets/combobox-sample.gif)

{% hint style="info" %}
This sample code is only from the ComboBox, to see the complete sample, including the ListBox, go to [github](https://github.com/TotalCross/TCSample/blob/master/src/main/java/totalcross/sample/components/ui/ComboListSample.java).
{% endhint %}

### Source Code

{% code title="ComboBoxSample.java" %}
```java
import totalcross.sys.Settings;
import totalcross.ui.ComboBox;
import totalcross.ui.Label;
import totalcross.ui.ScrollContainer;
import totalcross.ui.dialog.MessageBox;

public class ComboBoxSample extends ScrollContainer {

	private ComboBox simpleComboBox;
	private ComboBox popupComboBox;

	private int gap = (int) (Settings.screenDensity * 20);

	@Override
	public void initUI() {
		try {
			setScrollBars(false, true);
			setBackForeColors(0xF7F7F7, 0x000000);

			String[] items = { "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten" };

			Label lbCombos = new Label("Combos", CENTER);
			lbCombos.setFont(lbCombos.getFont().asBold());
			add(lbCombos, LEFT + gap, AFTER + gap * 2, FILL - gap, PREFERRED);

			ComboBox.usePopupMenu = false;
			simpleComboBox = new ComboBox(items);
			simpleComboBox.caption = "Numbers with Dropdown";
			simpleComboBox.setForeColor(0x000000);

			add(simpleComboBox, LEFT + gap, AFTER + gap / 2, FILL - gap, PREFERRED);

			ComboBox.usePopupMenu = true;
			popupComboBox = new ComboBox(items);
			popupComboBox.caption = "Numbers with Popup";
			popupComboBox.setForeColor(0x000000);

			add(popupComboBox, LEFT + gap, AFTER + gap / 2, FILL - gap, PREFERRED);

		} catch (Exception e) {
			MessageBox.showException(e, true);
		}
	}
}
```
{% endcode %}

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **int** | checkColor | Changing the value of this variable will change the color of the RadioButton, that only appears in the Android environment, or the color of the arrow in other evironments where MaterialUI is enabled |
| **Boolean** | enableSearch | When the number of items in a ComboBox is greater than 10, an area above the popup list is intended for item searching. By default, the value of this attribute is true, set it to false if you do not want this item search area |
| **String** | popupTitle | Changes the popup list title |
| **Boolean** | usePopMenu | Assign true to this variable before instanciate a new Combobox to show items in a popup window menu. |

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | ComboBox\( \) | Creates an empty ComboBox |
| **Constructor** | ComboBox\(Object\[ \] items\) | Creates a ComboBox with the given items |
| **Constructor** | ComboBox\(ListBox userListBox\) | Creates a ComboBox with a popup list containing the given ListBox. You can create a class that extends a ListBox to draw the items by yourself and then pass it as parameter to this constructor, so the popup list will use your class instead |
| **Constructor** | ComboBox\(ComboBoxDropDown userPopList\) | Creates a ComboBox with the given PopList |
| **void** | add\(Object item\) | Adds an object to the Listbox |
| **void** | add\(Object\[ \] items\) | Adds an array of Objects to the Listbox |
| **void** | clear\( \) | Resets the selected index to the value of the defaultClearValueInt attribute; the default value is 0 |
| **Object** | getItemAt\(int i\) | Get the object at the given index |
| **Object\[ \]** | getItems\( \) | Returns all items in this ComboBox |
| **ListBox** | getListBox\( \) | Returns the ListBox used to show the items of the ComboBox |
| **Object** | getSelectedItem\( \) | Returns the selected item of the ListBox |
| **void** | remove\(int itemIndex\) | Removes an object from the Listbox at the given index |
| **void** | remove\(Object item\) | Removes an object from the Listbox |
| **void** | removeAll\( \) | Empties the items of the ComboBox |
| **void** | setItemAt\(int i, Object s\) | Sets the object at the given index |
| **void** | setSelectedIndex\(int i\) | Select the given index |
| **void** | setSelectedIndex\(int i, boolean sendPressEvent\) | Select the given index, and optionally sends a PRESSED event |
| **void** | setSelectedItem\(Object name, boolean sendPress\) | Select an item, and optionally sends a PRESSED event |

### References

* See also our [quick tutorial video](https://www.youtube.com/watch?v=UN67cUHuD7M) on creating Combo and List Box.
* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/Button.html) for more information.

