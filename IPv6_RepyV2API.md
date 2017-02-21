# IPv6 Repy V2 Library Reference
This document describes the narrow IPv6 API available to repy programs. This document includes all of the calls that are available to a repy program and the use and meaning of these calls. For items built into the python programming language (like list operations, etc.) see the appropriate Python documentation.

The intent is that we will build libraries that will provide 'rich' functionality on top of these abstractions. For example, the file-like objects don't support next, but we can build this in a library. Also, notice that the logging mechanism doesn't support multiple arguments / do type conversion. We can do this in a user level library. We will expect that all users will load this library (and may even do it for them).

For IPv4 Repy_V2 API function library, refer this [link](https://github.com/SeattleTestbed/docs/blob/master/Programming/RepyV2API.md)

## Detailed Description

### API functions

#### Network functions

##### getAddripv6(name)
This API function is similar to gethostbyname in IPv4. It returns the IPv6 address of the host in string format in a list

 * Doc string:
	
	  ```
	  """
	   <Purpose>
	      Provides information about a hostname. Calls socket.getaddrinfo() instead of socket.gethostbyname().
	      Translate a host name to IPv6 address format. The IPv6 address is
	      returned in a list, such as [(30, 2, 17, '', ('2404:6800:4009:806::2004', 0, 0, 0))]. If the host name is an
	      IPv6 address itself it is returned unchanged.
	   <Arguments>
	     name:
	         The host name to translate.
	   <Exceptions>
	     RepyArgumentError (descends from NetworkError) if the name is not a string
	     NetworkAddressError (descends from NetworkError) if the address cannot
	     be resolved.
	   <Side Effects>
	     None.
	   <Resource Consumption>
	     This operation consumes network bandwidth of 4K netrecv, 1K netsend.
	     (It's hard to tell how much was actually sent / received at this level.)
	   <Returns>
	     The IPv6 address as a list.
	  """
	  ```


##### getmyip_ipv6()
Returns the localhost's "Internet facing" IPv6 address. If there are multiple interfaces, this IP will be on the interface that will be used by default to handle traffic to Internet hosts. Note that if the node is behind a NAT or similar, this may be a private IP. It may raise an exception on hosts that are not connected to the Internet.

 * Doc string:

      ```
	  """
	   <Purpose>

	      Provides the IP of this computer on its public facing interface.  
	      Does some clever trickery. 

	   <Arguments>

	      None
	   
	   <Exceptions>

	      InternetConnectivityError is the host is not connected to the internet.

	   <Side Effects>

	      None.
	   <Resource Consumption>

	      This operations consumes 256 netsend and 128 netrecv.
	   <Returns>

	      The localhost's IPv6 address
	  """
	  ```  


##### sendmessage_ipv6(destip, destport, message, localip, localport):
Sends a UDP message to a destination host / port using a specified local IPv6 address and localport. Returns the number of bytes sent.

 * Doc string:

    ```
	"""
     <Purpose>

       Send a message to a host / port

     <Arguments>

       destip:
          The IPv6 address to send the message to
       destport:
          The port to send the message to
       message:
          The message to send
       localip:
          The local IPv6 address to send the message from 
       localport:
          The local port to send the message from

     <Exceptions>
       AddressBindingError (descends NetworkError) when the local IP isn't
       a local IP.

       ResourceForbiddenError (descends ResourceException?) when the local
       port isn't allowed

       RepyArgumentError when the local IP and port aren't valid types
       or values

       AlreadyListeningError if there is an existing listening UDP socket
       on the same local IP and port.

       DuplicateTupleError if there is another sendmessage on the same
       local IP and port to the same remote host.
    """
	``` 

##### openconnection_ipv6(destip, destport, localip, localport, timeout)
Open a TCP connection to a remote computer, returning a socket object. There is a timeout value that can be set to limit the amount of time the system will wait for a response before abandoning the attempt to connect.

  * Doc string:

	    ```
		"""
		  <Purpose>
		    Opens a connection, returning a socket-like object


		  <Arguments>
		    destip: The destination ip to open communications with

		    destport: The destination port to use for communication

		    localip: The local ipv6 to use for the communication

		    localport: The local port to use for communication

		    timeout: The maximum amount of time (in seconds) to wait to connect.   This may
		             be a floating point number or an integer


		  <Exceptions>

		    RepyArgumentError if the arguments are invalid.   This includes both
		    the types and values of arguments. If the localip matches the destip,
		    and the localport matches the destport this will also be raised.

		    AddressBindingError (descends NetworkError) if the localip isn't 
		    associated with the local system or is not allowed.

		    ResourceForbiddenError (descends ResourceError) if the localport isn't 
		    allowed.

		    DuplicateTupleError (descends NetworkError) if the (localip, localport, 
		    destip, destport) tuple is already used.   This will also occur if the 
		    operating system prevents the local IP / port from being used.

		    AlreadyListeningError if the (localip, localport) tuple is already used
		    for a listening TCP socket.

		    CleanupInProgressError if the (localip, localport, destip, destport) tuple is
		    still being cleaned up by the OS.

		    ConnectionRefusedError (descends NetworkError) if the connection cannot 
		    be established because the destination port isn't being listened on.

		    TimeoutError (common to all API functions that timeout) if the 
		    connection times out

		    InternetConnectivityError if the network is down, or if the host
		    cannot be reached from the local IP that has been bound to.

		  <Resource Consumption>
		    This operation consumes 64*2 bytes of netsend (SYN, ACK) and 64 bytes 
		    of netrecv (SYN/ACK). This requires that the localport is allowed. Upon 
		    success, this call consumes an outsocket.

		  <Returns>
		    A socket-like object that can be used for communication. Use send, 
		    recv, and close just like you would an actual socket object in python.
		"""
	    ```	

##### listenforconnection_ipv6(localip, localport)
Binds to an IP and port and waits for incoming TCP connections. If this function is called multiple times on the same ip and port without the first tcpserversocket being closed, the second call will have an exception. These ports are separate from the message ports and so both a message and connection listener can use the same port. This call raises an exception instead of blocking.

  * Doc string:

      ```
      """
        <Purpose>
          Sets up a TCPServerSocket to recieve incoming TCP connections. 

        <Arguments>
          localip:
            The local IP to listen on
          localport:
            The local port to listen on

        <Exceptions>
          Raises AlreadyListeningError if another TCPServerSocket or process has bound
          to the provided localip and localport.

          Raises DuplicateTupleError if another process has bound to the
          provided localip and localport.

          Raises RepyArgumentError if the localip or localport are invalid

          Raises ResourceForbiddenError if the ip or port is not allowed.

          Raises AddressBindingError if the IP address isn't a local ip.

        <Side Effects>
          The IP / Port combination cannot be used until the TCPServerSocket
          is closed.

        <Resource Consumption>
          Uses an insocket for the TCPServerSocket.

        <Returns>
          A TCPServerSocket object.
      """
      ```    

##### listenformessage_ipv6(localip, localport)
Binds to an IPv6 address and port and waits for incoming UDP messages. If this function is called multiple times on the same ip and port without the first udpserversocket being closed, the second call will have an exception. These ports are separate from the connection ports and so both a message and connection listener can use the same port. This call will raise an exception if it would block.

 * Doc string:

    ```
    """
        <Purpose>
          Sets up a UDPServerSocket to receive incoming UDP messages.

        <Arguments>
          localip:
            The local IP to register the handler on.
          localport:
            The port to listen on.

        <Exceptions>
          DuplicateTupleError (descends NetworkError) if the port cannot be
          listened on because some other process on the system is listening on
          it.

          AlreadyListeningError if there is already a UDPServerSocket with the same
          IP and port.

          RepyArgumentError if the port number or ip is wrong type or obviously
          invalid.

          AddressBindingError (descends NetworkError) if the IP address isn't a
          local IP.

          ResourceForbiddenError if the port is not allowed.

        <Side Effects>
          Prevents other UDPServerSockets from using this port / IPv6 address

        <Resource Consumption>
          This operation consumes an insocket and requires that the provided messport is allowed.

        <Returns>
          The UDPServerSocket.
    """
    ```  

Note: This documentation points mainly to IPv6 implementation of repy_v2. These API functions are different from the already implemented IPv4 repy_v2, rest of them are usually the same as given [here](https://github.com/ankitbhatia32/docs/blob/master/Programming/RepyV2API.md). More API functions may be added as more refinement of documentation is done.



