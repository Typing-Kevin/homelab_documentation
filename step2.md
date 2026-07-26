# Step 2: Find AM's IP address

Interestingly enough, this is the simplest step. I logged on to AM, went to the terminal, and typed ``hostname -I`` to get AM's IP address. However, I wanted a better breakdown of both IPv4 and IPv6 IP addresses, so I typed ``ip a``. From my understanding of these two different commands, ``hostname -I`` is good to quickly show you your IP address (IPv4 only), where as ``ip a`` or ``ip addr`` will show you both IPv4 and 6, and other things about the network.

Now that I have an IP address I can work with, I can move on to the next step in the lab.