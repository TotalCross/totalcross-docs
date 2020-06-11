# totalcross.sys

## Settings

This class provides some preferences from the device configuration and other VM settings. All settings are read-only, unless otherwise specified. Changing their values may cause the VM to crash. Look at its JavaDoc for more details.

## **VM**

Vm contains various system-level methods. This class contains methods to copy arrays, obtain a timestamp, sleep, and get platform and version information, among many other things. Look at its JavaDoc for more details.

## Time

The Time class stores a specific a date and time. 

* The **year** must have **4 digits** 
* The **hour** is **numbered in 24-hour notation**, which is the international standard notation of time, and may also be referred as military time or astronomical time.

For performance reasons, the Time fields have public access. So you can directly access the field day to get or set its value, instead of calling a method. However, that makes the Time objects unsafe because the fields’ values are not checked when they are set, and may not be within the field valid range.

Since the fields can be set without any kind of validation, it would be pointless to add validation to the other methods, therefore, the Time fields’ values are never validated by any method or constructor. So you must know and always respect the fields’ range, and never set a field with a variable without first checking if the value is withing range \(for instance, let the user type the hour in an edit and simply convert it to int and set the hour field, without checking if its value is between 0 and 23\).

The Time fields with their respective range:

* **year:** The year in 4 digits;
* **month:** The month in the range of 1 to 12;
* **day:** The day in the range of 1 to the last day of the specified month;
* **hour:** The hour in the range of 0 to 23;
* **minute:** The minute in the range of 0 to 59;
* **second:** The second in the range of 0 to 59;
* **millis:** Milliseconds in the range of 0 to 999;

{% hint style="info" %}
Time has a constant called **SECONDS\_PER\_DAY**, which obviously represents the **number of seconds** in a day, being equal to 24 \* 3600.
{% endhint %}

### Constructors 

Time has six constructors:

* **Time\(\)**: Default constructor, creates a Time object set with the device’s current date and time. Most devices do not keep track of the milliseconds, therefore, the field millis of the new object will always have the default value 0 on them.
* **Time\(int year, int month, int day, int hour, int minute, int second, int millis\):** Creates a Time object with the given values.
* **Time\(long t\):** Creates a Time object from the given value, which must be in the format YYYYMMDDHHMMSS.
* **Time\(int yyyymmdd, int hhmmssmmm\):** Constructs a Time object from the given date and time values.
* **Time\(String iso8601\):** Creates a Time object using the given string, which must be in the ISO8601 format: YYYYMMDDTHH:MM:SS.

{% hint style="warning" %}
Please notice the last three constructors do not include the milliseconds, so the field millis will keep its default value 0.
{% endhint %}

* **Time\(String time, boolean hasYear, boolean hasMonth, boolean hasDay, boolean hasHour, boolean hasMinute, boolean hasSeconds\):** Constructs a Time object, parsing the string and placing the fields depending on the flags that were set, using Settings.timeSeparator as spliter. The number of parts must match the number of true flags, or an `ArrayIndexOutOfBoundsException` will be thrown. AM/PM is supported.

{% hint style="warning" %}
**Remember**: no kind of validation is done on the Time fields values, not even on the constructors. However, the default constructor will never initialize an object with invalid values, and the last two constructors may throw an InvalidNumberException if it fails to parse the given string.
{% endhint %}

### Methods 

Finally, Time has the following methods:

* **`update()`**: Updates the internal fields with the current timestamp.
* **`quals(Object o)`:** Compares two Time objects for equality. The result is true if and only if the argument is not null and it’s a Time object that represents the same point in time, from year to millisecond, as this object.
* **`getTimeLong()`:** Converts this Time object to a long value in the format YYYYMMDDHHMMSS. Milliseconds is not included.YYYYMMDDHHMMSS. Milliseconds is not included.
* **`toIso8601()`**: Converts this Time object to a string in the ISO8601 format: YYYYMMDDTHH:MM:SS. Milliseconds is not included.
* **`toString()`**: Returns the time in format specified in totalcross.sys.Settings \(does NOT include the date neither the milliseconds\). To return the date, use the class totalcross.util.Date. So, to get a string with the date and time, use:
  * `Time t = new Time();` 
  * `String dateAndTime = new Date(t) + " " + t;`
