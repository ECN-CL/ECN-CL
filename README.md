# ECN-CL
The operation of both scripts is summarized as follows. 
The ECN injector is in charge of setting b1 = 1, N1 times during Nw packets. For this simple test, the script generates the IP packets. However, in a real scenario these packets will be those forwarded by this node. Hence, for a certain level of congestion η, the algorithm to decide the value of b1 is: 

load=L 
total_sent=0 
ecn1_sent=0 
ratio=0.5 //initial ratio 
while true; 
obj_ratio=load/100 
if obj_ratio >= ratio 
send packet with ECN=1 
else 
send packet with ECN=1 
total_sent=total_sent++ 
ratio=ecn1_sent/total_sent 

This algorithm always tries to maintain the estimation error in the ECN reader as lower as possible. Each time a new update in the congestion level is made, the algorithm must be executed again. An example of usage for this script is: 

python ecn_injector.py -s aaa.aaa.aaa.aaa -d bbb.bbb.bbb.bbb -q 45 

where the options are: 

-h, --help Show the help message 
-s IP, --src=IP Source IP address 
-d IP, --dst=IP Destination IP address 
-q Load-level, --load=Load-level Load level from 0-100 

The ECN reader reads all IP packets that come from a specific interface and estimate the congestion level for each flow. This is made through the estimation of the ratio of packets with b1=1 between the total number of packets in window with a size Nw. The window length is in packets, and for this example is a non-overlapping window. Since the inter-arrival time between packets is random, the update interval for congestion estimation varies with time. The use of this script is: 

python sniffer2.py -w 5 

where the options are: 

-h, --help Show this help message and exit 
-w WinSize, --win=WinSize Window Size in number of packets 
