# Floating Button

### Overview

Floating Button is a circular floating button that keeps fixed on its initial position and, usually, is used for the main action of the screen.

![](../.gitbook/assets/floatingbutton.gif)

### Source Code

{% code title="FloatButton" %}
```java
Image ic = null;
try {
  ic = new Image("images/floatbtn.png");
} catch (IOException e) {
  e.printStackTrace();
} catch (ImageException e) {
  e.printStackTrace();
}
FloatingButton floatbutton = new FloatingButton(ic);
floatbutton.setBackColor(Color.getRGB(109, 156, 232));
floatbutton.setIconSize(30);
add(floatbutton, RIGHT-40, BOTTOM-40);

```
{% endcode %}

{% hint style="warning" %}
Do not forget **to create a folder** called "_**images**_" inside _**/src/main/resources**_ and **save the** [**floatbtn.png**](https://github.com/TotalCross/TCSample/blob/master/src/main/resources/images/floatbtn.png) **image inside it** \[images\].
{% endhint %}

### Métodos

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | FloatingButton\( \) | Creates a Floating Button with a predefined icon. |
| **Constructor** | FloatingButton\(Image foregroundImage\) | Creates a Floating Button with setting the icon. |
| **void** | setIcon\(image foregroundImage\) | Sets the Floating Button icon. |
| **void** | setIconSize\(int iconsize\) | Sets the Floating Button icon size. |
| **Image** | getIcon\( \) | Returns the Image that represents the Floating Button icon. |
| **int** | getIconSize\( \) | Returns the size of the Floating Button icon. |

