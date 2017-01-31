# ipv6-repy-sandbox
Adding IPv6 functionality to the current RepyV2 Sandbox. Enabling extended functionality to Seattle Sandbox. 

# Introduction
With the growing need of IP addresses and IPv4 address exhuasting soon, people are shifting to IPv6 addresses in networking. IPv6 with its increasing demand is an essential which can be added to Seattle RepyV2 Sanbox. This will enable users having IPv6 capability can make of Seattle Sandbox.

Newly added emulcomm_ipv6 module and various IPv6 API function call added in the current extention 

# IPv6 Testbed
To test IPv6 functionality we will be using NorNet testbed. NorNet is wonderful platform which have many nodes having IPv6 capability. NorNet bascially consists of slices, these slices further contains various nodes which may or may not have IPv6 capability. One of the slice has "srl_seattle" which has many nodes which are IPv6 enbaled, choose one of the nodes to on.

Note: Testbeds like NorNet is that nodes get reinsatlled more often and because of this, expect your progress to be washed away. It would be wise keep your progress up to date on github. 

# Basic Operation
To test IPv6 Implementation make sure you have Python 2 and git installed on your Linux machine. Make sure it has IPv6 capability. Lets follows certain steps to the functionality.

1. Clone the branch "ipv6_sandbox_repy" from my forked [repy_v2 repository](https://github.com/ankitbhatia32/repy_v2) . You can clone it using the command:
```git clone -b ipv6_sandbox_repy https://github.com/ankitbhatia32/repy_v2.git```

2. Now initialize and build the newly cloned repy_V2 like we usually do. Refer this [link](https://seattle.poly.edu/wiki/RepyV2Tutorial) if you are new to seattle 

3. 