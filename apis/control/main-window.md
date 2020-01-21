# Main Window

## Overview

Every TotalCross program must have one and only one class that extends totalcross.ui. MainWindow. It is the interface between the VM and the TotalCross program: it receives all events and dispatches them.

## Usage

```java
import totalcross.ui.*;
public class MainWindowSample extends MainWindow {
	
	public MainWindowSample() {
		setUIStyle(Settings.MATERIAL_UI);
		setDefaultFont(Font.getFont(Fonts.FONT_DEFAULT_SIZE));
	}
	
	static {
		Settings.applicationId = "MWSP";
		Settings.appVersion = "1.0.1";
		Settings.iosCFBundleIdentifier = "com.totalcross.sample.mainwindowsample";
	}
	
	public void initUI() {
		// add controls here
	}
		​
	public void onExit() {
		// close stuff here
	}
}
```

The VM first calls the default `MainWindow` constructor \(in this case, `MainWindowSample()`\), and then queues a timer event, which calls the `initUI()` method inherited from the `Container` class. **You must initialize the entire user interface in the `initUI(`\) method.**

Initializing the UI in the constructor may hang the application and some operations can only be performed after the `initUI(MainWindow)` method is reached.

The **`onExit()`** method is called when the VM exits under normal circumstances, that is, if the user closes the application or the programmer terminates the application using `exit()` or `exec()` or even when the application is interrupted by an exception treated.

{% hint style="warning" %}
 In abnormal circumstances where a fatal error occurs by resetting the device, the `onExit()` method is not called. When this is called, all segments are already dead.
{% endhint %}

At **line 5** we use the **`setUIStyle()`** method to assign the style of our application as `Settings.MATERIAL_UI` **and so all components and effects will be in the Google** [**Material Design standard**](https://blog.totalcross.com/en/material-o-layout-da-google/)**.**

To change the font used by all the created controls, you must call the `setDefaultFont()` method on **line 6**. In this case, we are setting the default font size that we defined in the **Fonts class**. To better understand this process, just [**click here**.](https://totalcross.gitbook.io/playbook/guideline/colors-fonts-and-images#fonts)

Still, inside the constructor, you can define MainWindow title and/or style using `setTitle()` and `setBorderStyle()` methods however **there is performance loss**. To reverse this loss, you can use the `super(title, style)` method, but this method can not be used with `setDefaultFont()`. Styles for border can be:

* Window.NO\_BORDER;
* Window.RECT\_BORDER;
* Window.ROUND\_BORDER;
* Window.TAB\_BORDER;
* Window.TAB\_ONLY\_BORDER.

{% hint style="info" %}
But these decisions must be made on the **basis of the design of your application**. TotalCross recommends that you all follow [**Material Design.**](https://blog.totalcross.com/en/material-o-layout-da-google/)\*\*\*\*
{% endhint %}

## The Application Lifecycle

The application on TotalCross has a predefined life cycle, handled by defined methods in MainWindow:

| methods | Definition |
| :--- | :--- |
| initUI\(\): | called when the application starts. |
| onMinimize\(\): | called when the user press the home key, or when a call is received, or when the screen turns off. On Android and Windows 32, the application execution is not paused. On Windows Phone 8 and iOS, it is paused. |
| onResume\(\): | called after the call ends, the screen is turned on again, or the program was exited softly on Android. It is also called again if the user clicks on the application icon on Android and iOS. On WP8, it is necessary to press back in the main menu and click on the opened application. Clicking on its icon in the list of applications will kill the current instance and relaunches it again. |
| onExit\(\): | called when the system decides that is time to finish the application. If the home key was pressed, this method is called when another TotalCross application is launched on Android if the application is not installed as a single package.   If the user press the home key and then forces the application to stop \(by going to the Settings/Applications\) on Android and iOS, then all Litebase tables may be corrupted \(actually, no data is lost, but a TableNotClosedException will be issued\). So, it’s a good thing to call |
| LitebaseConnection.closeAll\(\) | in your Litebase instances in the onMinimize\(\) method and recover them in the onResume\(\) method. Just remember that all prepared statements, row iterators and result sets will be invalid and can’t be reused. Notice that the application might also be killed by the system if it’s on background. |

On WP8, there is no way to kill an application. To kill it, you must restore it pressing back in the main menu and them openning the application again. Then, press back until finishing the application.

It is also a good practice to save all necessary data and application state so that the when the user goes back to the application it won’t need to do a task again, such as entering data again in a form which was lost when the application was closed by the system. Of course there are situations where the user must retype data, such as login and password and when using bank applications.

Remember that applications for Android, iOS, and Windows Phone 8 shouldn’t have an exit button or an exit option in the menu. The application should be designed to be opened all the time and only the system should close it when needed. Again, there are exceptions, for example when the user doesn’t agree with an eula and the application can’t continue running.

Finally, it is a good idea to map the device back key on Android and WP8 to go back to the last window/menu used. Just remember that on WP8 back is back, you just can use it to go back to the last screen used. On the first screen, back should exit the application. The only exception are games, where back during a game play goes to the pause window.

## References

* To know more details about totalcross.ui.MainWindow, read its [JavaDocs](https://rs.totalcross.com/doc/).

