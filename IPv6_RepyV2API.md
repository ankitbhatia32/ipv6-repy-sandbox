# IPv6 Repy V2 Library Reference
This document describes the narrow IPv6 API available to repy programs. This document includes all of the calls that are available to a repy program and the use and meaning of these calls. For items built into the python programming language (like list operations, etc.) see the appropriate Python documentation.

The intent is that we will build libraries that will provide 'rich' functionality on top of these abstractions. For example, the file-like objects don't support next, but we can build this in a library. Also, notice that the logging mechanism doesn't support multiple arguments / do type conversion. We can do this in a user level library. We will expect that all users will load this library (and may even do it for them).

## Detailed Description

### API functions

#### Network functions

##### getAddripv6(name)
This API function is similar to gethostbyname in IPv4. It returns the IPv6 address of the host in the string format.
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