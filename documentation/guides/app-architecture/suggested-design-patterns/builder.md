# Template Pattern

### What's Template Pattern

In this pattern, we will use an enum that will be responsible for providing a stylization for your controls, thus making your code less coupled and more practical to be developed

For example, in your application has a color pattern, font size and a particular font, you can create an enum that will represent this stylization for you and in case you need to change something in those controls you just need to change that enum. 

### How to apply this method

For example if in your application you have a need to create custom labels with a specific font and with different font sizes

#### Create a enum

You can create the enum in the root of the controller package

{% code title="Structures " %}
```text
└── src
    └── main
        └── java
            └── com.your_company_name.your_name_app
                .
                .
                .
                └── controller
                    └── Template.java
```
{% endcode %}

{% code title="Template.java" %}
```java
public enum Template {
        
/*

H1 to H4 will be used to stylize the controls with a font, bold style,
font size and forecolor and will be changed between those enum only your fontsize.
 
The parameters of the getFont () method are String font_name,
boolean boldStyle, int size in example h1 we have then:
        "Graviola Soft-Bold": font 
        false: boldStyle
        24: Font size
        0x363D86: forecolor
*/
    H1(Font.getFont("Graviola Soft-Bold", false, 24), 0x363D86),
    H2(Font.getFont("Graviola Soft-Bold", false, 20), 0x363D86),
    H3(Font.getFont("Graviola Soft-Bold", false, 18), 0x363D86),
    H4(Font.getFont("OpenSans-Bold", false, 12), 0x363D86),

    private final Font font;
    private final Integer forecolor;
    
    Template(Font font, Integer forecolor) {
        this.font = font;
        this.forecolor = forecolor;
    }

    public <T extends Control> T apply(T c) {
        if (forecolor != null) {
            c.setForeColor(forecolor);
        }
        
        if (font != null) {
            if (c instanceof Icon) {
                c.setFont(Font.getFont(c.getFont().name, false, font.size));
            } else {
                c.setFont(font);
            }
        }
        
        return c;
    }


```
{% endcode %}

#### To use the template

In your controls now you can use your previously created template to maintain a standard styling.

```java
Label lblHeader= new Label("Header");
Template.H1.apply(lblHeader);
add(lblHeader, CENTER, TOP);
```

The enum template created above is just an example of how to use this pattern, you can customize it according to the needs of your application.

