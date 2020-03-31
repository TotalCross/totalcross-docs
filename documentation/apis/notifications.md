# Notifications

Notification is a message that will be displayed to the user outside of the application’s usual UI.

When you execute a command telling the system to issue a notification, it will appear as an icon in the notification area, and to see the details, the user opens the **notification space**.

{% hint style="info" %}
The notification space is this area where the details are shown \(also called the notification drawer\) are areas controlled by the system and the user can see at any time.
{% endhint %}

### Creation of a Notification

* To specify actions and information that will be displayed to the user, use a `Notification.Builder` object.

* To create a push notification, use `Notification.Builder.build()`, which is an example of the type of `notification` provided as previously defined specifications.

* To notify a notification, simply pass the `Notification` object using `NotificationManager.getInstance().Notify();`

### Content Needed to Create a Notification

The object on smartphones should contain the following:

* A title, defined by `title();`
* Detail text, defined by `text();`

### A Simple Example

{% code title="HelloTCNotification" %}
```java
import totalcross.notification.Notification;
import totalcross.notification.NotificationManager;
import totalcross.sys.Settings;
import totalcross.ui.Button;
import totalcross.ui.Edit;
import totalcross.ui.MainWindow;

public class HelloWorld extends MainWindow {
	private Button btnHello;

	public HelloWorld(){
		super("", NO_BORDER);
		Settings.uiAdjustmentsBasedOnFontHeight = true;
		setUIStyle(Settings.Material);
	}

	public void initUI() {
		Edit title = new Edit("Title");
		title.caption = "Title";
		add(title, LEFT+150, TOP+100, FILL-150, PREFERRED);
		
		Edit text = new Edit("Text");
		text.caption = "Text";
		add(text, LEFT+150, AFTER+50, FILL-150, PREFERRED);
		
		btnHello = new Button("Notify!");
		btnHello.addPressListener(
				(e) -> {
					Notification.Builder builder = new Notification.Builder();
					Notification notification = builder
							.title(title.getText())
							.text(text.getText())
							.build();
					NotificationManager.getInstance().notify(notification);
				});
		add(btnHello, CENTER, AFTER+150, PARENTSIZE+38, PARENTSIZE+8);
	  }
}
```
{% endcode %}

### References

* to see the complete example, go to our [GitHub](https://github.com/TotalCross/Notifications)
* You can also view this [quick tutorial video](https://www.youtube.com/watch?v=Y1_0c9H8G4E) on how to create notifications.

