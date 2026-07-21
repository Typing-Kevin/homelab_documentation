# Step 1: Install additional SSH tools on AM

Okay, for this beginner step, I have to understand what I'm working with here. AM's operating system is MX Linux due to the amount (or lack there of) of RAM (2GB) and available storage (about 28 GB). 

First step, I opened the terminal (CLI to save time), and I typed in ``sudo apt upgrade -y`` before checking to see if this version of Linux had everything I needed. After I confirmed that everything was up to date, I proceeded to check to see if I had nmap. I typed in ``sudo apt install nmap``, ``sudo apt nstal net-tools -y``, and ``sudo apt install traceroute``.  Why did I do this? 

Well, ``nmap`` is a network discovery and auditing tool that, from my understanding, scans open ports, services and vulnerabilities. And ``net-tools`` contains commands like ``ifconfig``, ``route``, ``arp``, and ``netstat``. Lastly, ``traceroute`` is good because it's a network diagnostic tool that basically traces the path packets take from my host machine to a destination host. I will most likely need these things later, and since I'm experimenting, I might as well check to see if I have them available.

Now, most people would wonder, "Don't most Linux distros already have SSH capabilties and tools?". And the answer is... I'd rather be sure. I like to triple check if I have something installed on my computer. On most modern Linux distributions, I know SSH capabilities are typically pre installed. But in the extra tools I have installed, I had to double check if I had it or it needed to be installed. No harm in these things.

Now, I wanted to install ``openssh-server`` so I can run my own SSH server. And I also installed ``openssh-client`` to connect to remote SSH servers as well. Funny story, I had to write the command twice because I did "install apt openssh-server openssh-client" and then thinking it was wrong because I thought there was no space between server and openssh, typed "install apt openssh-serveropenssh-client". Obviously, the actual command that's correct is ``sudo apt install openssh-server openssh-client``. 

Always proofread commands and say it out loud. That was TRULY the lesson for this step.

The last command I typed was ``sudo apt install tree`` because I like to see my directories as beautiful trees. I'm a visual learner, it just works for me personally.