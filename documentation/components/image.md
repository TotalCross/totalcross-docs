# Image

### Overview

An image is a rectangular image that you can draw or copy onto a surface.

Image objects can not be added directly to the user interface because they are not controllers \(that is, they do not extend the Control class\).

To display an image in the user interface, you need to use a control that best suits your needs, such as ImageControl, Button, or Animation. If you do not want to use any controls, you can draw the image on the screen using the Graphics object.

It is important to note that some transformation methods return a new instance of the image, while others apply to the current instance. To preserve an image with a single frame, use getFrameInstance \(0\);

To better understand TotalCross's recommended way to use images in your projects, go to [the Colors, Fonts and Images](https://totalcross.gitbook.io/playbook/guideline/colors-fonts-and-images) page in the Guideline To Create Apps section.

![](../../.gitbook/assets/image-sample.gif)

### Source Code

{% code title="ImagImageAnimationSample.java" %}
```java
import totalcross.game.Animation;
import totalcross.sys.Settings;
import totalcross.ui.Button;
import totalcross.ui.ComboBox;
import totalcross.ui.Container;
import totalcross.ui.Label;
import totalcross.ui.dialog.MessageBox;
import totalcross.ui.event.ControlEvent;
import totalcross.ui.event.Event;
import totalcross.ui.gfx.Color;
import totalcross.ui.image.Image;

public class ImageAnimationSample extends Container {
	final int gap = 5;
	private Button btnStartStop;
	private Animation anim;
	private ComboBox cbEffect;
	private int effect;

	@Override
	public void initUI() {
		super.initUI();
		add(btnStartStop = new Button(" Start/Stop "), CENTER, TOP + Settings.screenHeight / 7, SCREENSIZE + 50,
				SCREENSIZE + 10);
		btnStartStop.setBackForeColors(0x4583d4, 0xFFFFFF);

		add(new Label("Effect: ", LEFT, Color.BLACK, false), LEFT + Settings.screenWidth / 5,
				BOTTOM - Settings.screenHeight / 4);

		String[] items = { "normal", "scaledBy", "smoothScaledBy", "getRotatedScaledInstance", "getTouchedUpInstance",
				"changeColors", "fadedInstance", "applyColor2/dither" };
		ComboBox.usePopupMenu = false;
		add(cbEffect = new ComboBox(items), AFTER, BOTTOM - Settings.screenHeight / 4,
				FILL - Settings.screenHeight / 10, PREFERRED);
		cbEffect.setSelectedIndex(0);
		cbEffect.setBackForeColors(0x3861af, 0xFFFFFF);
		cbEffect.fillColor = 0x4583d4;
		next(false);
	}

	@Override
	public void onAddAgain() {
		next(false);
	}

	@Override
	public void onEvent(Event event) {
		switch (event.type) {
		case ControlEvent.PRESSED: {
			if (event.target == cbEffect && effect != cbEffect.getSelectedIndex()) {
				next(true);
			} else if (event.target == btnStartStop) {
				if (anim.isPaused) {
					anim.resume();
				} else {
					anim.pause();
				}
			}
			break;
		}
		}
	}

	/**
	 * shows next frame
	 */
	private void next(boolean changeEffect) {
		try {
			onRemove();
			Image img = new Image("images/alligator.gif");
			effect = cbEffect.getSelectedIndex();
			double scale = Settings.isIOS() ? 1.5 : 2; // ios has less opengl
														// memory
			int scaledcount = Settings.screenWidth / 500;
			System.out.println(scaledcount + " ," + Settings.screenWidth);
			for (int i = 0; i < scaledcount; i++) {
				img = img.scaledBy(scale, scale);
			}
			switch (effect) {
			case 1:
				img = img.scaledBy(scale, scale);
				break;
			case 2:
				img = img.smoothScaledBy(scale, scale);
				break;
			case 3:
				img = img.getRotatedScaledInstance(50, 90, -1);
				break;
			case 4:
				img = img.getTouchedUpInstance((byte) 50, (byte) 100);
				break;
			case 5:
				img.changeColors(0xFF31CE31, 0xFFFF00FF);
				break;
			case 6:
				img = img.getFadedInstance();
				break;
			case 7:
				img.applyColor2(Color.RED);
				img.getGraphics().dither(0, 0, img.getWidth(), img.getHeight());
				break;
			}
			if (Settings.isOpenGL) {
				img.applyChanges();
			}
			anim = new Animation(img, 120);
			anim.pauseIfNotVisible = true;
			add(anim, CENTER, CENTER, PREFERRED, PREFERRED);
			anim.start(Animation.LOOPS_UNLIMITED);
		} catch (Throwable e) {
			MessageBox.showException(e, true);
		}
	}

	@Override
	public void onRemove() {
		if (anim != null) {
			anim.stop();
			remove(anim);
			anim = null;
		}
	}
}
```
{% endcode %}

