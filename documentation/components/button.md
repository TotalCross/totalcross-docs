# Button

### Overview

Buttons are an essential way to interact with and navigate through an app, and should clearly communicate what action will occur after the user taps them, like invoke an action to confirm \[ok\] or cancel \[cancel\] something. The Buttons can consist of text and/or icon/image, and can be enhanced with a variety of attributes. Here is a sample with some buttons using the Material Design style from Google \(now inside the UI package from the TotalCrossAPI sample\).

![](../../.gitbook/assets/buttons-sample.gif)

### Source Code

{% code title="ButtonSample.java" %}
```java
import totalcross.sys.Settings;
import totalcross.ui.Button;
import totalcross.ui.Label;
import totalcross.ui.ScrollContainer;
import totalcross.ui.font.Font;
import totalcross.ui.gfx.Color;
import totalcross.ui.image.Image;
import totalcross.util.UnitsConverter;

public class ButtonSample extends ScrollContainer {

	private Button btnDefaultColor;
	private Button btnRed;
	private Button btnGreen;
	private Button btnBlue;
	private Button btnFull;
	private Button btnRounded;
	private Button btnBorderless;
	private Button btnLeftImage;
	private Button btnRightImage;
	private Button btnImage;
	private Button btnLarge;
	private Button btnOutlined;
	private Button btnDefaultSize;
	private Button btnSmall;
	private int center;
	private Label lImages = new Label("Images", CENTER);

	public ButtonSample() {
		center = Settings.screenWidth / 2;
	}

	@Override
	public void initUI() {
		super.initUI();

		try {
			setInsets(0, 0, 0, UnitsConverter.toPixels(DP + 8));
			setBackForeColors(0xF7F7F7, 0x000000);
			setScrollBars(false, true);
			// Colors
			Label lColors = new Label("Colors", CENTER);
			Font bold = lColors.getFont().asBold();
			lColors.setFont(bold);
			btnDefaultColor = new Button("Default");
			btnRed = new Button("Red");
			btnRed.setBackForeColors(Color.getRGB("d34419"), Color.WHITE);
			btnGreen = new Button("Green");
			btnGreen.setBackForeColors(Color.getRGB("18d25a"), Color.WHITE);
			btnBlue = new Button("Blue");
			btnBlue.setBackForeColors(Color.getRGB("1878d1"), Color.WHITE);
			// Shapes
			Label lShapes = new Label("Shapes", CENTER);
			lShapes.setFont(bold);
			btnFull = new Button("Full Button");
			btnFull.setBackForeColors(0x3e72c1, Color.WHITE);
			btnRounded = new Button("Rounded Corners Button", Button.BORDER_ROUND);
			btnRounded.roundBorderFactor = 7;
			btnRounded.setBackForeColors(0x3e72c1, Color.WHITE);
			btnBorderless = new Button("Borderless Button", Button.BORDER_NONE);
			btnBorderless.setForeColor(0x3e72c1);
			btnOutlined = new Button("Outlined Button", Button.BORDER_OUTLINED);

			btnOutlined.setBackForeColors(0x3e72c1, Color.WHITE);
			// Images
			lImages.setFont(bold);
			Image img = new Image("images/bt_info.png").getHwScaledInstance(UnitsConverter.toPixels(DP + 18),
					UnitsConverter.toPixels(DP + 18));
			btnLeftImage = new Button("Left Image", img, RIGHT, UnitsConverter.toPixels(DP + 8));
			btnLeftImage.setBackForeColors(0x3e72c1, Color.WHITE);
			btnRightImage = new Button("Right Image", img, LEFT, UnitsConverter.toPixels(DP + 8));
			btnRightImage.setBackForeColors(0x3e72c1, Color.WHITE);
			btnImage = new Button(
					img.getHwScaledInstance(UnitsConverter.toPixels(DP + 24), UnitsConverter.toPixels(DP + 24)));
			btnImage.setBackForeColors(0x3e72c1, Color.WHITE);
			// Sizes
			Label lSizes = new Label("Sizes", CENTER);
			lSizes.setFont(bold);
			btnLarge = new Button("Large");
			btnLarge.setBackForeColors(0x3e72c1, Color.WHITE);
			btnLarge.setFont(Font.getFont(btnLarge.getFont().size * 3 / 2));
			btnDefaultSize = new Button("Default");
			btnDefaultSize.setBackForeColors(0x3e72c1, Color.WHITE);
			btnSmall = new Button("Small");
			btnSmall.setFont(Font.getFont(btnLarge.getFont().size * 3 / 4));
			btnSmall.setBackForeColors(0x3e72c1, Color.WHITE);

			add(lColors, LEFT, TOP + UnitsConverter.toPixels(DP + 8), FILL, DP + 36);
			add(btnDefaultColor, CENTER, AFTER + UnitsConverter.toPixels(DP + 8));
			add(btnGreen, CENTER, AFTER + UnitsConverter.toPixels(DP + 8));
			add(btnRed, BEFORE - UnitsConverter.toPixels(DP + 8), SAME);
			add(btnBlue, AFTER + UnitsConverter.toPixels(DP + 8), SAME, btnGreen);
			add(lShapes, LEFT, AFTER + UnitsConverter.toPixels(DP + 8), FILL, DP + 36);
			add(btnFull, CENTER, AFTER + UnitsConverter.toPixels(DP + 8), PARENTSIZE + 95, PREFERRED);
			add(btnRounded, CENTER, AFTER + UnitsConverter.toPixels(DP + 8), PARENTSIZE + 95, PREFERRED);
			add(btnOutlined, CENTER, AFTER + UnitsConverter.toPixels(DP + 8));
			add(btnBorderless, CENTER, AFTER + UnitsConverter.toPixels(DP + 8));
			add(lImages, LEFT, AFTER + UnitsConverter.toPixels(DP + 8), FILL, DP + 36);
			add(btnRightImage, center + UnitsConverter.toPixels(DP + 4), AFTER + UnitsConverter.toPixels(DP + 8));
			add(btnLeftImage, BEFORE - UnitsConverter.toPixels(DP + 4), SAME);
			add(btnImage, CENTER, AFTER + UnitsConverter.toPixels(DP + 8));
			add(lSizes, LEFT, AFTER + UnitsConverter.toPixels(DP + 8), FILL, DP + 36);
			add(btnLarge, LEFT + UnitsConverter.toPixels(DP + 8), AFTER + UnitsConverter.toPixels(DP + 8),
					btnLarge.getPreferredWidth() <= 48 ? DP + 96
							: btnLarge.getPreferredWidth() + UnitsConverter.toPixels(DP + 48),
					DP + 54);
			add(btnDefaultSize, AFTER + UnitsConverter.toPixels(DP + 8), CENTER_OF);
			add(btnSmall, AFTER + UnitsConverter.toPixels(DP + 8), CENTER_OF, btnSmall.getPreferredWidth() <= 24
					? DP + 48 : btnSmall.getPreferredWidth() + UnitsConverter.toPixels(DP + 24), DP + 27,
					btnDefaultSize);
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	@Override
	public void reposition() {
		center = Settings.screenWidth / 2;
		btnRightImage
				.setRect(center + UnitsConverter.toPixels(DP + 4), AFTER + UnitsConverter.toPixels(DP + 8),
						btnRightImage.getPreferredWidth() <= 32 ? DP + 64
								: btnRightImage.getPreferredWidth() + UnitsConverter.toPixels(DP + 32),
						DP + 36, lImages);
		btnLeftImage
				.setRect(BEFORE - UnitsConverter.toPixels(DP + 4), SAME,
						btnLeftImage.getPreferredWidth() <= 32 ? DP + 64
								: btnLeftImage.getPreferredWidth() + UnitsConverter.toPixels(DP + 32),
						DP + 36, btnRightImage);
	}
}
```
{% endcode %}

{% hint style="warning" %}
Do not forget **to create a folder** called "_**images**_" inside _**/src/main/resources**_ and **save the** [**bt\_info.png**](https://github.com/TotalCross/TCSample/blob/master/src/main/resources/images/bt_info.png) **image inside it** \[images\].
{% endhint %}

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

#### **Atributos**

* `Button.CENTRALIZE` **-** Centralizar imagem e texto no botão.

### **References**

* See also our [quick tutorial video](https://www.youtube.com/watch?v=xjqd3g1IYco) on creating buttons.
* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/Button.html) for more information.

