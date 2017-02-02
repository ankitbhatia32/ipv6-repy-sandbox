# ipv6-repy-sandbox
Adding IPv6 functionality to the current RepyV2 Sandbox. Enabling extended functionality to Seattle Sandbox. Various IPv6 API function call added to the Repy Sandbox. 

# Introduction
With the growing need of IP addresses and IPv4 address exhuasting soon, people are shifting to IPv6 addresses in networking. IPv6 with its increasing demand is an essential which can be added to Seattle RepyV2 Sanbox. This will enable users having IPv6 capability can make of Seattle Sandbox.

Newly added emulcomm_ipv6 module and various IPv6 API function call added in the current extention 

# IPv6 Testbed
To test IPv6 functionality we will be using NorNet testbed. NorNet is wonderful platform which have many nodes having IPv6 capability. NorNet bascially consists of slices, these slices further contains various nodes which may or may not have IPv6 capability. One of the slice is "srl_seattle" which has many nodes having IPv6 capability, choose one of the nodes to work on. 

###SSH into NorNet
1. First of all you need Secure Shell(SSH) access to the login server of the NorNet test bed. For this you need a gatekeeper NorNet Username and Password. Using your Username and Password SSH into login server with following command:

```ssh <username>@gatekeeper.nntb.no```

Use port forwarding to access PLC and Monitor servers:

```ssh <username>@gatekeeper.nntb.no -L 2000:plc.simula.nornet:443 -L 2001:monitor.simula.nornet:80```

This forwards TCP port 2000 to PLC server's HTTPS port and forwards TCP port 2001 to Monitor server's HTTP port

2. Access to PLC and Monitor is done via port forwarding:

Monitor: (http://localhost:2001/)

PLC: (https://localhost:2000/)

After SSH into login server you can choose a slice & node using above PLC link with your gatekeeper username and password.

In order to gain access to one of the nodes of the NorNet, follow the following steps:

1. Choose one of the slice on NorNet for example "srl_seattle"
2. Choose a node from that slice on which you want work on. Please choose the one which has IPv6 support. For example "solvang.simula.nornet"
3. Once in the NorNet core, use the following command to SSH into a slice and its corresponding node:

```ssh -i <your private key> <slice name>@<node name>```

Note: Testbeds like NorNet is that nodes get reinsatlled more often and because of this, expect your progress to be washed away. It would be wise keep your progress up to date on github. 

# Basic Operation
To test IPv6 Implementation make sure you have Python 2 and git installed on your Linux machine. Make sure it has IPv6 capability. Lets follows certain steps to the functionality.

1. Clone branch "ipv6_sandbox_repy" from my forked [repy_v2 repository](https://github.com/ankitbhatia32/repy_v2) . You can clone it using the command:

```git clone -b ipv6_sandbox_repy https://github.com/ankitbhatia32/repy_v2.git```

2. Now initialize and build the newly cloned repy_V2 like we usually do. Refer this [link](https://seattle.poly.edu/wiki/RepyV2Tutorial) if you are new to seattle 

