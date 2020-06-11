# Window

## Overview

As you already know, a TotalCross program with user interface consists of one and only one main window \(a class that directly or indirecly extends MainWindow\). This main window can pop up a window, and this new window can pop up another one, and so on. Windows in TotalCross are always modal, therefore, only the last popped up window can receive events and you cannot switch from the topmost Window to the previous without closing the topmost one.

Although the Window class extends Control, you can’t add a Window to a Container. Doing this results in a RuntimeException. To show a window, you must use the method `popup()` or the method `popupNonBlocking().`

If you want to know more about how differences between windows and container, how to navigate between interfaces and what are the best ways to handle containers and windows, just click on the link below:

{% page-ref page="../../guides/app-architecture/container-x-window.md" %}

## Usage

### create a popup window class:

{% code title="TestWindow" %}
```java
class TestWindow extends Window{
	
	public void onPopup() {
	 	logo = new ImageControl(Images.logo_branco);
		logo.scaleToFit = true;
		logo.centerImage = true;
		logo.transparentBackground = true;
		add(logo, CENTER, CENTER, PARENTSIZE + 50, PARENTSIZE + 50);

		FadeAnimation.create(logo, true, null, 3000)
				.then(FadeAnimation.create(logo, false, this::onAnimationFinished, 3000)).start();
	}
	
	public void onAnimationFinished(ControlAnimation anim) {
		this.unpop(); // a WINDOW_CLOSED event will be posted to this PARENT window.
	}
}
```
{% endcode %}

### Blocking

```java
public class Launcher extends MainWindow{
	Button btn;
	
	public void onEvent(Event e){
		if (e.target == btn){
			TestWindow tw = new TestWindow();
			tw.popup(); // this line is only executed after the window is closed.
		}
	}
}
```

### Non-blocking

To use it non-blocking \(the execution continues right after the popup command, even with the window still open\):

```java
public class Launcher extends MainWindow
{
	TestWindow tw;
	public void initUI()
	{
		tw = new TestWindow();
		tw.popupNonBlocking(); // this line is executed immediately
	}
	public void onEvent(Event event)
	{
		if (event.target == tw && event.type == ControlEvent.WINDOW_CLOSED)
		{
			// any stuff
			break;
		}
	}
}
```

Blocking popup may be use in InputBox/MessageBox classes, while non-blocking popup is used in MenuBar and other classes. 

Important note: you can’t use `popup()` with a delay to unpop it. In this case, the correct would be to use `popupNonBlocking()`:

```java
mb = new MessageBox(...);
mb.popupNonBlocking();
Vm.sleep(5000); // or do something else
mb.unpop();
```

If you use `popup()` in this specific case, the VM will hang.

## Others features of the Window Class

* Windows can have a title that can be set by the method setTitle\(String title\) \(which calls repaint\(\)\) or passed to the constructor. 
* The window border can be selected from one of the multiple styles shown below, by using the setBorderStyle\(byte borderStyle\) method or passing the desired style to the Window constructor. The parameter value can be NO\_BORDER, RECT\_BORDER, ROUND\_ BORDER, TAB\_BORDER, TAB\_ONLY\_BORDER, HORIZONTAL\_GRADIENT, or VERTICAL\_ GRADIENT. To retrive it, use getBorderStyle\(\). 
* There are two constructors: the default one, that creates a window with no title and no border, and one constructor with both title and border parameters.

  * `Window()`;
  * `Window(String title, byte borderStyle)`

