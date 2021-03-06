# ipv6-repy-sandbox
Adding IPv6 functionality to the current RepyV2 Sandbox. Enabling extended functionality to Seattle Sandbox. Various IPv6 API function call added to the Repy Sandbox. 

## Introduction
With the growing need of IP addresses and IPv4 address exhuasting soon, people are shifting to IPv6 addresses in networking. IPv6 with its increasing demand is an essential which can be added to Seattle RepyV2 Sanbox. This will enable users having IPv6 capability can make of Seattle Sandbox.

Newly added emulcomm_ipv6 module and various IPv6 API function call added in the current extention. New RepyV2 IPv6 modules are in repy_v2 branch [ipv6_sandbox_repy](https://github.com/ankitbhatia32/repy_v2/tree/ipv6_sandbox_repy), various scripts and newly added emulcomm_ipv6 module is in this branch of the Repy_V2 repository.

## IPv6 Testbed
To test IPv6 functionality we will be using NorNet testbed. NorNet is wonderful platform which have many nodes having IPv6 capability. NorNet bascially consists of slices, these slices further contains various nodes which may or may not have IPv6 capability. One of the slice is "srl_seattle" which has many nodes having IPv6 capability, choose one of the nodes to work on. 

Brief overview on how to SSH into NorNet is given below. For in depth details refer the [link](https://www.simula.no/file/simulasimula2130pdf/download)

### SSH into NorNet
  1. First of all you need Secure Shell(SSH) access to the login server of the NorNet test bed. For this you need a gatekeeper NorNet Username and Password. Using your Username and Password SSH into login server with following command:

      ```ssh <username>@gatekeeper.nntb.no```

  Use port forwarding to access PLC and Monitor servers:

      ```ssh <username>@gatekeeper.nntb.no -L 2000:plc.simula.nornet:443 -L 2001:monitor.simula.nornet:80```

  This forwards TCP port 2000 to PLC server's HTTPS port and forwards TCP port 2001 to Monitor server's HTTP port

  2. Access to PLC and Monitor is done via port forwarding:

      Monitor: 'http://localhost:2001/'

      PLC: 'https://localhost:2000/'

  3. After SSH into login server you can choose a slice & node using above PLC link with your gatekeeper username and password credentials.

  4. In order to gain access to one of the nodes of the NorNet, follow the following steps:

      1. Choose one of the slice on NorNet for example "srl_seattle"
      2. Choose a node from that slice on which you want work on. Please choose the one which has IPv6 support. For example              "solvang.simula.nornet"
      3. Once in the NorNet core, use the following command to SSH into a slice and its corresponding node
    
            ```ssh -i <your private key> <slice name>@<node name>```

Note: In testbeds like NorNet the nodes/machines get reinsatlled more often and because of this, expect your progress to be washed away after sometime. It would be wise keep your progress up to date on github. 

## Basic Operation
To test IPv6 Implementation make sure you have Python 2 and git installed on your Linux machine. Make sure it has IPv6 capability. Lets follows certain steps to the functionality.

  1. Clone branch "ipv6_sandbox_repy" from my forked [repy_v2 repository](https://github.com/ankitbhatia32/repy_v2) . You can clone it   using the command:

      ```git clone -b ipv6_sandbox_repy https://github.com/ankitbhatia32/repy_v2.git```

  2. Now intitialize and build the cloned repy_v2 by navigating into the scripts directory. This is shown as follows:
    
         ``` 
             $ cd repy_v2
             $ cd scripts
             $ python initialize.py
             $ python build.py 
         ```                  
         
     Refer this [link](https://seattle.poly.edu/wiki/RepyV2Tutorial) for complete details and if you are new to seattle.

  3. After building and intializing navigate to RUNNABLE directory. You will find that this directory will have all the desired files to run repy sandbox. Especially newly added emulcomm_ipv6.py module. Now lets try an example to test our implementation.

### Example
In this example we will run our implementation to find the local IPv6 address of the NorNet node. Follow the following steps:
  1. Assuming after cloning the repository you have initialized and build the implementation. Now navigate to RUNNABLE directory. 
  2. We will run r2py file 'localIPv6.r2py'. To run the file use the repy command as shown below:

      ```python repy.py restrictions.test localIPv6.r2py```
      
  3. The complete procedure is shown as follow:

```
srl_seattle@solvang.simula.nornet $ git clone -b ipv6_sandbox_repy https://github.com/ankitbhatia32/repy_v2.git
Cloning into 'repy_v2'...
remote: Counting objects: 1918, done.
Receiving objects: 100% (1918/1918), 1.18 MiB | 273.00 KiB/s, done.
remote: Total 1918 (delta 0), reused 0 (delta 0), pack-reused 1918
Resolving deltas: 100% (999/999), done.
Checking connectivity... done.
srl_seattle@solvang.simula.nornet $ cd repy_v2/
srl_seattle@solvang.simula.nornet $ cd scripts/
srl_seattle@solvang.simula.nornet $ python initialize.py 
Checking out repo from https://github.com/SeattleTestbed/seattlelib_v2 ...
Done!
Checking out repo from https://github.com/SeattleTestbed/portability ...
Done!
Checking out repo from https://github.com/SeattleTestbed/seash ...
Done!
Checking out repo from https://github.com/SeattleTestbed/affix ...
Done!
Checking out repo from https://github.com/SeattleTestbed/common ...
Done!
Checking out repo from https://github.com/SeattleTestbed/utf ...
Done!
srl_seattle@solvang.simula.nornet $ python build.py 
Building into /home/srl_seattle/repy_v2/RUNNABLE
Done building!
srl_seattle@solvang.simula.nornet $ cd ..
srl_seattle@solvang.simula.nornet $ cd RUNNABLE/
srl_seattle@solvang.simula.nornet $ python repy.py restrictions.test localIPv6.r2py 
2001:700:4100:901::b5:69
```
    
This is the IPv6 address for the node "solvang.simula.nornet"





