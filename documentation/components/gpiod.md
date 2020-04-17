---
description: This library serves to control the digital pins of the embedded GPIO.
---

# Gpiod

## Output

To activate and deactivate any external component the embedded board is to change the value of the GPIO pin that will activate it.

![](../../.gitbook/assets/image%20%2812%29.png)

![](../../.gitbook/assets/image%20%28109%29.png)

```java
package com.totalcross.DocRpi;
import totalcross.ui.MainWindow;
import totalcross.ui.event.ControlEvent;
import totalcross.ui.event.PressListener;
import totalcross.ui.gfx.Color;
import totalcross.ui.Button;
import totalcross.io.device.gpiod.GpiodChip;
import totalcross.io.device.gpiod.GpiodLine;
import totalcross.sys.Settings;

public class DocRpi extends MainWindow {
    // Integers to store state of each LED pin, 0 (LOW) and 1 (HIGH)
    private int    stt;
    // Buttons to control
    private Button btn;
    public DocRpi(){
        setUIStyle(Settings.MATERIAL_UI);
    }
    @Override
    public void initUI(){
        // Board Setup
        GpiodChip gpioChip = GpiodChip.open(0); // GIPIO bus
        GpiodLine pin = gpioChip.line(21);      //
        // Set LED pins as outputs and default value stt
        pin.requestOutput("CONSUMER",stt);
        // The TotalCross button:
        btn = new Button("Pin");                                    // Button instantiation
        // without text
        btn.setBackColor(Color.RED);                                // Set background color (red)
        btn.addPressListener(new PressListener(){                  // Press event listener
            @Override
            public void controlPressed(ControlEvent controlEvent) {
                stt = 1 - stt;                                      // Invert pin state 
                pin.setValue(stt);                                  // Set value (HIGH or LOW)
            }
        });
        add(btn, CENTER, CENTER);  
    }
}                               
```

## Input

In several embedded applications, it is necessary to receive digital signal from an external component such as sensors or even to activate another component indirectly.

![](../../.gitbook/assets/image%20%2869%29.png)

```java
package com.totalcross.DocRpi;
import totalcross.ui.MainWindow;
import totalcross.ui.event.ControlEvent;
import totalcross.ui.event.PressListener;
import totalcross.ui.gfx.Color;
import totalcross.ui.Button;
import totalcross.io.device.gpiod.GpiodChip;
import totalcross.io.device.gpiod.GpiodLine;
import totalcross.sys.Settings;
import totalcross.sys.Vm;

public class DocRpi extends MainWindow{
    // Integers to store state of each LED pin, 0 (LOW) and 1 (HIGH)
    private int stt;
    // Buttons to control 
    private Button btn;
    public DocRpi(){
        setUIStyle(Settings.MATERIAL_UI);   
    }
    @Override
    public void initUI(){
    
        // Board Setup
        GpiodChip gpioChip = GpiodChip.open(0); // GIPIO bus
        GpiodLine pin = gpioChip.line(21);      //
        // Set LED pins as outputs and default value stt
        pin.requestOutput("CONSUMER", stt);
        GpiodLine pinPushButton = gpioChip.line(22);
        // Set Reset pin as input
        pinPushButton.requestInput("CONSUMER");
        new Thread(){
            @Override
            public void run(){
                while(true){
                    if(pinPushButton.getValue() == 1){//check pin status
                        stt = 1 - stt;          // Invert pin state 
                        pin.setValue(stt);      // Set value (HIGH or LOW)
                    }
                    Vm.sleep(200);
                 } 
             }
         }.start();
    }
}

```



## Behind the Class

### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **Constructor** | open\(int chip\) | Defines which GPIO bus will be used. |
| **Construtor** | line\(int pin\) | Defines which pin of GPIO bus will be used. |
| **Void** | requestOutput\(String consumer, int defaultValue\) | Names the pin, defines as output and the initial value. |
| **Void** | setValue\(int value\) | Changes pin value. |
| **Void** | requestInput\(String consumer\) | Names the pin and defines as input. |
| **Int** | getValue\(\) | Returns pin status |