* **`toString(String timeSeparator)`**: Similar to the above method except that it uses the specified separator.
* **`dump(StringBuffer sb, String timeSeparator, boolean includeMillis)`** : Dumps the time into the given StringBuffer, using the given separator and including the millileconds if asked by the user.
* **`isValid()`**: Returns true if the time is valid. Note that the date part is NOT checked; only hour, minute, second, and millis are checked against valid ranges.
* **`inc(int hours, int minutes, int seconds)`**: Increments or decrements the fields below. Note that this method does NOT update the day/month/year fields. The parameters can be positive \(to increment\), zero \(to keep it\), or negative \(to decrement\).

## CharacterConvert

This class is used to correctly handle international character conversions. The default character scheme converter is the 8859-1 \(ISO Latin 1\). 

If you want to use a different one, you must extend this class, implementing the `bytes2chars()` and `chars2bytes()` methods, and then assign the public member of `Convert.charConverter` to use your class instead of this default one. You can also use the method `Convert.setDefaultConverter()` to change it, passing, as parameter, the prefix of your CharacterConverter class \(better look at the implementation to know what to pass on\). 

For example, if you created a class named Iso88592CharacterConverter, call

```java
Convert.setDefaultConverter("Iso88592");
```

To find out which `sun.io.CharacterEncoder` you’re using on JDK to implement an equivalent version for TotalCross, use:

```java
System.out.println("" + sun.io.ByteToCharConverter.getDefault());
```

## UTF8CharacterConvert

This class extends the CharacterConvert class, and implements the UTF8 byte to UCS-2 character conversion. To use this class, you can call:

```java
Convert.setDefaultConverter("UTF8");
```

## Convert

Convert basically provides methods that allows object and basic type conversion. Furthermore, it also provides handy methods for common operations that should be used for a better performance.

This class is final and cannot be instantiated – its methods and fields are static.

To give you a better view of this class, its documentation was split into sub-sections:

### **Changing the default character converter**

The field charConverter keeps a reference to a character converter that will be used by default. You may change it by setting another character converter of your choice.

You may also use the method `setDefaultConverter(String name)`, which searches for a character converter by its name, and makes it the default by changing the charConverter field. Use like

```java
Convert.setDefaultConverter("UTF8");
```

to change all bytes\_to\_char and `char_to_bytes` operations to use UTF8 instead. Issuing

```java
Convert.setDefaultConverter("");
```

sets back the default encoder. The method returns true if the given encoder was found; false, otherwise. If not found, the encoder is reseted to the default one \(ISO 8859-1\).

### **Conversion between String and basic types**

| **Method** | Definition |
| :--- | :--- |
| toDouble\(String s\) |  Converts the given string to double. |
| toInt\(String s\)  | Converts the given string to int. The number may be prefixed with 0’s. |
| toShort\(String s\) | Convert a string to the short type. Note that this method is slower than \(short\)Convert.toInt\(\). However, it will throw an InvalidNumberException if the number is out of the short range. |
| toLong\(String s\)  | Converts the given string to long. |
| toLong\(String s, int radix\)  | Converts the given string to long in the given radix, which must be between 2 and 16. |
| toString\(boolean b\)   | Converts the given boolean to a string. |
| toString\(char c\)  | Converts the given char to a string. |
| toString\(double d\)  | Converts the given double to a string, formatted in scientific notation.  |
| toString\(double val, int decimalCount\) |  Converts the given double to a string, formatted with the given number of decimal places.  |
| toString\(int i\) Converts |  the given int to a string. |
| toString\(long l\)  | Converts the given long to a string using base 10. |
|  toString\(long i, int radix\)  | Converts the given long to a string in the given radix, which must be between 2 and 16.  |
| toString\(String doubleValue, int n\)  | Formats the given string as a double, rounding with n decimal places. |
|  unsigned2hex\(int b, int places\)  | Converts the given unsigned integer to hexadecimal using the given number of places \(up to 8\). |

