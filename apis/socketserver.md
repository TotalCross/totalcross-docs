# SocketServer

## Overview

This class implements server sockets. A server socket waits for requests to come in over the network. It may then accept the incoming TCP/IP connection and perform some operation based on that request, possibly returning a result to the requester.

**ServerSocket** constructors:

## Constructors

| Type | Name | Description |
| :--- | :--- | :--- |
| **constructor** | ServerSocket\(int port\) | Attempts to open a server socket at the specified port number. By default, the maximum number of simultaneous connections allowed is DEFAULT\_BACKLOG and the default timeout for accept is DEFAULT\_SOTIMEOUT, and the server is not bound to any specific local address. The port number must be between 0 and 65535. |
| **constructor** | ServerSocket\(int port, int timeout\) | Same as the above, but you may also specify the timeout value, in milliseconds, for the accept operation. This value must be a positive value, or 0 to wait forever. |
| **constructor** | ServerSocket\(int port, int timeout, String addr\) | Same as the above, but you may also specify a local address, which the server should bind to. If the argument addr has a null value, it is ignored and the server is not bind to any address. |
| **constructor** | ServerSocket\(int port, int timeout, int backlog, String addr\) | Same as the above, but you may also specify the maximum number of simultaneous connections allowed with the argument backlog, which must have a positive value. |

You may retrieve the address and port values of this **ServerSocket** with **`getHost()`** and **`getLocalPort( )`**.

After creating a server socket, you may use the method **`accept()`** to wait for incoming connections. This method blocks the thread for the amount of time specified by the timeout value passed to the constructor, returning a **null** value when the timeout is over, or until a connection request is received and accepted, returning a socket instance representing the new connection.

The returned object is always a valid **Socket** instance, that may be used to transfer data between this server and the client that requested the connection, and that should be closed when no longer needed.

You should never use blocking operations on threads handling events and/or the graphical interface, otherwise the user won’t be able to interact with the application. Take a look at the source code of the sample ServerSocketTest.

Finally, you may use the method **`close()`** to close this server socket, releasing any associated resources.

Remember to close any sockets associated to this server socket before closing it. Otherwise all open sockets will throw an **IOException**.

## References

* For more details, check out **totalcross.net.ServerSocket** [JavaDoc](https://rs.totalcross.com/doc/).

