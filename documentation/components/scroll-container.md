# Scroll Container

## Overview

The Container scroll is a container that has side scroll, horizontal scroll or no scroll.

### How to use

```java
public class ScrollContainerSample extends MainWindow {

    public ScrollContainerSample(){
        setUIStyle(Settings.Material);
    }

    @Override
        public void initUI() {
            super.initUI();
            ScrollContainer sc = new ScrollContainer(false, true);
            int gap = UnitsConverter.toPixels(DP + 16);
            sc.setInsets(gap, gap, gap, gap);
            add(sc, LEFT, TOP, FILL, FILL);

            Button b;
            ScrollContainer sc1, sc2, sc3;
            // a ScrollContainer with both ScrollBars
            sc.add(new Label("Vertical and horizontal:"), LEFT, TOP);
            sc.add(sc1 = new ScrollContainer());
            sc1.setBorderStyle(BORDER_ROUNDED);
            sc1.setInsets(3, 3, 3, 3);
            sc1.setRect(LEFT, AFTER, FILL, SCREENSIZE + 30);
            int xx = new Label("Name99").getPreferredWidth() + 2; // edit's alignment
            for (int i = 0; i < 50; i++) {
                sc1.add(new Label("Name" + i), LEFT, AFTER + 10);
                sc1.add(new Edit(), xx, SAME, SCREENSIZE + 90, PREFERRED);
                if (i % 3 == 0) {
                    sc1.add(new Button("Go"), AFTER + 2, SAME, PREFERRED, SAME);
                }
            }

            // a ScrollContainer with vertical ScrollBar disabled
            sc.add(new Label("Horizontal-only:"), LEFT, AFTER + gap);
            sc.add(sc2 = new ScrollContainer(true, false));
            sc2.setBorderStyle(BORDER_ROUNDED);
            sc2.setInsets(3, 3, 3, 3);
            int lines = Settings.screenHeight > 320 ? 4 : 3;
            sc2.setRect(LEFT, AFTER, FILL, lines * (fmH + Edit.prefH) + fmH / 2);
            for (int i = 0; i < lines; i++) {
                sc2.add(new Label("Name" + i), LEFT, AFTER);
                sc2.add(new Edit(""), xx, SAME, PARENTSIZE + 200, PREFERRED); // fit
                sc2.add(new Button("Go"), AFTER, SAME, PREFERRED, SAME);
            }

            // a ScrollContainer with horizontal ScrollBar disabled
            sc.add(new Label("Vertical-only:"), LEFT, AFTER + gap);
            sc.add(sc3 = new ScrollContainer(false, true));
            sc3.setBorderStyle(BORDER_ROUNDED);
            sc3.setInsets(3, 3, 3, 3);
            sc3.setRect(LEFT, AFTER, FILL, SCREENSIZE + 30);
            for (int i = 0; i < 50; i++) {
                sc3.add(new Label("Name" + i), LEFT, AFTER);
                sc3.add(b = new Button("Go"), RIGHT, SAME, PREFERRED, SAME);
                sc3.add(new Edit(""), xx, SAME, FIT - 2, PREFERRED, b); // fit
            }
        }
}
```

## References

* To know more details read its [JavaDocs](https://rs.totalcross.com/doc/totalcross/ui/ScrollContainer.html).

[  
](https://app.gitbook.com/@totalcross/s/playbook/~/drafts/-LfzE7W6V32fHcj-QL-S/primary/apis/visao-geral-da-api)