### **Character, String and StringBuffer utilities**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Method</b>
      </th>
      <th style="text-align:left">Definition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p>appendPath(String path1, String path2)</p>
      </td>
      <td style="text-align:left">Concatenates two strings, ensuring there&#x2019;s a single slash between
        them. Removes extra slashes or backslashes if necessary.</td>
    </tr>
    <tr>
      <td style="text-align:left">digitOf(char ch, int radix)</td>
      <td style="text-align:left">Returns the value of the digit stored as char in the specified radix,
        which must be between 2 and 16. This method only handles the standard ASCII
        table.</td>
    </tr>
    <tr>
      <td style="text-align:left">dup(char c, int count)</td>
      <td style="text-align:left">Returns a string filled with the given char and size equals to count.</td>
    </tr>
    <tr>
      <td style="text-align:left">forDigit(int digit, int radix)</td>
      <td style="text-align:left">Returns the given digit in the specified radix, which must be between
        2 and 16.</td>
    </tr>
    <tr>
      <td style="text-align:left">getBreakPos(FontMetrics fm,StringBuffer sb,int start, int width,boolean
        doWordWrap)</td>
      <td style="text-align:left">Finds the best position to break the line with the given width, respecting
        word-wrap option and line endings</td>
    </tr>
    <tr>
      <td style="text-align:left">hashCode(StringBuffer sb)</td>
      <td style="text-align:left">Returns the hash code of the string stored by this StringBuffer.</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
The class StringBuffer does not have a method that returns its hash code, so you would have to first create a String from the StringBuffer to get its hash code, like this:   
  
****`int hashCode = sb.toString.hashCode();` 
{% endhint %}

| **Method** | Definition |
| :--- | :--- |
| Convert.hashCode\(\) |  calculates the StringBuffer’s hash code directly, without using an intermediary String object, resulting in better performance and memory usage. |
| insertAt\(StringBuffer sb, int pos, char c\)  | Inserts the given char at the specified position in the StringBuffer. |
| insertLineBreak\(int maxWidth, FontMetrics fm, String text\)  | Returns a new string which is a copy of the given text with line breaks, placed based on the maxWidth and fm arguments. Very useful method to help you keep your application’s interface cross-platform. It can be used to insert line breaks on strings passed to message boxes or list boxes. |
| insertLineBreak\(int maxWidth, FontMetrics fm, String text\) |  Returns a new string which is a copy of the given text with line breaks, placed based on the maxWidth and fm arguments. Very useful method to help you keep your application’s interface cross-platform. It can be used to insert line breaks on strings passed to message boxes or list boxes. |
| numberOf\(String s, char c\)  | Returns the number of occurrences of the specified char in the given string. |
| replace\(String source, String from, String to\)  | Searches the string source for occurrences of the string from, replacing them by the string to. |
| tokenizeString\(String input, char delim\)  | Tokenizes the given string using the given char as separator. The return is a string array with size equal to the number of tokens. |
| tokenizeString\(String input, String delim\)   | Same as the above, but uses a String instead of a char as separator. Never use this method with 1 character length strings, like: `String[] tokens = Convert.tokenizeString(input, “#”);` |

Use the previous method instead for better performance**:**

* **`toLowerCase(char c)`**: Converts the given char to lower case. 
* **`toUpperCase(char c)`**: Converts the given char to upper case. 
* **`zeroPad(String s, int size)`**: Pads the string, adding zeros at left. 
* **`zeroUnpad(String s)`**: Removes left zeros of the string.

### **Arrays**

|  |  |
| :--- | :--- |
| cloneStringArray\(String\[\] strs\) | Returns a copy of the given string array. |
| toStringArray\(Object\[\] objs\) | Converts the given object array into a string array, by calling toString\(\) for each object. |
| detectSortType\(Object item\) | Returns the sort type for the given item sample \(which is usually the first item of an array\). |

