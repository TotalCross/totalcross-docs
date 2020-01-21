# Progress Bar

### Overview

It is a bar that can demonstrate the progress of a particular request or a loading of an event. You can have text that indicates the current status of the ProgressBar and can be used both horizontally and vertically.

### Source code

{% code title="ProgressBarSample" %}
```java
import totalcross.sys.Convert;
import totalcross.sys.Settings;
import totalcross.sys.Vm;
import totalcross.ui.Container;
import totalcross.ui.Control;
import totalcross.ui.MainWindow;
import totalcross.ui.ProgressBar;
import totalcross.ui.dialog.MessageBox;
import totalcross.ui.gfx.Color;
import totalcross.util.UnitsConverter;

public class ProgressBarSample extends MainWindow {
    ProgressBar  pbHYellow, pbVRed, pbVCyan, pbHRed, pbHPurple;
    int gap = UnitsConverter.toPixels(DP + 8);

    public ProgressBarSample() {
        setUIStyle(Settings.MATERIAL_UI);
    }

    @Override
    public void initUI() {
        try {
            super.initUI();

            Container sc = new Container();
            sc.setInsets(gap, gap, gap, gap);
            add(sc, LEFT, TOP, FILL, FILL);

            pbHPurple = new ProgressBar();
            pbHPurple.max = 50;
            pbHPurple.highlight = true;
            pbHPurple.suffix = " of " + pbHPurple.max;
            pbHPurple.textColor = 0xAAAA;
            pbHPurple.drawText = true;
            sc.add(pbHPurple, LEFT, TOP, FILL, PREFERRED);

            // endless ProgressBarSample
            pbHYellow = new ProgressBar();
            pbHYellow.max = width / 4; // max-min = width of the bar
            pbHYellow.setBackColor(Color.YELLOW);
            pbHYellow.setForeColor(Color.ORANGE);
            pbHYellow.prefix = "Loading, please wait...";
            pbHYellow.drawText = true;
            sc.add(pbHYellow, LEFT, AFTER + gap, FILL, PREFERRED);

            pbHRed = new ProgressBar();
            pbHRed.max = 50;
            pbHRed.setEndless();
            pbHRed.setBackForeColors(Color.DARK, Color.RED);
            sc.add(pbHRed, LEFT, AFTER + gap, FILL, FONTSIZE + 50);

            final int max = Settings.onJavaSE ? 2000 : 200;
            // vertical ones
            pbVCyan = new ProgressBar();
            pbVCyan.vertical = true;
            pbVCyan.max = max;
            pbVCyan.textColor = Color.BLUE;
            pbVCyan.setBackColor(Color.CYAN);
            pbVCyan.setForeColor(Color.GREEN);
            sc.add(pbVCyan, RIGHT, AFTER + gap, PREFERRED, FILL);

            pbVRed = new ProgressBar();
            pbVRed.vertical = true;
            pbVRed.max = 50;
            pbVRed.setBackForeColors(Color.RED, Color.DARK);
            sc.add(pbVRed, BEFORE - gap, SAME, FONTSIZE + 50, SAME);

            onSwapFinished();
        } catch (Exception ee) {
            MessageBox.showException(ee, true);
        }
    }

    @Override
    public void onSwapFinished() {
        final int ini = Vm.getTimeStamp();
        repaintNow();
        // runs the bench test
        int max = pbVCyan.max;
        for (int i = max; --i >= 0;) {
            int v = pbHPurple.getValue();
            v = (v + 1) % (pbHPurple.max + 1);
            Control.enableUpdateScreen = false; // since each setValue below updates the screen, we disable it to let it paint all at once at the end
            pbHPurple.setValue(v);
            pbVCyan.setValue(i);
            pbHYellow.setValue(5); // increment value
            pbHRed.setValue(v);
            Control.enableUpdateScreen = true;
            pbVRed.setValue(v);
            if (Settings.onJavaSE) {
                Vm.sleep(20);
            }
        }
    }
}
```
{% endcode %}

### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **int** | max | Progress Bar maximum value. |
| **int** | value | Current value of progress Bar. |
| **String** | prefix | It is the text that appears to the left of the value, remembering that the text output is prefix + value + sufix |
| **String** | suffix | It is the text that appears to the right of the value, remembering that the text output is prefix + value + suffix |
| **boolean** | drawText | It will indicate if the text will be displayed in progress bar or not, by default it comes as false. |
| **boolean** | drawValue | It will indicate if the value will be displayed in the progress bar. |

### Methods

<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Constructor</b>
      </td>
      <td style="text-align:left">ProgressBar()</td>
      <td style="text-align:left">Instances a ProgressBar with the minimum values 0 and maximum value 100.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Constructor</b>
      </td>
      <td style="text-align:left">ProgressBar(int min, int max)</td>
      <td style="text-align:left">Instances a ProgressBar with the values passed in the variables min and
        max.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Void</b>
      </td>
      <td style="text-align:left">setEndless()</td>
      <td style="text-align:left">Use in a horizontal ProgressBar to leave it without end.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Void</b>
      </td>
      <td style="text-align:left">setValue(int n)
        <br />
      </td>
      <td style="text-align:left">Updates the current progressbar value and draws the ProgressBar with the
        updated state.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Void</b>
      </td>
      <td style="text-align:left">setValue(int value, String prefix, String suffix)</td>
      <td style="text-align:left">
        <p>Updates the current value of progressBar and draws it again with the updated
          state and with texts before the value and after the value.</p>
        <p></p>
      </td>
    </tr>
  </tbody>
</table>## References

* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/ProgressBar.html) for more information.
* You can check the example contained in the SDK, in tc.samples.api.ui ProgressBarSample.

