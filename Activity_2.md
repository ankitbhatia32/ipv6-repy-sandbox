# Activity 2
In this activity similar to activity 1, here also we'll take IPv6 enabled NorNet nodes and setup a TCP connection between the two nodes instead of UDP connection. Again you can choose any two IPv6 enabled NorNet nodes by following the steps given in the Introduction.

## Setup
Let us setup the TCP test case:

1. First choose two nodes and clone the branch "ipv6_sandbox_repy" of repy_v2 on both the nodes. Initialize and build as we discussed before.

2. On one node we'll run our listen case and on the other node we'll run our send test case. Listen r2py test case is "listen_tcp.r2py" and the send r2py test case is "send_tcp.r2py" 

3. First we will setup a connection between the listening node and the sending node. This is a TCP test case so first the connection setup take place, and the connection is maintained untill terminated. Let us run the listening node:
  ```
     srl_seattle@yalongbay.hu.nornet $ python repy.py restrictions.test listen_tcp.r2py 
     Now Listening.......
  ```
  Note: We have used "alongbay.hu.nornet" NorNet node here. You can choose any IPv6 enabled node.

  Now, lets run send part on another node. This is shown as follows:
  ```
     srl_seattle@nanshan.hu.nornet $ python repy.py restrictions.test send_tcp.r2py 
     5 
  ```   
  Note: Here we choosen "nanshan.hu.nornet" NorNet node. Also, "5" above represents the length of the message sent.

  We can see the recieved message on our listening node and also the connection will not be terminated as it used in UDP test case activity. This is shown as follows:
  ```
     srl_seattle@yalongbay.hu.nornet $ python repy.py restrictions.test listen_tcp.r2py 
     Now Listening.......
     Hello

  ```

4. We can see our intended message recieved on the listening side of the connection. If we run the send case multiple times we will recieve multiple "Hello" message on the listening node. This is shown as follows:
   ```
   srl_seattle@yalongbay.hu.nornet $ python repy.py restrictions.test listen_tcp.r2py 
   Now Listening.......
   Hello 
   Hello 
   Hello 
   Hello

   ``` 

   We can see the multiple Hello message as above. 			 

