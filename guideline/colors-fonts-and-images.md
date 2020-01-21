# Best practices to improve project maintenance

## Overview

There are a few recommended practices to improve the organization, maintenance, and performance, and consequently loading your application. Some of them are very basic, like creating a class apart to store the colors used in the application and other more complex as working with loading images that are pulled from an external bank. In this chapter we will learn about these recommendations. 

You can download the [Material Templates project](https://github.com/TotalCross/MaterialTemplates), which contains all the recommendations below.

![](../.gitbook/assets/imagem.png)

## Colors

In the development of any application it is essential to have a design to prototype the user interfaces. It turns out that when the developer takes these prototypes and starts to develop, it often ends up adding these colors in the UI classes themselves, which makes it difficult to maintain this code. 

{% hint style="info" %}
you will find free website recommendations for screen prototyping in the part of [references](https://totalcross.gitbook.io/playbook/guideline/colors-fonts-and-images#references) in the last topic of this chapter. 
{% endhint %}

Now let's say you have an update to your application and the background color of the APP has changed. If your project has 2 or 3 screens, is it relatively quick to change these colors but if it is a more robust design of 15 screens? The developer would have to quit by changing the background color 15 times. 

Thinking about this, TotalCross recommends that you create a class named Colors and create constants for each color that you will need to use in the application, and preferably with suggestive names such as BACKGROUND. The name of the constants must always be in upper case. Here is the standard suggested by TotalCross, feel free to adapt to the needs of your project.

{% code title="Colors.class" %}
```java
import totalcross.ui.gfx.Color;

public class Colors {
	// The entire color palette follows the default material selected by the
	// Material Color Tool:
	// https://material.io/tools/color/#!/?view.left=0&view.right=1

	// Primary Colors
	public static int PRIMARY = 0xD32F2F;
	public static int P_LIGHT = 0xFF6659;
	public static int P_DARK = 0x9A0007;

	// Secondary Colors
	public static int SECONDARY = 0xF44336;
	public static int S_LIGHT = 0xFF7961;
	public static int S_DARK = 0xBA000D;

	//Texts Colors
	public static int TEXT_ON_P = 0xFFFFFF;
	public static int TEXT_ON_P_LIGHT = 0x000000;
	public static int TEXT_ON_P_DARK = 0xFFFFFF;

	public static int TEXT_ON_S = 0x000000;
	public static int TEXT_ON_S_LIGHT = 0x000000;
	public static int TEXT_ON_S_DARK = 0xFFFFFF;

	
	// Backcolor samples colors
	public static int BACKGROUND_GRAY_01 = Color.getRGB(245, 245, 246);
	public static int BACKGROUND_GRAY_02 = Color.getRGB(225, 225, 226);
	public static int BACKGROUND_GRAY_03 = Color.getRGB(205, 205, 206);

	// Others
	public static int SOFT_PEACH = 0xE9E2E1;
	public static int GRAY = 0XC0C1E8;

}

```
{% endcode %}

The names we attributed to the contenders were not by chance but rather due to the Color [Material](https://blog.totalcross.com/en/material-o-layout-da-google/) standard. You can generate each of these colors and better understand this pattern through [Material Color Tools](https://material.io/tools/color/#!/). With this Material tool you select the primary and secondary color of your project and it already generates the application's color palette and font color.  

We also provide the source code for you to download and adapt for the project. Just click [here](https://github.com/TotalCross/MaterialTemplates). 

## Images

To facilitate code maintenance, it is also recommended that all images be instantiated in a separate class called Images and only be called in the interface classes. 

Images class example:

{% code title="Images.class" %}
```java
import totalcross.io.IOException;
import totalcross.ui.image.Image;
import totalcross.ui.image.ImageException;

public class Images {
	public static Image addperson, cart, ic_adaptive_launcher_shell_background_retang;

	private Images() {
	}

	public static void loadImages(int fmH) {
		try {
			addperson = new Image("images/addperson.png");
			cart = new Image("images/cart.png");
			ic_adaptive_launcher_shell_background_retang = new Image(
					"images/ic_adaptive_launcher_shell_background.png");
		} catch (ImageException | IOException e) {
			e.printStackTrace();
		}
	}
}
```
{% endcode %}

Using Images.class:

```java
	public void initUI() {
		Images.loadImages(fmH);
		ImageControl cart = new ImageControl(Images.cart);
		add(cart, LEFT, TOP, FILL, FILL);
	}
```

## Fonts

As with colors and images, it happens when we are going to edit the fonts and here the problem is even worse, because we still have to stick to the size of fonts, colors and type.

So we advised that before the developer can already take with Design all these details to pass through a class with everything custom, as in the example below: 

{% code title="Fonts" %}
```java
import totalcross.ui.font.Font;

public class Fonts {

	public static final int FONT_DEFAULT_SIZE = 12;

	public static Font latoMediumDefaultSize;
	public static Font latoMediumPlus1;
	public static Font latoMediumPlus2;
	public static Font latoMediumPlus4;
	public static Font latoMediumMinus1;
	public static Font latoMediumMinus2;
	public static Font latoMediumMinus4;

	public static Font latoBoldDefaultSize;
	public static Font latoBoldMinus1;
	public static Font latoBoldMinus2;
	public static Font latoBoldMinus4;
	public static Font latoBoldPlus1;
	public static Font latoBoldPlus2;
	public static Font latoBoldPlus4;
	public static Font latoBoldPlus6;
	public static Font latoBoldPlus8;

	public static Font latoLightDefaultSize;
	public static Font latoLightPlus1;
	public static Font latoLightPlus2;
	public static Font latoLightPlus4;
	public static Font latoLightPlus6;
	public static Font latoLightMinus1;
	public static Font latoLightMinus2;
	public static Font latoLightMinus4;

	public static Font latoRegularMinus5;
	public static Font latoRegularDefaultSize;

	static {

		// Lato Regular
		latoRegularDefaultSize = Font.getFont("Lato Regular", false, FONT_DEFAULT_SIZE);
		latoRegularMinus5 = latoRegularDefaultSize.adjustedBy(-5);

		// Lato Medium
		latoMediumDefaultSize = Font.getFont("Lato Medium", false, FONT_DEFAULT_SIZE);
		latoMediumPlus1 = latoMediumDefaultSize.adjustedBy(1);
		latoMediumPlus2 = latoMediumDefaultSize.adjustedBy(2);
		latoMediumPlus4 = latoMediumDefaultSize.adjustedBy(4);
		latoMediumMinus1 = latoMediumDefaultSize.adjustedBy(-1);
		latoMediumMinus2 = latoMediumDefaultSize.adjustedBy(-2);
		latoMediumMinus4 = latoMediumDefaultSize.adjustedBy(-4);
		// Lato Bold
		latoBoldDefaultSize = Font.getFont("Lato Bold", false, FONT_DEFAULT_SIZE);
		latoBoldPlus1 = latoMediumDefaultSize.adjustedBy(1);
		latoBoldPlus2 = latoMediumDefaultSize.adjustedBy(2);
		latoBoldPlus4 = latoMediumDefaultSize.adjustedBy(4);
		latoBoldPlus6 = latoMediumDefaultSize.adjustedBy(6);
		latoBoldPlus8 = latoMediumDefaultSize.adjustedBy(8);
		latoBoldMinus1 = latoMediumDefaultSize.adjustedBy(-1);
		latoBoldMinus2 = latoMediumDefaultSize.adjustedBy(-2);
		latoBoldMinus4 = latoMediumDefaultSize.adjustedBy(-4);
		// Lato Light
		latoLightDefaultSize = Font.getFont("Lato Light", false, FONT_DEFAULT_SIZE);
		latoLightPlus1 = latoLightDefaultSize.adjustedBy(1);
		latoLightPlus2 = latoLightDefaultSize.adjustedBy(2);
		latoLightPlus4 = latoLightDefaultSize.adjustedBy(4);
		latoLightPlus6 = latoLightDefaultSize.adjustedBy(6);
		latoLightMinus1 = latoLightDefaultSize.adjustedBy(-1);
		latoLightMinus2 = latoLightDefaultSize.adjustedBy(-2);
		latoLightMinus4 = latoLightDefaultSize.adjustedBy(-4);
	}
}
```
{% endcode %}

to apply this class:

```java
public void initUI() {
  Label lbl = new Label(txt);
  lbl.setFont(Fonts.latoMediumMinus2);
  lbl.setForeColor(Colors.WHITE);
  add(lbl, LEFT, BOTTOM);
}
```

{% hint style="success" %}
Another way would be to create an enum to stylize and only apply where you need it. To learn how to do it this way just click [here](https://totalcross.gitbook.io/playbook/guideline/suggested-design-patterns/builder). 
{% endhint %}

## Material Constants

The Material recommends a series of [size and spacing patterns](https://material.io/design/components/), so it is ideal to create a class within the useful package and assigning these patterns to the constants, as in the example below: 

{% code title="MaterialConstants" %}
```java
import totalcross.ui.Control;
import totalcross.util.UnitsConverter;

/**
 * Constants of positioning and components size to make it easier to maintain
 * the app.
 * 
 * @author brunoamuniz
 *
 */

public class MaterialConstants {

	public static final int BORDER_SPACING = UnitsConverter.toPixels(16 + Control.DP);

	public static final int COMPONENT_SPACING = UnitsConverter.toPixels(8 + Control.DP);

	public static final int FAB_SIZE = UnitsConverter.toPixels(56 + Control.DP);

	public static final int MINI_FAB_SIZE = UnitsConverter.toPixels(40 + Control.DP);

	public static final int EDIT_HEIGHT_NO_CAPTION = UnitsConverter.toPixels(40 + Control.DP);

	public static final int EDIT_HEIGHT = UnitsConverter.toPixels(52 + Control.DP);

	public static final int TABS_HEIGHT = UnitsConverter.toPixels(40 + Control.DP);

}
```
{% endcode %}

to apply this class:

```java
Button btn = new Button("Button");
add(btn, LEFT + MaterialConstants.BORDER_SPACING, AFTER + MaterialConstants.COMPONENT_SPACING,
				FILL - MaterialConstants.BORDER_SPACING, PREFERRED);
```

## References

* Screen prototyping tool - [Invision app](https://www.invisionapp.com/), [figma](https://www.figma.com/), [marvel app](https://marvelapp.com/) and [adobeXD](https://www.adobe.com/br/creativecloud.html?ef_id=Cj0KCQjwtr_mBRDeARIsALfBZA571eitMauX00tdmLL6ARRBAGWNYxk-hO-eTsRNi61SH1Y6RlO1y4EaArMwEALw_wcB:G:s&gclid=Cj0KCQjwtr_mBRDeARIsALfBZA571eitMauX00tdmLL6ARRBAGWNYxk-hO-eTsRNi61SH1Y6RlO1y4EaArMwEALw_wcB&mv=search&s_kwcid=AL!3085!3!301784432823!b!!g!!adobe+creative&sdid=KQPOT);
* To better illustrate where each of them is used, you can download the [Nubank\_Sample project in GitHub](https://github.com/totalcross/Nubank_Sample);
* Screen templates in standard Material Design made with totalcross - [Material Templates](https://github.com/TotalCross/MaterialTemplates) ;
* [Material Standards](https://material.io/design/components/).



