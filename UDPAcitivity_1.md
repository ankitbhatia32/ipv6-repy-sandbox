# Activity 1
In this Activity we'll take two IPv6 enabled NorNet nodes and setup a UDP connection between the two nodes. You can choose any two nodes by following Introduction. 

## Setup
Follow the steps to setup the test case:

1. First choose two nodes and clone the branch "ipv6_sandbox_repy" of repy_v2 on both the nodes. Initialize and build as we discussed before.

2. On one node we'll run our listen case and on the other node we'll run our send test case. Listen r2py test case is "test1_listen.r2py" and the send r2py test case is "test1_send.r2py"  

3. Run listen test. This will be shown as follows:

```
srl_seattle@akerselva.simula.nornet $ python repy.py restrictions.test test1_listen.r2py 
Now listening.....

```

Now the UDP listen case has started listening

3. Now run the send test case on another NorNet node. But before you run this, using 'vim' command change the destination IPv6 address to the IPv6 address of the listening node and also change the message you want to send, here I am trying to send message "Hello". When we run our send case we can see our message on our listening node, both are represented as follow:

Send Part:

```
srl_seattle@solvang.simula.nornet # python repy.py restrictions.test test1_send.r2py 
5
```

Finally Listen Part looks like as follows:

```
srl_seattle@akerselva.simula.nornet # python repy.py restrictions.test test1_listen.r2py 
Now listening.....
Hello
Terminated
```

This completed our UDP connection between two nodes.
