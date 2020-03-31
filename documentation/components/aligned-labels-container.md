# Aligned Labels

### Overview

Aligned Label is a Container used to align all controls to the maximum width of a set of labels.

{% hint style="info" %}
In Totalcross this component is called **`AlignedLabelContainer`**.
{% endhint %}

![](../../.gitbook/assets/alignedlabels-sample.gif.pagespeed.ce.d4badoy8p.gif)

### Source Code

{% code title="AlignedLabelsSample.java" %}
```java
import totalcross.ui.AlignedLabelsContainer;
import totalcross.ui.Button;
import totalcross.ui.ComboBox;
import totalcross.ui.Edit;
import totalcross.ui.Label;
import totalcross.ui.ListBox;
import totalcross.ui.ScrollContainer;
import totalcross.util.UnitsConverter;

public class extends ScrollContainer {
	private int gap = UnitsConverter.toPixels(10 + DP);
	private boolean canInsert = true;
	private ListBox lb;
	private Label output;

	@Override
	public void initUI() {
		uiAdjustmentsBasedOnFontHeightIsSupported = false;
		setBackForeColors(0xF7F7F7, 0x000000);
		setScrollBars(false, true);

		String[] labels = { "Name", "Born date", "Telephone", "Address", "City", "Country" };
		Edit edits[] = new Edit[5];
		edits[0].transparentBackground = true;
		Edit.useNativeNumericPad = true;

		for (int i = 0; i < edits.length; i++) {
			switch (i) {
			case 1:
				edits[i] = new Edit("99/99/9999");
				edits[i].setMode(Edit.NORMAL, true);
				edits[i].setValidChars(Edit.numbersSet);
				edits[i].setKeyboard(Edit.KBD_NUMERIC);
				break;
			case 2:
				edits[i] = new Edit("(99)9999-99999");
				edits[i].setMode(Edit.NORMAL, true);
				edits[i].setValidChars(Edit.numbersSet);
				edits[i].setKeyboard(Edit.KBD_NUMERIC);
				break;
			default:
				edits[i] = new Edit();
			}
		}

		Label title = new Label("This is an AlignedLabelsContainer.\nAll the content will be automatically aligned.",
				CENTER, 0, true);
		title.autoSplit = true;
		add(title, LEFT + gap, TOP + gap, FILL - gap, PREFERRED);

		AlignedLabelsContainer alc = new AlignedLabelsContainer();
		alc.uiAdjustmentsBasedOnFontHeightIsSupported = false;
		alc.labelAlign = RIGHT;

		alc.setInsets(gap, gap, 0, 0);
		alc.setLabels(labels, edits[0].getPreferredHeight());
		add(alc, LEFT, AFTER, FILL, PREFERRED);
		int i;
		for (i = 0; i < edits.length - 1; i++) {
			alc.add(edits[i], LEFT + gap, alc.getLineY(i), FILL - gap, PREFERRED);
		}

		Button btnInsert = new Button("Insert data", (byte) 0);
		btnInsert.setBackForeColors(0x4583d4, 0xFFFFFF);
		alc.add(edits[edits.length - 1], LEFT + gap, alc.getLineY(i), edits[3].getWidth() / 2 - gap / 2, PREFERRED);
		alc.add(btnInsert, RIGHT - gap, CENTER_OF, SAME, PREFERRED, edits[edits.length - 1]);

		ComboBox cbCountry = new ComboBox(new String[] { "Brazil", "USA" });
		alc.add(cbCountry, LEFT + gap, alc.getLineY(++i), SAME, PREFERRED, edits[edits.length - 1]);

		Button btnClear = new Button("CLEAR DATA", (byte) 0);
		alc.add(btnClear, RIGHT - gap, CENTER_OF, SAME, PREFERRED);

		btnInsert.addPressListener(e -> {
			if (canInsert) {
				lb = new ListBox();
				for (int j = 0; j < edits.length; j++)
					lb.add(labels[j] + ": " + edits[j].getText());
				if (cbCountry.getSelectedIndex() != -1)
					lb.add("Country: " + cbCountry.getSelectedItem());
				else
					lb.add("Country: ");

				output = new Label("OUTPUT:");
				output.setFont(font.asBold());
				add(output, CENTER, AFTER);
				add(lb, CENTER, AFTER + gap, SCREENSIZE + 80, PREFERRED);
				canInsert = false;

				scrollToControl(lb);
			} else {
				lb.removeAll();
				for (int j = 0; j < edits.length; j++)
					lb.add(labels[j] + ": " + edits[j].getText());
				if (cbCountry.getSelectedIndex() != -1)
					lb.add("Country: " + cbCountry.getSelectedItem());
				else
					lb.add("Country: ");
			}
			// reposition(); reposition bugando o edit
		});

		btnClear.addPressListener(e -> {

			// Cleaning the labels' content
			for (Edit edit : edits)
				edit.clear();
			cbCountry.setSelectedIndex(-1);
			if (!canInsert) {
				// Cleaning the output
				remove(lb);
				remove(output);
				canInsert = true;
			}
		});
	}
}
```
{% endcode %}

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **Font** | childrenFont | Set this member to the font you want to set to the controls that are added to this container |
| **int\[ \]** | foreColors | Sets an array with the same number of labels and the colors you want to show for each label |
| **int** | labelAlign | The alignment of the labels |

### Methods

| ype | Name | Description |
| :--- | :--- | :--- |
| **Construtor** | AlignedLabelsContainer\( \) | Creates a new AlignedLabelsContainer without labels |
| **Construtor** | AlignedLabelsContainer\(String\[\] labels\) | Creates a new AlignedLabelsContainer with the given labels |
| **Construtor** | AlignedLabelsContainer\(String\[\] labels, int vgap\) | Creates a new AlignedLabelsContainer with the given labels and a vertical gap between the labels |
| **void** | add\(Control c\) | Since this is an AlignedLabelsContainer, use this to add a label |
| **int** | getLineY\(int line\) | Given a line \(staring from 0\), returns the y position |
| **void** | setLabels\(String\[ \] labels, int vgap\) | Sets the labels and the extra gap between rows \(which may be 0\) |

### 

