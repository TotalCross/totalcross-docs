---
description: >-
  Buttons are an essential way to interact with and navigate through an app, and
  should clearly communicate what action will occur after the user taps them
---

# Button

## Examples

To adapt the component to the style of the application it is often necessary to change its colors.

![](../../.gitbook/assets/image%20%2867%29.png)

```java
package com.totalcross;
import totalcross.ui.gfx.Color;
import totalcross.sys.Settings;
import totalcross.ui.Button;
import totalcross.ui.MainWindow;
public class HelloWorld extends MainWindow {

    private Button btnRed;
    private Button btnGreen;
    private Button btnBlue;
    public HelloWorld(){
        setUIStyle(Settings.MATERIAL_UI);
    }
    @Override
    public void initUI(){
        btnRed = new Button("Red");
        btnRed.setBackForeColors(Color.RED, Color.WHITE);
        add(btnRed, CENTER,CENTER );
        
        btnGreen = new Button("Green");
        btnGreen.setBackForeColors(Color.GREEN, Color.WHITE);
        add(btnGreen, CENTER, AFTER );
        
        btnBlue = new Button("Blue");
        btnBlue.setBackForeColors(Color.BLUE, Color.WHITE);
        add(btnBlue, CENTER,AFTER);
    }
}
```

## Full Button

![](../../.gitbook/assets/image%20%2863%29.png)

Make the button the width of the screen.

```java
package com.totalcross;
import totalcross.ui.gfx.Color;
import totalcross.sys.Settings;
import totalcross.ui.Button;
import totalcross.ui.MainWindow;
public class HelloWorld extends MainWindow {

    private Button btnFull;
    
    public HelloWorld(){
        setUIStyle(Settings.MATERIAL_UI);
    }
    @Override
    public void initUI() {
        btnFull = new Button("Full Button");
        btnFull.setBackForeColors(Color.BLUE, Color.WHITE);
        add(btnFull, CENTER, CENTER, PARENTSIZE, PREFERRED);

    }
}
```

## Button shapes

![](../../.gitbook/assets/image%20%2843%29.png)

Modify the button edges.

```java
package com.totalcross;
import totalcross.ui.gfx.Color;
import totalcross.sys.Settings;
import totalcross.ui.Button;
import totalcross.ui.MainWindow;
public class HelloWorld extends MainWindow{

    private Button btnRounded;
    private Button btnBorderless;
    private Button btnOutlined;
    
    public HelloWorld(){
        setUIStyle(Settings.MATERIAL_UI);
    }
    @Override
    public void initUI(){
        btnRounded = new Button("Rounded Corners Button", Button.BORDER_ROUND);
        btnRounded.setBackForeColors(Color.BLUE, Color.WHITE);
        add(btnRounded, CENTER, CENTER );

        btnBorderless = new Button("Borderless Button", Button.BORDER_NONE);
        btnBorderless.setBackForeColors(Color.BLUE, Color.WHITE);
        add(btnBorderless, CENTER, AFTER+5);
        
        btnOutlined = new Button("Outlined Button", Button.BORDER_OUTLINED);
        btnOutlined.setBackForeColors(Color.BLUE, Color.WHITE);
        add(btnOutlined, CENTER, AFTER+5);

    }
}
```

## Sizes

![](../../.gitbook/assets/image%20%2894%29.png)

Change the size of the buttons.

```java
package com.totalcross;
import totalcross.ui.gfx.Color;
import totalcross.sys.Settings;
import totalcross.ui.Button;
import totalcross.ui.MainWindow;
public class HelloWorld extends MainWindow {

    private Button btnLarge;
    private Button btnDefaultSize;
    private Button btnSmall;
    
    public HelloWorld() {
        setUIStyle(Settings.MATERIAL_UI);
    }
    @Override
    public  void  initUI() {
        
        btnLarge = new Button("Large",Button.BORDER_ROUND);
        btnLarge.setBackForeColors(Color.BLUE, Color.WHITE);
        add(btnLarge, LEFT+20, CENTER,btnLarge.getPreferredWidth() <=  48  ? DP +  96: btnLarge.getPreferredWidth(),DP +  54);
        
        btnDefaultSize = new Button("Default",Button.BORDER_ROUND);
        btnDefaultSize.setBackForeColors(Color.BLUE, Color.WHITE);
        add(btnDefaultSize, AFTER+5, CENTER_OF);
        
        btnSmall = new Button("Small",Button.BORDER_ROUND);
        btnSmall.setBackForeColors(Color.BLUE, Color.WHITE);
        add(btnSmall, AFTER+5, CENTER_OF, btnSmall.getPreferredWidth() <=  24? DP +  48  : btnSmall.getPreferredWidth(), DP +  27,btnDefaultSize);
        
    }
}
```

## Button image

![](../../.gitbook/assets/image%20%2879%29.png)

Add an image to the button.

```java
package com.totalcross;
import totalcross.ui.gfx.Color;
import totalcross.ui.image.Image;
import totalcross.sys.Settings;
import totalcross.ui.Button;
import totalcross.ui.MainWindow;
public class HelloWorld extends MainWindow {

    private Button btnLeftImage;
    
    public HelloWorld() {
        setUIStyle(Settings.MATERIAL_UI);
    }
    @Override
    public void initUI() {
        try {
            Image img = new Image("images/bt_info.png");
            btnLeftImage = new Button("Left Image", img.scaledBy(0.2,0.2), RIGHT,10);
            btnLeftImage.setBackForeColors(Color.BLUE, Color.WHITE);
            add(btnLeftImage, CENTER, AFTER+25);    
        } catch (Exception exception) {
            exception.printStackTrace();
        }       
    }
}
```

{% hint style="warning" %}
Do not forget **to create a folder** called "_**images**_" inside _**/src/main/resources**_ and **save the** [**bt\_info.png**](https://github.com/TotalCross/TCSample/blob/master/src/main/resources/images/bt_info.png) **image inside it** \[images\].
{% endhint %}

## Behind the Class

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **boolean** | Button.CENTRALIZE | Center image and text on the button. |

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | Button\( \) | Creates a simple button |
| **Constructor** | Button\(Image img\) | Creates a simple button with the referred image |
| **Constructor** | Button\(Image img, byte border\) | Creates a button with the referreds image and border |
| **Constructor** | Button\(String text\) | Creates a button with the referred text |
| **Constructor** | Button\(String text, byte border\) | Creates a button with the referreds text and border |
| **Constructor** | Button\(String text, Image img, int textPosition, int gap\) | Creates a button with the referred text and image |
| **Image** | getImage\( \) | Return the button image |
| **String** | getText\( \) | Return the button text |
| **Boolean** | isPressed\( \) | Return true if button is pressed |
| **void** | press\(boolean pressed\) | If true, press the button |
| **void** | setBorder\(byte border\) | Set the button border style |
| **void** | setImage\(Image img\) | Set the button image |
| **void** | setPressedColor\(int newColor\) | Return the button text |
| **void** | setText\(String text\) | Set the button text |
| **void** | simulatePress\( \) | Press and depress the button |

## **References**

* See also our [quick tutorial video](https://www.youtube.com/watch?v=xjqd3g1IYco) on creating buttons.
* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/Button.html) for more information.

