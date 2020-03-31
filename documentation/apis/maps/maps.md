# Maps - Deprecated

## Overview

You can use google maps to display a map in your app, and you can add some geometric shapes to your map

## Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **int** | SHOW\_SATELLITE\_PHOTOS | Used in the flags argument of showRoute: shows the satellite photos |
| **int** | USE\_WAZE | Used in the flags argument of showRoute: use waze to show the route of the current location to a target address. Note that the destination address is NOT used |

## Methods

| Return | Name | Description |
| :--- | :--- | :--- |
| **int** | toCoordI\(Double v\) |  |
| **boolean** | showAddress\(String address, boolean showSatellitePhotos\) | Shows the given address in a separate viewer |
| **boolean** | showRoute\(String addressI, String addressF, String traversedPoints, int flags\) | Shows the route between two points. |
| **boolean** | showMap\(MapItem\[\] items, boolean showSatellitePhotos\) | Shows an array of MapItem elements in the map. |
| **double\[\]** | getLocation\(String address\) | Returns the location after searching Google. |

## Nested Class

### MapItem

is an abstract class that will serve as inheritance for the classes below

#### Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **abstract void** | serialize\(StringBuffer sb\) | Creates a simple switch |

### Place

#### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **double** | lat | The location of the place |
| **double** | lon | The location of the place |
| **String** | caption |  An optional caption of the place, shown in bold |
| **String** | detail | The detail of the place. Use \n to split lines. Cannot be null |
| **int** | backColor | The item's background color. Alpha defaults to 255 if not specified |
| **int** | capColor | The item caption's color. Alpha defaults to 255 if not specified |
| **int** | detColor | The item details' color. Alpha defaults to 255 if not specified |
| **int** | pinColor | The item pin's color. Alpha defaults to 255 if not specified |
| **int** | fontPerc | The percentage of the font based on the device's original font size. Defaults to 100 |

#### Methods

| Return | Name | Description |
| :--- | :--- | :--- |
| **void** | serialize\(StringBuffer sb\) |  |

### Shape

#### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **double\[\]** | lats | The coordinates of the polygon |
| **double\[\]** | lons | The coordinates of the polygon |
| **boolean** | filled | Set if the item is filled or not |
| **int** | color | The item color. Alpha defaults to 255 if not specified |

#### Methods

| Return | Name | Description |
| :--- | :--- | :--- |
| **void** | serialize\(StringBuffer sb\) |  |

### Circle



#### Attributes

| Type | Name | Description |
| :--- | :--- | :--- |
| **double** | lat | Center of the circle |
| **double** | lon | Center of the circle |
| **double** | rad | The radius; if &gt; 0, its computed as meters; if &lt; 0, its computed as delta of the coordinates |
| **boolean** | filled | Set if the item is filled or not |
| **int** | color | The item color. Alpha defaults to 255 if not specified. |

#### Methods

| Return | Name | Description |
| :--- | :--- | :--- |
| **void** | serialize\(StringBuffer sb\) |  |



## **References**

* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/map/GoogleMaps.html) for more information.
* Within the **TotalCross SDK**, usually on Disk C, there is a folder called src/main/java/totalcross and there will be a folder named **Map**, containing a **simple sample** on map. Typically the path to this folder is this pattern:

```text
C:\Program Files\TotalCross\sdk\src\main\java\totalcross\map
```