* Windows can be moved around the screen by dragging the window’s title. If the window has no title, it can’t be moved. You can make a titled window unmovable by calling the makeUnmovable\(\) method. 
* The title font can be changed using the setTitleFont\(\) method. To retrive it, use getTitleFont\(\). By default, the font is the one used by the main window, with bold style. 
* Only one control can hold the focus at a time. To change focus to another control, use the setFocus\(Control c\) method \(this can also be done through the requestFocus\(\) method in the totalcross.ui.Control class\). When a user types a key, the control with focus gets the key event. Calling this method will cause a FOCUS\_OUT control event to be posted to the window’s current focus control \(if one exists\) and will cause a FOCUS\_IN control event to be posted to the new focus control. The getFocus\(\) method returns the control that currently owns the focus. 
* The rectangle area excluding the border and the title is defined as the client rectangle. You can get it with the getClientRect\(\) method. 
* A window can be popped up by calling the popupNonBlocking\(\) method and can be unpopped by calling the unpop\(\) method. The popup process saves the area behind the window that is being popped up and the unpop process restores that area. The unpop\(\) method posts a ControlEvent.WINDOW\_CLOSED event to the caller window. The popupNonBlocking\(\) method can be called like this.popupNonBlocking\(\). Calling unpop\(\) when only the MainWindow is active does nothing. 
* A window can also be popped up by calling the popup\(\) method, and be unpopped by the same unpop\(\) method described above. The big difference is that in popupNonBlocking\(\), the program execution continues to the next line, while in popup\(\), the program execution is halted and only continues when the popped up window is dismissed. Menu, MessageBox, ComboBox, and ComboBoxDropDown are popped up using popupNonBlocking\(\), because execution does not need to be halted. InputDialog, Calendar, and Calculator are usually popped up using popup\(\) because the user may want to get the result of the dialog in an easy way. You can’t use `popup()` to popup alternating windows that call each other recursively. For example, suppose that from win1 you call win2.popup\(\), then at win2 you call `unpop()` and then win1.`popup()`. Then, from win1 you do `unpop()` again and win2.popup\(\), and so on. This will lead to an OutOfMemoryError on the device due to a native stack overflow. To fix this, just replace the popup by popupNonBlocking\(\). 
* The topmost window \(the one who receive events\) can be obtained with the static method `getTopMost().` To check if this window is the topmost, use the `isTopMost()` method. 
* Try `setGrabPenEvents()` for settting to a control to redirect all pen events directly to it. This method speeds up pen event processing. Used in Whiteboard class. 
* You may check if this window is visible using the isVisible\(\) method. This method is inherited from totalcross.ui.Control, but it simply checks if the current window is the topmost one. 
* Each window can have a menu attached by using the method setMenuBar\(\). The menuBar can be made visible programatically by calling the popupMenuBar\(\) method. 
* Suppose you wish to allow the user to abort a task being executed by pressing. You can use the method pumpEvents\(\) to process all events in the queue. This method is used to implement a blocking Window. Here is an example:  
  `while(someCondition)   
    Event.pumpEvents(); Event.pumpEvents();`

* The methods getPreferredWidth\(\) and getPreferredHeight\(\) have a special meaning for the Window class. They return the minimum width/height needed for the correct display of this window. getPreferredWidth\(\) returns the width of the title \(if any\) plus the width of the border \(if any\). getPreferredHeight\(\) returns the height of the title \(if any\) plus the height of the border \(if any\).

## **Protected methods**

There are some useful protected methods that may be implemented by controls that extend totalcross.ui.Window. Those methods are placeholders and there is no need to call the super method.

| **Methods** | Definitions |
| :--- | :--- |
| onClickedOutside\(int x, int y\): | This method is used in popup windows. If the user clicks outside the window’s bounds, this method is called giving the absolute coordinates of the clicked point. There are two options: If you had handled the action, return true in this method. Otherwise, false must be returned and if the beepIfOut member is true, a beep is played \(in other words, beepIfOut can be set to false to disable this beep\). |
| onPopup\(\): | Called just after the behind contents are saved and before the popup process begin. When this method is called, the topmost window is still the parent of the window being popped up. |
| postPopup\(\): | Called after the popup process ended. When this method is called, the popped up window is fully functional. It is a good place to put a control.requestFocus\(\) to make the window popup with the focus in a default control. |
| onUnpop\(\): | Called just before the unpop process begin. |
| postUnpop\(\): | Called after the unpop process ended. When this method is called, the unpopped window has gone away and the parent window is currently the topmost. |
| postPressedEvent\(\): | Posts a ControlEvent.PRESSED event on the focused control. |

A very common mistake is to popup a window without setting its bounds. If no bounds are set, the window will not receive events.

## **Other Members**

