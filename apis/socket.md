# Socket

## Overview

The **Socket** class allows you to open TCP/IP connections from your device. To be able to establish a connection with a particular server, both the server and the device must be connected to a common network \(e.g. a local network that connects your computers and devices, or the Internet\).

A **Socket** object denotes a client-server connection over a network using the TCP/IP protocol, where the device acts as a client, which connects to a specific server port.

The **Socket** class does not provide many methods besides the ones inherited from **Stream**. After creating a socket, you’ll usually just perform read and write operations, closing the socket after you’re done.

However, streams that handle remote connections are more likely to fail due to hardware and communication problems, so we shouldn’t handle socket operations the same way we do with file operations.

In TotalCross, socket’s read and write operations are blocking with a timeout – that means that socket methods will block the thread until the operation is completed, or the timeout for the operation is reached. If the operation is completed, the method returns immediately, regardless of the amount of time left. Otherwise, the method will just return the amount of data processed.

It’s important to notice that no exception is thrown if the method times out. This is just a way to prevent your thread from being blocked indefinitely because of communication problems. You may just keep executing the same method until it finishes processing all the data.

## **Constructors**

| Type | Name | Description |
| :--- | :--- | :--- |
| **constructor** | Socket\(String host, int port, int timeout, boolean noLinger\) | Creates a new socket that attempts to establish a connection by looking up the given host and performing the 3 way TCP/IP handshake. The argument port specifies the server port to connect to, while timeout specifies the timeout for this operation in milliseconds. The argument noLinger indicates if a socket upon close should shutdown the connection immediately or check for any server response before closing. |
| **constructor** | Socket\(String host, int port, int timeout\) | Same as the above, but uses the default value false for the argument noLinger. |
| **constructor** | Socket\(String host, int port\) | Same as the above, but uses the default value 1500 \(milliseconds\) for the argument timeout. |
| **constructor** | Socket\(String host, int port, int timeout, String params\) | Opens a socket with additional parameters. Each parameter is specified in a key=value form and separated by a ; from the next parameter. For example: p1=v1;p2=v2. If true, the socket is closed immediately, and no ack is waited from the server. Note that this must be done for the very first socket creation per application. |

You cannot open a socket before the main event loop. In other words, you cannot open a socket in the app’s constructor, but you can in the **initUI\( \)** method.

The socket general behavior, including the timeout for read and write operations, are stored in the following public fields:

* **`readTimeout`** - The timeout value for read operations. Its default value is Socket. `DEFAULT_READ_TIMEOUT`. 
* **`writeTimeout`** - The timeout value for write operations. Its default value is Socket. `DEFAULT_WRITE_TIMEOUT`.

Usually you should not worry about the read and write timeouts. The default values will be fine in most cases. However, you may increase the timeout value if you experience problems with slow connections.

Reducing the timeout value is usually a bad idea. If your device has a high speed connection, the read and write methods should also be fast and return before the timeout is reached. However, reducing the timeout value won’t give you any benefit, and may even decrease your program performance.

Methods for read and write operations:

## Methods:



| Type | Name | Description |
| :--- | :--- | :--- |
| **int** | readBytes\(byte\[\] buf\) | Attempts to read enough bytes from this socket to fill the given buffer. |
| **String** | readLine\( \) | Attempts to read a line of text from this socket. A line is a sequence of characters delimited by any character lower than blank. This method correctly handles newlines with \n or \r\n. |
| **int** | writeBytes\(byte\[\] buf\) | Attempts to write the contents of the given buffer to this socket. |
| **int** | writeBytes\(String s\) | Attempts to write the given string to this socket. |

Except for the method **readLine\( \)**, the methods above are just available for convenience and may be replaced by read/write calls inherited from **Stream**. This has a cost however - using these methods increases the number of method calls for each read/write operation by one \(they actually just call the **Stream** methods\). If your application makes heavy use of sockets, you may avoid using these methods to improve its performance.

## References

* For more details, check out **totalcross.net.Socket** [JavaDoc](https://rs.totalcross.com/doc/).