Convert provides the quick sort algorithm for array sorting.

### Constants

* **SORT\_AUTODETECT** - Chooses between one of the sort types below based on the first element of the array.
* **SORT\_OBJECT** - The objects are compared by their string representation.
* **SORT\_STRING** - The array contains String objects, and the sort is case sensitive.
* **SORT\_INT** - The array contains String objects that represents integer values.
* **SORT\_DOUBLE** - The array contains String objects that represents double values.
* **SORT\_DATE** - The array contains String objects that represents a Date object with day, month, and year.
* **SORT\_COMPARABLE** - The array contains comparable objects \(objects that implements the ****Comparable interface\).
* **SORT\_STRING\_NOCASE** - The array contains String objects, and the sort is case insensitive, which is slower than case sensitive sorting.

### **Methods**

* **qsort\(Object\[\] items, int first, int last\) -** Applies the quick sort algorithm to the elements of the given array, sorting in ascending order and sort type equals to SORT\_AUTODETECT. 
* **qsort\(Object\[\] items, int first, int last, int sortType\)** - Same as the above method, but you can specify the sort type. 
* **qsort\(Object\[\] items, int first, int last, int sortType, boolean ascending\)** - Same as the above, but you can also choose between sorting in ascending or descending order.

### **Other Conversions and Methods**

* **chars2int\(String fourChars\)** - Converts a creator id or type to int.
* **int2chars\(int i\)** - Converts an int to a creator id or type.
* **doubleToIntBits\(double f\)** - Converts the given double to its bit representation in IEEE 754 format, using 4 bytes instead of 8 \(a conversion to float is applied\).
* **intBitsToDouble\(int i\)** - Converts the given IEEE 754 bit representation of a float to a double.
* **doubleToLongBits\(double value\)** - Returns a representation of the specified floating-point value according to the IEEE 754 floating-point "double format" bit layout.
* **longBitsToDouble\(long bits\)** - Converts the given bit representation to a double.
* **rol\(long i, int n, int bits\)** - Does a rol of n bits in the given long. n must be &lt; bits. Unlike the shift left operator \(&lt;&lt;\), bits that would have been lost are reinserted in order at the right.
* **ror\(long i, int n, int bits\)** - Does a ror of n bits in the given long. n must be &lt; bits. Unlike the shift right operator \(&gt;&gt;\), bits that would have been lost are reinserted in order at the left.

### **Another Useful Constants**

| **Constants** |  |
| :--- | :--- |
| CRLF  | \r\n. |
| CRLF\_BYTES | {’\r’,’\n’} |
| MAX\_SHORT\_VALUE | The maximum short value: 32767 |
| MIN\_SHORT\_VALUE | The minimum short value: -32768. |
| MIN\_INT\_VALUE  | The minimum int value: -2147483648 |
| MAX\_INT\_VALUE | The maximum int value: 2147483647. |
| MIN\_LONG\_VALUE | The minimum long value: -9223372036854775808. |
| MAX\_LONG\_VALUE | The maximum long value: 9223372036854775807 |
| MAX\_DOUBLE\_VALUE |  The maximum double value: 9.007199254740992E15. |
| MIN\_DOUBLE\_VALUE  | The minimum double value: 1.1102230246251565E-16. |
| MAX\_DOUBLE\_DIGITS |  The maximum number of digits in a double value, used when formatting to string. |
| DOUBLE\_POSITIVE\_INFINITY\_VALUE | The double that represents a positive infinity. |
| DOUBLE\_NEGATIVE\_INFINITY\_VALUE | The double that represents a negative infinity. |
| DOUBLE\_POSITIVE\_INFINITY\_BITS | The long whose bits represent a positive infinity. |
| DOUBLE\_NEGATIVE\_INFINITY\_BITS | The long whose bits represent a negative infinity. |
| DOUBLE\_NAN\_BITS | The long whose bits represent a Not a Number \(NaN\). |