{% hint style="warning" %}
Do not forget **to create a folder** called "_**images**_" inside _**/src/main/resources**_ and **save the** [**alligator.gif**](https://github.com/TotalCross/TCSample/blob/master/src/main/resources/images/alligator.gif) **image inside it** \[images\].
{% endhint %}

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | Image\(int width, int height\) | Creates an Image object with the given width and height. The new image has the same color depth and color map of the default drawing surface. |
| **Constructor** | Image\(byte\[\] fullDescription\) | Creates an Image object from the given byte array, which must specify the whole image, including its headers. Use only JPEG or PNG images on the devices \(GIF and BMP are supported on the desktop only\). |
| **Constructor** | Image\(String path\) | Attempts to read the contents of the file specified by the given path, creating an Image object from the bytes read. The path given is the path to the image file. The file must be in 2, 16, 256, 24 bpp color compressed \(RLE\) or uncompressed BMP bitmap format, a PNG file, a GIF file, or a JPEG file. If the image cannot be loaded, an ImageException will be thrown. |
| **Constructor** | Image\(Stream s\) | Attempts to read the contents of the given stream, and create an Image object from the bytes read. Loads a BMP, JPEG, GIF, or PNG image from a stream. Note that GIF and BMP are supported only on the desktop. Note that all the bytes of the given stream will be fetched, even those bytes that may follow the image. |
| **Boolean** | isSupported\(String filename\) | Check if a specific file is supported by the platform at runtime; PNG or JPEG are always supported. GIF and BMP are supported on JavaSE only. |
| **int** | getWidth\( \) | Returns the image width |
| **int** | getHeight\( \) | Returns the image height |
| **Graphics** | getGraphics\( \) | Returns the Graphics object used by this image |
| **void** | changeColors\(int from, int to\) | change all pixels of the same color by another color |
| **void** | applyColor\(int color\) | Applies the given color RGB values to all pixels of this image, preserving the transparent color and alpha channel, if set. |
| **Image** | scaledBy\(double scaleX, double scaleY\) | Returns a scaled instance of this image. The new dimensions are calculated based on this image’s dimensions and the given proportions. The algorithm used is the replicate scale: not good quality, but fast. The given values must be &gt; 0 |
| **Image** | smoothScaledBy\(double scaleX, double scaleY, int backColor\) | Returns a scaled instance of this image. The new dimensions are calculated based on this image’s dimensions and the given proportions. The given values must be &gt; 0. The transparent pixels are replaced by backColor, which produces a smooth border. |
| **Image** | getRotatedScaledInstance\(int scale, int angle, int fillColor\) | Returns a rotated and/or scaled version of this image, where the scale parameter indicates the percentage of scaling to be performe, the angle indicates the rotation angle, expressed in trigonometric degrees and FillColor is the fill color. Do not use this method for scaling only, because the scaling methods are faster. If you need a smooth scale and rotate, scale it first with smoothScaledBy\(\) or getSmoothScaledInstance\(\) and rotate it without scaling \(or vice-versa\). |
| **Image** | getTouchedUpInstance\(byte brightness, byte contrast\) | Retorna uma instância retocada da imagem, onde o parâmetro brightness indica o brilho\(que deve ser entre -128 e 127\) e o constrast indica o nível de contraste, que também deve ser entre -128\(onde não há contraste\) e 127\(o nível máximo de contraste\) |
| **Image** | getFadedInstance\(int backColor\) | Returns a touched-up instance of this image with the specified brightness and contrast. |

### References

* See also our [quick tutorial video](https://www.youtube.com/watch?v=1cZBjr7sg3s) on creating Image Animation sample.
* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/Button.html) for more information.

