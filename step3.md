# Step 3: Ping AM from "Test1" laptop

After I acquired AM's IPv4 address (192.168.0.110), I opened up Test1, and signed into my Virtual machine running Debian 13. From here, I opened the terminal in Test1 and typed in ``ping 192.168.0.110``, and it actively retrieved data packets from AM. I let it run for a while before I terminated it. The summary was this:

--- 192.168.0.110 ping statistics ---

151 packets transmitted, 151 received, 0% packet loss, time 150923ms rtt min/avg/max/mdev = 3.896/57.139/200.770/45.331 ms

## Explaining the ping statistic

From what I researched, each ping statistic says something:

* 151 packets transmitted means Test1 sent 151 ICMP Echo Request packets to AM.
* 151 received means AM successfully responded to every single one.
* 0% packet loss means nothing was lost during the test. It means my connection is reliable. 
* 150923 ms means the entire ping test ran for about 151 seconds (about 2 minutes and 31 seconds)

The rtt stands for (Round Trip Time), and it's to measure how long it took a packet to travel from Test1 to AM and to Test1 again. Here's a breakdown of what the rtt says:

* 3.896 ms is the minimum measurement, meaning it is the fastest response.
* 57.139 ms is the average measurement, it's the average round trip response.
* 200.770 ms is the maximum measurement, which means its the slowest response.
* 45.331 ms is the mdev (deviation) measurement, which means how much latiency varied.

From what I'm seeing looking at my statistics, it's showing me that my response times are inconsistent to the degree I want it. Sometimes the responses would be around 4ms and then jump to 201 ms. Now, from what I gathered, 57ms is higher than I'd want for a LAN connection. But, both devices are on WI-FI, maybe that's why?? I'll investigate this later. Right now, this is good because it proves these devices can find each other.