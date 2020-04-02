---
description: >-
  An Edit is a field used to show and alter texts. Also known as UITextField on
  Swift and input on HTML. There also is some variations, like Outlined Edit,
  Calculator Edit, Password Edit, etc.
---

# Edit

## Examples

![](../../.gitbook/assets/image%20%2869%29.png)

In most applications is necessary to remove the background from the object and change the color of the element so that it is better viewed.

```java
package com.totalcross;
import totalcross.sys.Settings;
import totalcross.ui.Edit;
import totalcross.ui.MainWindow;
import totalcross.ui.dialog.MessageBox;
import totalcross.ui.gfx.Color;
import totalcross.util.UnitsConverter;

public class HelloWorld extends MainWindow {
    private Edit simpleEdit;
    private int GAP = UnitsConverter.toPixels(DP +  15);

    public HelloWorld(){
        setUIStyle(Settings.MATERIAL_UI);
    }  

    @Override
    public void initUI(){
        try{
            simpleEdit = new Edit();
            simpleEdit.caption = "Simple Edit";
            simpleEdit.transparentBackground = true;
            simpleEdit.captionColor = Color.RED;
            simpleEdit.setForeColor(Color.RED);

            add(simpleEdit, LEFT + GAP, AFTER + GAP);
        } catch (Exception e) {
            MessageBox.showException(e, true);
        }
    }
}
```

## Numeric edit

![](../../.gitbook/assets/image%20%2862%29.png)

In some situations, entry should be limited to numbers.

```java
package com.totalcross;
import totalcross.sys.Settings;
import totalcross.ui.Edit;
import totalcross.ui.MainWindow;
import totalcross.ui.dialog.MessageBox;
import totalcross.util.UnitsConverter;

public class HelloWorld extends MainWindow {

    private Edit numericEdit;
    private Edit calculatorEdit;
    private int GAP = UnitsConverter.toPixels(DP +  15);
    
    public HelloWorld(){
        setUIStyle(Settings.MATERIAL_UI);
    }  
    @Override
    public void initUI(){
        try{
            numericEdit = new Edit();
            numericEdit.caption =  "NumericBox Edit";
            numericEdit.setMode(Edit.CURRENCY);
            numericEdit.setKeyboard(Edit.KBD_NUMERIC);  
            add(numericEdit, LEFT + GAP, AFTER + GAP);
            
            calculatorEdit =  new  Edit();
            calculatorEdit.caption =  "Calculator Edit";
            calculatorEdit.setMode(Edit.CURRENCY, true);
            add(calculatorEdit, LEFT + GAP, AFTER + GAP);
        } catch (Exception  ee) {
            MessageBox.showException(ee, true);
        }
    }
}
```

## Password Edit

![](../../.gitbook/assets/image%20%2834%29.png)

If the entry is a password, it should not be possible to see it.

```java
package com.totalcross;
import totalcross.sys.Settings;
import totalcross.ui.Edit;
import totalcross.ui.MainWindow;
import totalcross.ui.dialog.MessageBox;
import totalcross.util.UnitsConverter;

public class HelloWorld extends MainWindow {
    private Edit passwordShowEdit;
    private Edit passwordHidenEdit;
    private int GAP = UnitsConverter.toPixels(DP +  15);

    public HelloWorld(){
        setUIStyle(Settings.MATERIAL_UI);
    }  
    @Override
    public void initUI(){
        try{
            passwordShowEdit = new Edit();
            passwordShowEdit.caption = "Password Edit (last character is shown)";
            passwordShowEdit.setMode(Edit.PASSWORD);
            add(passwordShowEdit, LEFT + GAP, AFTER + GAP);
            
            passwordHidenEdit =  new  Edit();
            passwordHidenEdit.caption =  "Password Edit (all characters are hidden)";   
            passwordHidenEdit.setMode(Edit.PASSWORD_ALL);
            add(passwordHidenEdit, LEFT + GAP, AFTER + GAP);
        }catch (Exception  ee) {
            MessageBox.showException(ee, true);
        }
    }
}
```

## Edit shapes

![](../../.gitbook/assets/image%20%2829%29.png)

To receive different input formats, which are not predefined in TotalCross.

```java
package com.totalcross;
import totalcross.sys.Settings;
import totalcross.ui.Edit;
import totalcross.ui.MainWindow;
import totalcross.ui.dialog.MessageBox;
import totalcross.util.UnitsConverter;

public class HelloWorld extends MainWindow {
    private Edit calendarEdit;
    private Edit timerEdit;
    private Edit maskedEdit;
    private int GAP = UnitsConverter.toPixels(DP +  15);

    public HelloWorld(){
        setUIStyle(Settings.MATERIAL_UI);
    }  

    @Override
    public void initUI(){
        try{
            calendarEdit = new Edit("99/99/99");
            calendarEdit.caption =  "Calendar Edit";
            calendarEdit.setMode(Edit.DATE, true);
            add(calendarEdit, LEFT + GAP, AFTER + GAP);

            timerEdit = new Edit("99"  + Settings.timeSeparator +  "99"  + Settings.timeSeparator +  "99");
            timerEdit.caption = "TimeBox Edit (24-hour format)";
            timerEdit.setValidChars("0123456789AMP");
            timerEdit.setMode(Edit.NORMAL, true);
            timerEdit.setKeyboard(Edit.KBD_TIME);
            add(timerEdit, LEFT + GAP, AFTER + GAP);

            maskedEdit = new Edit("999.999.999-99");
            maskedEdit.caption = "Masked Edit (999.999.999-99)";
            maskedEdit.setMode(Edit.NORMAL, true);
            maskedEdit.setValidChars(Edit.numbersSet);
            add(maskedEdit, LEFT + GAP, AFTER + GAP);
        }catch (Exception  ee){
            MessageBox.showException(ee, true);
        }
    }
}
```

## Behind the Class

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

