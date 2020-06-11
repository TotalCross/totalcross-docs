# Tabbed Container

### Overview

Tabbed Container is a control that has tabs that can have text and / or images. It has an automatic scrool, that is, by clicking on a specific tab, the controler simulates the drag to the chosen tab.

### Source Code

```java
import totalcross.io.IOException;
import totalcross.sample.util.Colors;
import totalcross.sys.Settings;
import totalcross.ui.Container;
import totalcross.ui.Label;
import totalcross.ui.ScrollContainer;
import totalcross.ui.TabbedContainer;
import totalcross.ui.dialog.MessageBox;
import totalcross.ui.gfx.Color;
import totalcross.ui.image.Image;
import totalcross.ui.image.ImageException;

public class TabbedContainerSample extends ScrollContainer {
	private final int gap = (int)(Settings.screenDensity * 30);

	@Override
	public void initUI() {
		try {
			setBackForeColors(Colors.BACKGROUND, Colors.ON_BACKGROUND);

			CreateImageAndTextTabbedContainer();
			CreateTextOnlyTabbedContainer();
			CreateBulletsTabbedContainer();
		} catch (Exception ee) {
			MessageBox.showException(ee, true);
		}
	}

	private void CreateImageAndTextTabbedContainer() throws ImageException, IOException {
		String[] caps = { 
			"Social 1", 
			"Social 2", 
			"Social 3" 
		};
		Image[] icons = { 
			new Image("images/fb_icon_40.png"), 
			new Image("images/gmail_icon_40.png"),
			new Image("images/insta_icon_40.png") 
		};

		Label sampleTitle = new Label("This is a icon and text Tabbed Container", CENTER);
		sampleTitle.autoSplit = true;
		add(sampleTitle, LEFT + gap, TOP + gap, FILL - gap, PREFERRED);
		
		Container spacing = new Container();
		add(spacing, LEFT + gap*2, AFTER + gap/2, FILL - gap*2, (int) (Settings.screenHeight * 0.3));
		
		final TabbedContainer tc = new TabbedContainer(caps);
		tc.setBackColor(Color.DARK);
		tc.getContainer(0).setBackColor(Colors.P_300);
		tc.getContainer(1).setBackColor(Colors.P_400);
		tc.getContainer(2).setBackColor(Colors.P_500);
		tc.setIcons(icons);
		tc.pressedColor = Colors.P_800;
		tc.activeTabBackColor = Colors.P_800;
		tc.allSameWidth = true;
		tc.extraTabHeight = fmH * 2;
		spacing.add(tc, LEFT, TOP, FILL, PARENTSIZE);
		for(int i = 0; i < 3; i++)
			tc.getContainer(i).add(new Label("Container " + (i+1)), CENTER, CENTER);
	}

	private void CreateTextOnlyTabbedContainer() throws ImageException, IOException {
		String[] caps = new String[3];
		caps[0] = "Home";
		caps[1] = "Photos";
		caps[2] = "Profile";
		
		
		Label sampleTitle = new Label("This is a text only Tabbed Container", CENTER);
		sampleTitle.autoSplit = true;
		add(sampleTitle, LEFT + gap, AFTER + gap*2, FILL - gap, PREFERRED);
		
		Container spacing = new Container();
		add(spacing, LEFT + gap*2, AFTER + gap/2, FILL - gap*2, (int) (Settings.screenHeight * 0.3));
		
		final TabbedContainer tc = new TabbedContainer(caps);
		tc.setType(TabbedContainer.TABS_BOTTOM);
		tc.setBackColor(Color.DARK);
		tc.getContainer(0).setBackColor(Colors.P_300);
		tc.getContainer(1).setBackColor(Colors.P_400);
		tc.getContainer(2).setBackColor(Colors.P_500);
		tc.useOnTabTheContainerColor = true;
		tc.allSameWidth = true;
		tc.extraTabHeight = fmH / 2;
		spacing.add(tc, LEFT, TOP, FILL, PARENTSIZE);
		for(int i = 0; i < 3; i++)
			tc.getContainer(i).add(new Label("Container " + (i+1)), CENTER, CENTER);
	}

	private void CreateBulletsTabbedContainer() throws ImageException, IOException {
		Image[] images = new Image[3];
		Image empty = new Image("images/bullet_empty.png").getSmoothScaledInstance(fmH, fmH);
		Image filled = new Image("images/bullet_full.png").getSmoothScaledInstance(fmH, fmH);
		filled.applyColor2(Color.ORANGE);

		for (int i = images.length; --i >= 0;) {
			images[i] = empty;
		}
		
		Label sampleTitle = new Label("This is a image-only Tabbed Container", CENTER);
		sampleTitle.autoSplit = true;
		add(sampleTitle, LEFT + gap, AFTER + gap*2, FILL - gap, PREFERRED);
		
		Container spacing = new Container();
		add(spacing, LEFT + gap*2, AFTER + gap/2, FILL - gap*2, (int) (Settings.screenHeight * 0.3));

		final TabbedContainer tc = new TabbedContainer(images);
		tc.setActiveIcon(filled);
		tc.setType(TabbedContainer.TABS_BOTTOM);
		tc.setBackColor(Color.DARK);
		tc.getContainer(0).setBackColor(Colors.P_300);
		tc.getContainer(1).setBackColor(Colors.P_400);
		tc.getContainer(2).setBackColor(Colors.P_500);
		tc.allSameWidth = true;
		tc.extraTabHeight = fmH / 2;
		tc.setBorderStyle(Container.BORDER_NONE);
		tc.transparentBackground = true;
		spacing.add(tc, LEFT, TOP, FILL, PARENTSIZE);
		for(int i = 0; i < 3; i++)
			tc.getContainer(i).add(new Label("Container " + (i+1)), CENTER, CENTER);
	}
}
```

### Methods

<table>
  <thead>
    <tr>
      <th style="text-align:left">Tipo</th>
      <th style="text-align:left">Nome</th>
      <th style="text-align:left">Descri&#xE7;&#xE3;o</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Construct</b>
      </td>
      <td style="text-align:left">TabbedContainer(String[] strCaptions)</td>
      <td style="text-align:left">Uses a string array as capations for the tabs.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Construct</b>
      </td>
      <td style="text-align:left">TabbedContainer(Image[] imgCaptions, int transparentColor)</td>
      <td style="text-align:left">Uses an image array to represent the flaps and set a color.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Construct</b>
      </td>
      <td style="text-align:left">TabbedContainer(Image[] imgCaptions)</td>
      <td style="text-align:left">Uses an image array to represent the flaps</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Container</b>
      </td>
      <td style="text-align:left">getContainer(int i)</td>
      <td style="text-align:left">Returns the Container for tab</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Void</b>
      </td>
      <td style="text-align:left">setType(byte type)</td>
      <td style="text-align:left">
        <p>Sets the position of the tabs.</p>
        <p>You can use TABS_TOP, TABS_BOTTOM, TABS_NONE</p>
      </td>
    </tr>
  </tbody>
</table>

### References

* See a example on [github](https://github.com/TotalCross/TCSample/blob/master/src/main/java/totalcross/sample/components/ui/TabbedContainerSample.java) .
* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/Grid.html) for more information.



