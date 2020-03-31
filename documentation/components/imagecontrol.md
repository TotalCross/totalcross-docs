# ImageControl

### Overview

A control that can show an image bigger than its area and that can be dragged using a pen to show the hidden parts.

Note that, by default, events \(and dragging\) are disabled. You must call setEventsEnabled to allow dragging.

### Source Code

{% code title="Login TCSample" %}
```java
import java.sql.SQLException;

import totalcross.db.sqlite.SQLiteUtil;
import totalcross.io.IOException;
import totalcross.sample.util.Colors;
import totalcross.sql.PreparedStatement;
import totalcross.sql.Statement;
import totalcross.sys.Settings;
import totalcross.sys.Vm;
import totalcross.ui.Button;
import totalcross.ui.Check;
import totalcross.ui.Container;
import totalcross.ui.Edit;
import totalcross.ui.ImageControl;
import totalcross.ui.ScrollContainer;
import totalcross.ui.dialog.MessageBox;
import totalcross.ui.event.ControlEvent;
import totalcross.ui.event.Event;
import totalcross.ui.gfx.Color;
import totalcross.ui.image.Image;
import totalcross.ui.image.ImageException;
import totalcross.util.InvalidDateException;

public class Login extends ScrollContainer {
	private Edit edPass, edLogin;
	private Check ch;
	private Button btLogin, btRegister;
	private ImageControl ic;
    private SQLiteUtil util;
	
	public void initUI(){
		try {
			setBackForeColors(Colors.BACKGROUND, Colors.ON_BACKGROUND);
			ic = new ImageControl(new Image("images/logo.png"));
			ic.scaleToFit = true;
			ic.centerImage = true;
			add(ic, LEFT, TOP+100, FILL, PARENTSIZE+30);
			
			edLogin = new Edit();
			edLogin.caption = "Login";
			//edLogin.setBackColor(Color.RED);
			add(edLogin, CENTER, AFTER+60, PARENTSIZE+90, PREFERRED+30);
			
			edPass = new Edit();
			edPass.caption = "Password";
			//edPass.setBackColor(Color.RED);
			edPass.setMode(Edit.PASSWORD_ALL);
			add(edPass, SAME, AFTER+70, PARENTSIZE+90, PREFERRED+30);
			
			ch = new Check("Remember Me");
			add(ch, LEFT+86, AFTER+100, PARENTSIZE, PREFERRED+30);
			
			btLogin = new Button("Login");
			btLogin.setBackColor(Color.WHITE);
			add(btLogin, CENTER, AFTER+140, PARENTSIZE+80, PREFERRED+60);
			
			btRegister = new Button("Register Now");
			btRegister.transparentBackground = true;
			btRegister.setBorder(BORDER_NONE);
			add(btRegister, CENTER, AFTER, PARENTSIZE+30, PREFERRED+20);
			btRegister.addPressListener(e -> {Vm.exec("url", "http://www.totalcross.com", 0, true);});
			
			//Creating Database
			util = new SQLiteUtil(Settings.appPath,"database.db");
	        Vm.debug(util.fullPath);
			    
	        Statement st = util.con().createStatement();
			st.execute("create table if not exists person (login varchar(20), password varchar(20))");
			st.close();
		
		} catch (IOException | ImageException | SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	
	public void onEvent(Event e){
		try{
			switch(e.type){
				case ControlEvent.PRESSED:
					if(e.target == btLogin){
						doInsert();
					}
			}
		}catch(Exception ee){
			MessageBox.showException(ee, true);
		}
	}
	
	private void doInsert() throws SQLException, InvalidDateException, ImageException {
		if (edLogin.getLength() == 0 || edPass.getLength() == 0){
			MessageBox mb = new MessageBox("Message","Please fill all fields!",new String[]{"Close"});
			mb.setBackForeColors(Color.WHITE, Color.BLACK);
			mb.popup();
		}else {
		// simple example of how you can insert data into SQLite..
			String sql = "insert into person values(?,?)";
			PreparedStatement st = util.con().prepareStatement(sql);
			st.setString(1, edLogin.getText());
			st.setString(2, edPass.getText());
			st.executeUpdate();
			st.close();		
			
			MessageBox mbox = new MessageBox(null,"Data inserted successfully!");
			mbox.setBackForeColors(Color.WHITE, Color.BLACK);
			mbox.popup();
			
		}
	}
}

```
{% endcode %}

{% hint style="warning" %}
Do not forget **to create a folder** called "_**images**_" inside _**/src/main/resources**_ and **save the logo**[**.**](https://github.com/TotalCross/TCSample/blob/master/src/main/resources/images/alligator.gif)**png image inside it** \[images\].
{% endhint %}

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | ImageControl\(Image img\) | Constructs an ImageControl using the given image. |
| **Constructor** | ImageControl\(\) | Constructs with no initial image. You must set the image with the setImage method. |
| **void** | setEventsEnabled\(boolean enabled\) | Pass true to enable dragging and events on the image. |
| **void** | setImage\(Image img\) | Sets the image to the given one. If the image size is different, you must explicitly call setRect again if you want to resize the control. |
| **void** | setImage\(Image img, boolean resetPositions\) | Sets the image to the given one, optionally resetting the image position. If the image size is different, you must explicitly call setRect again if you want to resize the control. |
| **int** | getImageHeight\(\) | Returns the image's height; when scaling, returns the scaled height |
| **int** | getImageWidth\(\) | Returns the image's width; when scaling, returns the scaled width.  |
| **Image** | getImage\(\) | Returns the current image assigned to this ImageControl. |
| **void** | setBackground\(Image img\) | Sets the given image as a freezed background of this image control.  |
| **boolean** | moveTo\(int newX, int newY\) | Moves to the given coordinates, respecting the current moving policy regarding  |

### References

* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/ImageControl.html) for more information.
* See the code on [Github](https://github.com/TotalCross/TCSample/blob/master/src/main/java/totalcross/sample/components/ui/Login.java)



