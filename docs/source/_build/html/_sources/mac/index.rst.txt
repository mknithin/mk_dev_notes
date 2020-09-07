##################
Programming in Mac
##################

Apple mac book pro is my preferred machine for programming. I'm a long time linux user and switched to mac for 3-4 years now.
I enjoyed the user interface of mac os and consistency of the machine, we programmers always require a tough machine and switching machine in between is lot of hassle.



How to list listening ports in mac  
**********************************

When you're developing apps that listen to port , you require a command to verify the port are really listening.
We use **netstat** command for that but it's not available in mac for default.(may be you can install it )

I always use the **lsof** command, and this is how it works

.. code-block::

    $ lsof -i -P | grep -i "listen"

    output:

    LogiMgrDa   449 nithinmk    8u  IPv4 0xff0ce6d23cfcf2d9      0t0  TCP *:59866 (LISTEN)
    node      12307 nithinmk   12u  IPv6 0xff0ce6d24f6b0ae9      0t0  TCP *:5556 (LISTEN)
    node      12307 nithinmk   13u  IPv6 0xff0ce6d24f6af269      0t0  TCP *:5557 (LISTEN)
    Kite      54597 nithinmk    9u  IPv4 0xff0ce6d256ad62d9      0t0  TCP localhost:46624 (LISTEN)
