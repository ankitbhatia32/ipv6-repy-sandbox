# Tutorial
This part explains the IPv6 implementation of Repy_V2. Tutorial will explain basic implmentation related to IPv6 and most importantly, the difference in the approach between IPv4 & IPv6 Repy_V2 and various issues faced. Python IPv6 socket networking function library has been helpful throughout the implementation, which is given [here](https://docs.python.org/2/library/socket.html).

As we know with the given exhaustion of IPv4 addresses and the ever growing need of IP addresses, the world is moving from IPv4 to IPv6 addresses. 

## Repy_V2 IPv4 vs IPv6
IPv6 implementation of repy_v2 involved design and python socket functional differences from IPv4 which have been implemented. More details about the IPv6 socket functions is given [here](https://docs.python.org/2/library/socket.html)
Major difference in the Repy_v2 [IPv4](https://github.com/SeattleTestbed/docs/blob/master/Programming/RepyV2API.md) API functions and [IPv6](https://github.com/ankitbhatia32/ipv6-repy-sandbox/blob/master/IPv6_RepyV2API.md) functions can be compared.

#### Difference in Implementation
Repy_v2 IPv6 implementation is somewhat different than IPv4 implementation. Let us discuss major differences and issues faced in the Implementation:

  1. For hostname resolvement in IPv4 we generally use the following:
  				```socket.gethostbyname()```

  	 But for IPv6 we use the following socket functions:
  	 			```socket.getaddrinfo()```

  	 Both [IPv4](https://github.com/ankitbhatia32/repy_v2/blob/ipv6_sandbox_repy/emulcomm.py#L611) and [IPv6](https://github.com/ankitbhatia32/repy_v2/blob/ipv6_sandbox_repy/emulcomm_ipv6.py#L491) is compared emulcomm.py and emulcomm_ipv6.py module.

  2. Valid IPv4 address have been clearly defined in the IPv4 implementation. It clearly, bad or invalid IPv4 address is clearly defined as well as the valid IPv4 addresses for e.g. IPv4 address 198.168.0.0 is invalid address and is exactly invalidiated. This is clearly represented [here](https://github.com/ankitbhatia32/repy_v2/blob/ipv6_sandbox_repy/emulcomm.py#L452-L506).

  But on the otherhand clearly defining valid IPv6 address is an issue as there is a huge sample space of IPv6 addresses so for this, the following socket function is used:
  				```socket.inet_pton(socket.AF_INET6, ipaddr)```
  This convert an IP address from its family-specific string format to a packed, binary format. In the implementation it is represented in emulcomm_ipv6.py module [here](https://github.com/ankitbhatia32/repy_v2/blob/ipv6_sandbox_repy/emulcomm_ipv6.py#L398)

  3.     
