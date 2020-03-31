# Container

## Overview

The container is a control that contains child controls. It is possible to adjust its transparency, screen transition effects, borders and background style.

If you want to know more about how differences between windows and container, how to navigate between interfaces and what are the best ways to handle containers and windows, just click on the link below:

{% page-ref page="../../guides/app-architecture/container-x-window.md" %}

## Usage

{% code title="Container" %}
```java
class ContainerSample extends Container{
	
	@Override
    public void initUI() {
      try {
            ImageControl logo = new ImageControl(new Image("path_of_your_logo_img"));
            logo.scaleToFit = true;
            logo.centerImage = true;
            logo.transparentBackground = true;
            add(logo, CENTER, CENTER, PARENTSIZE + 50, PARENTSIZE + 50);
        } catch (ImageException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
{% endcode %}

## Features of Container

* \*\*\*\*[**How to navigate between screens**](https://app.gitbook.com/@totalcross/s/playbook/~/drafts/-LeSnZoHZefj9mq9OlAt/primary/faq#how-to-navigate-between-screens-containers-and-windows)\*\*\*\*
* **Container characteristics are assigned to child controls**

### Method

Some methods that are most commonly used

<table>
  <thead>
    <tr>
      <th style="text-align:left">name</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>add(Control control, int x, int y, int w, int h, Control relative);</p>
        <p></p>
        <p><a href="https://rs.totalcross.com/doc/totalcross/ui/Container.html#add-totalcross.ui.Control-">add</a>(
          <a
          href="https://rs.totalcross.com/doc/totalcross/ui/Control.html">Control</a>control)</p>
        <p>
          <br />add(Control control, int x, int y)
          <br />
          <br /><a href="https://rs.totalcross.com/doc/totalcross/ui/Container.html#add-totalcross.ui.Control-int-int-totalcross.ui.Control-">add</a>(
          <a
          href="https://rs.totalcross.com/doc/totalcross/ui/Control.html">Control</a>control, int x, int y, <a href="https://rs.totalcross.com/doc/totalcross/ui/Control.html">Control</a> relative)
            <br
            />
            <br />add(Control control, int x, int y, int w, int h)</p>
        <p></p>
      </td>
      <td style="text-align:left">Adds the control on the screen where the parameter x is the positioning
        of the control in the container in relation to the x axis, the parameter
        y is the positioning of the control in the container in relation to the
        y axis, parameter w is the length of the component, parameter h represents
        the height of the component and the relative parameter is to change the
        reference of the control to add on the screen (by default the relative
        is the last control added).</td>
    </tr>
    <tr>
      <td style="text-align:left">setBackForeColors(Color back, Color fore)</td>
      <td style="text-align:left">Assigns the color of the back parameter to the container background and
        the color of the fore parameter to the forecolor of the container. It is
        interesting to remember that the children of the container inherit the
        characters of the same.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>setBackColor(Color back);
          <br />
        </p>
        <p></p>
      </td>
      <td style="text-align:left">Assigns the color of the back parameter to the container background</td>
    </tr>
  </tbody>
</table>## Referencies

You can see more information in [javaDoc](https://rs.totalcross.com/doc/totalcross/ui/Container.html)

