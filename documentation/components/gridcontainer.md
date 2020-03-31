# GridContainer

### Overview

Is a class that uses grid layout, where each cell is a container.  
To use as cell you need to create a class that extends from GridContainer.Cell.

{% hint style="warning" %}
This component only works until version 4.3.8.
{% endhint %}

### Source Code

```java
add(gc = new GridContainer(GridContainer.HORIZONTAL_ORIENTATION),LEFT,TOP,FILL,FILL);
   gc.setBackColor(Color.WHITE);
   Flick f = gc.getFlick();
   f.shortestFlick = 1000;
   f.longestFlick = 6000;
   gc.setPageSize(linhas,colunas);
   gc.setRowsPerPage(linhasPorPagina);
   Celula []cels = new Celula[TOTAL_ITEMS];
   for (int i = 0; i < cels.length; i++)
      cels[i] = new Celula(i);
   gc.setCells(cels);
```

### Construtor

```java
GridContainer(int orientation){}
```

Constructs a GridContainer with the given orientation

### Methods

| Modifier and Type | Method | Description |
| :--- | :--- | :--- |
| Flick |  getFlick\(\) | Returns the flick attached to the ScrollContainer. |
| void |  initUI\(\) | Called to initialize the User Interface of this container. |
| void |  onColorsChanged\(boolean colorsChanged\) | Called after a setEnabled, setForeColor and setBackColor and when a control has been added to a Container. |
| void |  onEvent\(Event e\) | Called to process key, pen, control and other posted events. |
| void |  onFontChanged\(\) | Called after a setFont |
| void |  setCells\(GridContainer.Cell\[\] cells\) | Sets the cells of this GridContainer. |
| void |  setPageSize\(int cols, int rows\) | Sets the page size in columns and rows. |
| void |  setRowsPerPage\(int rpp\) | Sets the rows per page. |

### References

* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/GridContainer.html) for more information.

