# GPS

### Overview

**GPS** is a class that retrieves GPS coordinates read from Android, WP8, and iOS native API. This class only retrieves data updating the internal fields. If you want to display that data, you may use the **GPSView** class.

If the GPS fails connecting to the satellites, and the phone has signal, you can use the cell tower location as a rough location. The precision varies between 50m to 3km, depending on the phone location. In this case, you can get the latitude and longitude using **CellInfo.toCoordinates\(\)** on Android and Windows 32. This won’t work on other platforms. Don’t forget to turn on the GPS, going to somewhere similar to Settings / Security & Location / Enable GPS satellites. You won’t be able to use if if it’s off in the settings.

### GPS class

Here is an example of GPS usage:

{% code title="GPS\_SAMPLE" %}
```java
new Thread()

{
	public void run()
	{
		gps = new GPS();
		for (int i = 0; i < 60*2 && gps.location[0] == 0; i++) // wait 60s
		{
			Vm.safeSleep(500);
			try
			{
				gps.retrieveGPSData();
			}
			catch (Exception eee)
			{
				eee.printStackTrace();
				break;
			}
		}
	}
}.start();
```
{% endcode %}

### Atributes

| Type | Name | Description |
| :--- | :--- | :--- |
| int | satellites | Number of satellites  |
| double\[\]  | location | Stores the location - latitude on first index \(0\) and longitude on second index \(1\). |
| double | direction | Stores the direction in degrees from the North. |

### methods

| **Type** | Name | Description |
| :--- | :--- | :--- |
| boolean | retrieveGPSData\(\) | Call this method to retrieve the data from the GPS, true if the data was retrieved, false if low signal. |
| void |  stop\(\) | Closes the underlying PortConnector or native api. |
| double | getLatitude\(\) | Returns the latitude |
| double | getLongitude\(\) | Returns the longitude |

## **References**

For more details, check out [JavaDoc](https://rs.totalcross.com/doc/).



