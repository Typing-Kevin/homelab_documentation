# Step 4: ssh into AM from Test1

## What I had to deal with:

Alright, so step 4 took a while for me to deal with. So first, I started by ``sudo apt upgrade -y`` both devices. I did that to make sure both devices were up to date. Afterwards, I proceeded by going on to Test1 CLI, and typing ``ssh -v Homelab@192.168.0.110`` to see if I can ssh into AM. I used the verbose mode for the command because when I initially tried it, it was just blank and I had no idea what was going on (verbose shows the process of it trying to connect). However, it did not connect me to AM, it ended up displaying:

``Connecting to 192.168.0.110
[192.168.0.110] port 22.
connect to address 192.168.0.110 port 22: Connection refused
ssh: connect to host 192.168.110
port 22: connection refused``

Now, I was utterly confused as to why it said that. My guess was that AM wasn't configured correctly (even though I didn't touch it) or it must be the firewall. From this, I knew Test1 could reach AM, but the ssh connection to TCP port 22 was being refused.

I quickly moved over to AM, and checked to see if its ssh server was running. I typed ``sudo service ssh status`` and AM did report that sshd is running. So, from that message alone, I knew OpenSSH wasn't missing or stopped. I checked to see if AM was actively listening for ssh connections on port 22 by typing ``sudo ss -tlnp | grep :22``. The output I received two columns of:

``0.0.0.0:22
[::]:22``

Which meant that sshd was listening on port 22.

I was so stumped on what the hell to do. I had ZERO clue in this. So I did the best thing someone can do in this case: troubleshoot. So, thinking that maybe something was wrong on AM's side, I restarted the ssh service by typing ``sudo service ssh restart`` and then confirmed that sshd was still actively listening on port 22 by typing ``sudo ss -tlnp | grep :22``. It confirmed it. 

I wasn't sure what else could be the matter so I decided to make sure I had the right IP address, so I typed ``hostname -I``, which returned ``192.168.0.110``, which was the IP address I was using the whole time. So Test1 was attempting to connect to the right machine. So, I doubled down, and wanted to see if I can ssh into AM itself on AM as a debugging measure. I typed ``ssh Homelab@localhost``. I received that normal, first time authentication warning, so I proceeded to hit "yes" and entered AM's password. Everything went smoothly from here, so I knew the ssh server itself worked. 

From my best educated guess, it had to do with something affecting the connection coming from another machine than ssh being broken. So, I decided to check out AM's ufw firewall by typing ``sudo ufw status verbose`` and it showed:

``Status: active
Default: deny (incoming), allow (outgoing), disabled (routed)``

Which was super important, because it showed that AM's firewall was active and was configured to deny incoming connections by default. I also inspected the underlying firewall rules by typing ``sudo iptables -L -n -v`` and I literally saw a bunch of rules that I can't type here (too many), but thanks to that command, I saw that there was a default DROP policy for incoming traffic. This helped explain why ssh could work locally while Test1 couldn't initially do the remote connection.

During all of this, I actually created a .txt file on AM called "hello_test1.txt" in my Documents folder on AM. I did this with the intention of finding this file when I was able to ssh remotely from Test1 into AM and reading it from Test1. Keep that in mind.

I went back to Test1 and I attempted the connection again. I received the standard authentication warning for first time connection, hit yes, and it worked! My prompt changed from ``student@Echo2`` to ``Homelab@Homelab:~$``, which made me extremely happy. While I was remotely connected to AM, I typed ``ls`` and saw the ``/Documents`` directory. So I typed ``cd Documents`` and then typed ``ls``, once I was in the Documents folder on AM through Test1. It showed the text file I made "hello_test1.txt" and I ran ``cat hello_test1.txt`` and it displayed this message:

"Hi, if you can see this from Test1's device, you are doing good!"

