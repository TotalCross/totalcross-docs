# Running C++ applications with TotalCross

## Introduction

We hope you learn how to use TotalCross Runtime and Process implementations. See more about:

* Java 7 [Runtime class](https://docs.oracle.com/javase/7/docs/api/java/lang/Runtime.html)
* Java 8 [Process class](https://docs.oracle.com/javase/8/docs/api/java/lang/Process.html)

{% hint style="warning" %}
These implementations work only for Linux platforms
{% endhint %}

## Requirements

Can compile C ++ applications and finish Get Started:

{% page-ref page="running-c++-applications-with-totalcross.md" %}

## Guide

Use external codes with Totalcross:

**Step 1:** create a blank project based in `HelloWorld` of VS Code plugin \(we named it `RunningCpp`\)

**Step 2:**  create an I/O sample in C++, in our case we did:

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string input;
    std::getline(std::cin, input);
    std::cout << "\nI received: " + input + "\n";
    return 0;
}
```

{% hint style="info" %}
It's a simple application to get an I/O input and shortly thereafter return it as output.
{% endhint %}

**Step 3:** compile \(something like this\):

![](../../.gitbook/assets/image%20%2829%29.png)

**Step 4:** inside `initUI` method at `RunningCpp` class, create a label to show the results:

```java
// Label to show the results
Label label;
label = new Label();
label.setBackForeColors(Color.WHITE,  Color.BLACK);
```

**Step 5:** create a child process:

```java
// Process initialization
Process process = null;
```

**Step 6:** output to the target program:

```java
// Output to program
byte[] output = "Take the output!!!\n".getBytes();              // convert string to
                                                                // byte array 
try {
    process = Runtime.getRuntime().exec("./io");                // execute your
                                                                // application (sh like)
    process.getOutputStream().write(output, 0, output.length);  // write output into 
                                                                // output strem
    process.waitFor();                                          // blocking method 
                                                                // (wait io finish)
} catch (IOException ioe) {
    ioe.printStackTrace();
} catch (InterruptedException ie) {
    ie.printStackTrace();
};
```

**Step 7:** read the C++ program output as input to TotalCross application

```java
// Input from program
String input;
try {
    // Read line by line the buffered stream
    LineReader lineReader = new LineReader(Stream.asStream(process.getInputStream()));
    while ((input = lineReader.readLine()) != null) {
        label.setText(input);
    }
} catch (IOException ioe) {
    ioe.printStackTrace();
};

// Add label to window
add(label, CENTER, CENTER);
```

**Step 8:** run `TotalCross: Package` with VS Code plugin or run `mvn package` in your terminal.

**Step 9:** copy C++ binary to target folder \(something like\):

![](../../.gitbook/assets/image%20%2839%29.png)

**Step 10:** run your program!!!

## See more

See our article about how to run RS232 protocol. See the full code:

```java
package com.totalcross;

import java.io.IOException; 
import java.lang.Process;

import totalcross.ui.Label; 
import totalcross.ui.MainWindow; 
import totalcross.ui.gfx.Color; 

import totalcross.io.LineReader; 
import totalcross.io.Stream; 

import totalcross.sys.Settings;

public class RunningCPP extends MainWindow {
    public RunningCPP() {
        setUIStyle(Settings.MATERIAL_UI);
    }
    
    @Override
    public void initUI() {
        // Label to show the results
        Label label;
        label = new Label();
        label.setBackForeColors(Color.WHITE,  Color.BLACK);
    
        // Process initialization
        Process process = null;
    
        // Output to program
        byte[] output = "Take the output!!!\n".getBytes();              // convert string to
                                                                        // byte array 
        try {
            process = Runtime.getRuntime().exec("./io");                // execute your
                                                                        // application (sh like)
            process.getOutputStream().write(output, 0, output.length);  // write output into 
                                                                        // output strem
            process.waitFor();                                          // blocking method 
                                                                        // (wait io finish)
        } catch (IOException ioe) {
            ioe.printStackTrace();
        } catch (InterruptedException ie) {
            ie.printStackTrace();
        };
    
        // Input from program
        String input;
        try {
            LineReader lineReader = new LineReader(Stream.asStream(process.getInputStream()));
            while ((input = lineReader.readLine()) != null) {
                label.setText(input);
            }
        } catch (IOException ioe) {
            ioe.printStackTrace();
        };
    
        // Add label to window
        add(label, CENTER, CENTER);
    }
}
```

## References

* Java 7 [Runtime class](https://docs.oracle.com/javase/7/docs/api/java/lang/Runtime.html)
* Java 8 [Process class](https://docs.oracle.com/javase/8/docs/api/java/lang/Process.html)

