# Sliding Window

### **Overview**

Sliding Window is a fullscreen window that slides in and out of the screen during pop and unpop events. Use it to create transition effects between screens.

![](https://totalcross.com/documentation/img/samples/slidingwindow-sample.gif)

### Source Code

{% code title="SlidingWindowSample.java" %}
```java
@Override
public void controlPressed(ControlEvent e) {
    SlidingWindow sw = new SlidingWindow(new Presenter() {
        @Override
        public Container getView() {
            return new Container() {
                public void initUI() {
                    ImageControl i;
                    try {
                        i = new ImageControl(new Image("images/logoV.png"));
                        i.scaleToFit = true;
                        i.centerImage = true;
                        add(i, CENTER, CENTER, 100 + DP, 100 + DP);
                    } catch (IOException e) {
                        e.printStackTrace();
                    } catch (ImageException e) {
                        e.printStackTrace();
                    }
                };
            };
        }
    });
    sw.popup();
}
});
add(btn, CENTER, BOTTOM);
} catch (IOException | ImageException e) {
    e.printStackTrace();
}
```
{% endcode %}

{% hint style="info" %}
Because it is a more complex example, we only show the specific Sliding Window example code, if you want to see the whole code of the image interface construction [click here](https://github.com/TotalCross/TCSample/blob/master/src/main/java/totalcross/sample/components/Home.java).
{% endhint %}

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | SlidingWindow\(Presenter&lt;Container&gt; provider\) | Creates a SlidingWindow with the specified provider. Use the provider class to implement your view code. |
| **Constructor** | SlidingWindow\(Presenter&lt;Container&gt; provider, boolean delayInitUI\) | Creates a SlidingWindow with the specified provider and if it should delay the InitUI execution. Use the delayed InitUI if your screen takes a significant amount of time to load \(e.g., it fetches data from a server\) and the non-delayed InitUI if it is fast enough to be loaded prior to the animation. If the delayed option is used, the screen will popup with a spinner. |
| **void** | unpop\( \) | Unpops the SlidingWindow, hiding it. |
| **void** | popup\( \) | Popups the SlidingWindow, showing it. |

