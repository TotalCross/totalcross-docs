# Edit

### Overview

An Edit is a field used to show and alter texts. Also known as UITextFIeld on Swift and input on HTML. There also is some variations, like Outlined Edit, Calculator Edit, Password Edit, etc, that are shown on the example bellow.

### Source Code

{% code title="EditSample.java" %}
```java
public class EditSample extends Container {

	private ScrollContainer sc;
	private Edit simpleEdit;
	private Edit numericEdit;
	private Edit calculatorEdit;
	private Edit calendarEdit;
	private Edit timerEdit;
	private Edit passwordShowEdit;
	private Edit passwordHidenEdit;
	private Edit maskedEdit;
	private MultiEdit multiEdit;
	private OutlinedEdit outlinedEdit;

	private final int H = UnitsConverter.toPixels(DP + 4);
	private int GAP = UnitsConverter.toPixels(DP + 15);
	private int focusColor = Color.GREEN;

	@Override
	public void initUI() {
		try {
			Edit.useNativeNumericPad = false;
			Settings.is24Hour = true;
			UIColors.calculatorFore = Colors.BACKGROUND;
			UIColors.numericboxBack = Colors.BACKGROUND;
			UIColors.calendarBack = Colors.BACKGROUND;
			UIColors.timeboxVisorBack = Colors.BACKGROUND;
			sc = new ScrollContainer(false, true);
			add(sc, LEFT, TOP, FILL, FILL);

			simpleEdit = new Edit();
			simpleEdit.caption = "Simple Edit";
			simpleEdit.setBackColor(Color.BRIGHT);
			simpleEdit.transparentBackground = true;
			
			outlinedEdit = new OutlinedEdit();
			outlinedEdit.caption = "OutlinedEdit";
			outlinedEdit.captionColor = Color.getRGB(176, 46, 247);

			multiEdit = new MultiEdit();
			multiEdit.caption = "MultiEdit";
			
			numericEdit = new Edit();
			numericEdit.caption = "NumericBox Edit";
			numericEdit.setMode(Edit.CURRENCY);
			numericEdit.setKeyboard(Edit.KBD_NUMERIC);

			calculatorEdit = new Edit();
			calculatorEdit.caption = "Calculator Edit";
			calculatorEdit.setMode(Edit.CURRENCY, true);

			calendarEdit = new Edit("99/99/99");
			calendarEdit.caption = "Calendar Edit";
			calendarEdit.setMode(Edit.DATE, true);

			timerEdit = new Edit("99" + Settings.timeSeparator + "99" + Settings.timeSeparator + "99");
			timerEdit.caption = "TimeBox Edit (24-hour format)";
			TimeBox.hideIfInvalid = false;
			timerEdit.setValidChars("0123456789AMP");
			timerEdit.setMode(Edit.NORMAL, true);
			timerEdit.setKeyboard(Edit.KBD_TIME);

			passwordShowEdit = new Edit("");
			passwordShowEdit.caption = "Password Edit (last character is shown)";
			passwordShowEdit.setMode(Edit.PASSWORD);
			passwordHidenEdit = new Edit("");
			passwordHidenEdit.caption = "Password Edit (all characters are hidden)";
			passwordHidenEdit.setMode(Edit.PASSWORD_ALL);

			maskedEdit = new Edit("999.999.999-99");
			maskedEdit.caption = "Masked Edit (999.999.999-99)";
			maskedEdit.setMode(Edit.NORMAL, true);
			maskedEdit.setValidChars(Edit.numbersSet);

			noPredictionEdit = new Edit();
			noPredictionEdit.caption = "No Prediction Edit";
			noPredictionEdit.setPrediction(false);
			
			noPredictionMultiEdit = new MultiEdit();
			noPredictionMultiEdit.caption = "No Prediction MultiEdit";
			noPredictionMultiEdit.setPrediction(false);
			
			sc.add(simpleEdit, LEFT + GAP, AFTER + GAP);
			sc.add(outlinedEdit, LEFT + GAP, AFTER + GAP);
			sc.add(multiEdit, LEFT + GAP, AFTER + GAP, FILL - GAP, DP + 48);
			sc.add(numericEdit, LEFT + GAP, AFTER + GAP);
			sc.add(calculatorEdit, LEFT + GAP, AFTER + GAP);
			sc.add(calendarEdit, LEFT + GAP, AFTER + GAP);
			sc.add(timerEdit, LEFT + GAP, AFTER + GAP);
			sc.add(passwordShowEdit, LEFT + GAP, AFTER + GAP);
			sc.add(passwordHidenEdit, LEFT + GAP, AFTER + GAP);
			sc.add(maskedEdit, LEFT + GAP, AFTER + GAP);
			sc.add(noPredictionEdit, LEFT + GAP, AFTER + GAP);
			sc.add(noPredictionMultiEdit, LEFT + GAP, AFTER + GAP, FILL - GAP, DP + 48);

		} catch (Exception ee) {
			MessageBox.showException(ee, true);
		}
	}

}
```
{% endcode %}

### Attributes

<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>String</b>
      </td>
      <td style="text-align:left">clearValueStr</td>
      <td style="text-align:left">stores the value that will be used by the clear() method to switch texts</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Byte</b>
      </td>
      <td style="text-align:left">captalise</td>
      <td style="text-align:left">
        <p>used to modify the the letter case from the text within the Edit:</p>
        <ul>
          <li>ALL_NORMAL: normal case</li>
          <li>ALL_LOWER: all lowercase</li>
          <li>ALL_UPPER: all uppercase</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>String</b>
      </td>
      <td style="text-align:left">caption</td>
      <td style="text-align:left">The Edit&apos;s placeholder text</td>
    </tr>
  </tbody>
</table>### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | Edit\( \) | Creates a box for user input |
| **Constructor** | Edit\(String mask\) | Creates a box for user input, but with a mask |
| **void** | setMode\(byte mode\) | Used to change the mode value to one of the accepted ones by the mode constants, without masking. To enable masking, you should use the setMode\(byte mode, boolean maskedEdit\) method, and pass the mode you wish and true on the second parameter |
| **void** | setEditable\(boolean on\) | will enable or disable the Edit. Can be used as a way to make sure the user don't modify something that was already saved on server and can't be modified without proper authorization |
| **String** | getText\( \) | Returns the text within the Edit, without care for the mask. It's important to note that in the case where there is mask, the characters from the mask will come with the user input, to get only the user input you should be using the getTextWithoutMask\(\) method to recover the text |
| **void** | setMaxLength\(\) | Is used to limit the characters number the user can digit on the text field |
| **void** | setPrediction\(boolean prediction\) | Is used to set if there should or not exist prediction on this Edit, it is, however set to true by default. |

### References

* See also our [quick tutorial video](https://www.youtube.com/watch?v=QIBNLwn8uYU) on creating Edits.
* See the [Java Docs ](https://rs.totalcross.com/doc/totalcross/ui/Edit.html)for more information.

