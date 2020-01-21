# Radio Group

### Overview

A radio group is a group of [Radios](https://totalcross.gitbook.io/playbook/ui-ux-api/radio) \(**`RadioButton`**\). It allows a user to select at most one radio from a set. Checking one RadioButton that belongs to a radio group unchecks any previous checked radio button within the same group.

![](../.gitbook/assets/radio-sample.gif)

### Source Code

{% code title="RadioGroupControllerSample.java" %}
```java
  // Creating a RadioGroup
RadioGroupController radioGroup = new RadioGroupController();
  // Assigning RadioButtons to the RadioGroup
Radio radio = new Radio("RadioButton", radioGroup);
add(radio, LEFT+100, AFTER+100 ,PREFERRED+100,PREFERRED+25);
```
{% endcode %}

{% hint style="info" %}
To see the complete example [click here](https://github.com/TotalCross/RadioSample/blob/master/src/main/java/radioButton/RadioButton.java).
{% endhint %}

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **boolean** | sendPressOnLast | Set to false to disable sending PRESSED events to the previous control |

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | RadioGroupController\( \) | Instance a empty RadioGroupController |
| **int** | add\(Radio newMember \) | Adds a new Radio to the list of Radios this controller handles |
| **Radio** | getRadio\(int idx\) | Returns the Radio at the given index |
| **int** | getSelectedIndex\( \) | Returns the currently selected index \(in the order that the Radios were added to the container\), or -1 if none |
| **Radio** | getSelectedItem\( \) | Returns the currently selected Radio, or null if none |
| **int** | getSize\( \) | Returns the number of Radio's |
| **void** | remove\(Radio oldMember\) | Removes the given Radio from the list of Radios this controller handles |
| **void** | setSelectedIndex\(int i\) | Selects the given radio and deselects the other one |
| **void** | setSelectedItem\(String text\) | Selects a radio whose text matches the given caption |
| **void** | setSelectedItem\(String text, boolean caseInsensitive\) | Selects a radio whose text starts with the given caption |

### **References**

* See the [JavaDocs](https://rs.totalcross.com/doc/totalcross/ui/RadioGroupController.html) for more information