The other members that can be used \(all public and some protected\) of the Window class are explained here:

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Members</b>
      </th>
      <th style="text-align:left">Definitons</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">needsPaint</td>
      <td style="text-align:left">
        <p></p>
        <p>true if there are any controls marked for repaint (some area of the window
          is invalidated).
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">tempTitle</td>
      <td style="text-align:left">A temporary title that will be displayed when the Window pops up. It will
        be replaced by the original title when it is closed.</td>
    </tr>
    <tr>
      <td style="text-align:left">topmost</td>
      <td style="text-align:left">Stores the topmost window.</td>
    </tr>
    <tr>
      <td style="text-align:left">firstFocus</td>
      <td style="text-align:left">The control that should get focus when a focus traversal key is pressed
        and none has focus.</td>
    </tr>
    <tr>
      <td style="text-align:left">canDrag(protected)</td>
      <td style="text-align:left">
        <p></p>
        <p>If true and if this is a popup window, the user is allowed to drag the
          title and make the window move around.
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">cancelPenUp</td>
      <td style="text-align:left">If true, the next PEN_UP event will be ignored. This is used when a PEN_DOWN
        cancels a flick, or if a drag-scrollable control needs to cancel the next
        pen_up during a drag-scrolling interaction.</td>
    </tr>
    <tr>
      <td style="text-align:left">gradientTitleStartColor</td>
      <td style="text-align:left">The starting and ending colors used to fill the gradient title.</td>
    </tr>
    <tr>
      <td style="text-align:left">gradientTitleEndColor</td>
      <td style="text-align:left">The starting and ending colors used to fill the gradient title.</td>
    </tr>
    <tr>
      <td style="text-align:left">titleColor</td>
      <td style="text-align:left">The title color depends on the border type: it will be the foreground
        color if NO_BORDER is set; otherwise, it will be the background color.</td>
    </tr>
    <tr>
      <td style="text-align:left">titleGap</td>
      <td style="text-align:left">A vertical gap used to increase the title area. Defaults to fmH/2 on Android
        and 0 on other user interface styles.</td>
    </tr>
    <tr>
      <td style="text-align:left">titleAlign</td>
      <td style="text-align:left">The title horizontal alignment in the window&#x2019;s title area. It can
        be LEFT, CENTER, or RIGHT, and you can use an adjustment on the value (E.G.:
        LEFT+5).</td>
    </tr>
    <tr>
      <td style="text-align:left">headerColor, footerColor</td>
      <td style="text-align:left">Has the header and the footer colors when on Android style and border
        type is ROUND_BORDER. Not used on other styles.</td>
    </tr>
    <tr>
      <td style="text-align:left">fadeOtherWindows</td>
      <td style="text-align:left">Set to true to make the other windows be faded when the window appears.</td>
    </tr>
    <tr>
      <td style="text-align:left">fadeValue
        <br />
      </td>
      <td style="text-align:left">The value used to fade the other windows. Defaults to 128.</td>
    </tr>
    <tr>
      <td style="text-align:left">robot</td>
      <td style="text-align:left">The UIRobot instance that is being used to record or play events.</td>
    </tr>
  </tbody>
</table>

Never mess with the public member zStack. It is used to store the windows that are currently popped up. It is made public because the totalcross.Launcher class uses it.

## How controls inside a window are repainted:

* The programmer calls the `repaint()` method of some controls, or a control is clicked and marks itself for repaint. 
* The `damageRect(`\) method in class window creates a rectangle \(stored in the paintX, paintY, paintWidth and paintHeight members\) with the union of the bounds of all controls marked for repaint. 
* The next time a VM event is posted, the `_doPaint()` method of the topmost window is called. This method paints the window’s title/border \(if any\) and calls the onPaint\(\) method of all containers and controls that lies inside the rectangle area marked for repaint. This explains why nothing in the window is updated when you receive events directly from a native library \(the Scanner class, for example\). Because the VM is not receiving the event, it never validates the window. In these cases, you must update the window yourself, calling repaintNow\(\) or the validate methods.

Many classes in the totalcross.ui package extend totalcross.ui.Window. Examples of such classes are `CalculatorBox` and `CalendarBox`. Other good examples are `ComboBoxDropDown` and `MessageBox`.

It’s important to be aware that it is not a good practice to create classes that extend Window if they will occupy the whole screen, because they use a lot of memory to store the underlying area. Opening the menu may lead to time-consuming redraws of all opened windows due to out-of-memory problems. In these cases, it is better to use `Containers`.

