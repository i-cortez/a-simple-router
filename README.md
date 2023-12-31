# A Simple Router - Final Project for CSE 150
## Description
This project simulates a production network for a small company. The company has a 2 floor building with each floor having its own switches and subnets. In addition, there is a switch and subnet for all the servers in the data center, and a core switch connecting everything together. The goal is to protect the company network from outside access and to allow or block traffic between the internal hosts and servers. This is achieved by implementing routing between devices on different subnets and implementing firewalls for certain subnets.
## How to Run the Project
* Install Mininet: http://mininet.org/download/
* Once on the Mininet VM clone the project
* The `finalcontroller_skel.py` file needs to be placed in `~/pox/pox/misc` and `final_skel.py` should be placed in the home directory (~)
* Launch the controller with the command `sudo ~/pox/pox.py misc.finalcontroller_skel
* In a separate terminal, run the Mininet file with the command `sudo python ~/final_skel.py`
* The Mininet file should now be running and waiting for commands `mininet>`
## Testing the Network
First we verify that the devices are successfully created using the `nodes` command:<br/>
![sample output](/images/snip-1.png)<br/>
Take note of the host names under `available nodes are`.
<br/><br/>
Next, we verify that the links are successfully created using the `net` command:<br/>
![sample output](/images/snip-2.png)
<br/><br/>
Verify that the IP addresses are correct using the `dump` command:<br/>
![sample output](/images/snip-3.png)
<br/><br/>
Use the `pingall` command to verify that the devices can communicate on the network:<br/> 
![sample output](/images/snip-4.png)<br/>
Note that this takes up to 10 minutes to complete and due to the controller configuration, communication is only allowed between authorized parties.
<br/><br/>
Now we can test the firewalls and routing between devices.
The Untrusted Host cannot send ICMP traffic to Hosts 10 to 80. For example, to verify that the Untrusted Host cannot send ICMP traffic to Host 10, use the command `h_untrust ping -c 1 h10`:<br/>
![sample output](/images/snip-5.png)
<br/><br/>
The Untrusted Host can send ICMP traffic to the Trusted Host. Verify this with the command `h_untrust ping -c 1 h_trust`. The Untrusted Host can send TCP traffic to all hosts. For exapmle, to verify that the Untrusted Host can send TCP traffic to Host 10, use the command `iperf h_untrust h10`:<br/>
![sample output](/images/snip-6.png)
<br/><br/>
The Untrusted Host cannot send IP or ICMP traffic to the server. To verify this, use the command `h_untrust ping -c h_server:`<br/>
![sample output](/images/snip-7.png)
<br/><br/>
The Trusted Host cannot send IP or ICMP traffic to the Server. Verify this using the command `h_trust ping -c 1 h_server:`<br/>
![sample output](/images/snip-8.png)
<br/><br/>
The Trusted Host cannot send ICMP traffic to Hosts 10 through 40 but can send ICMP traffic to Hosts 50 through 80. For example, to verify that the Trusted Host can send ICMP traffic to Host 50, use the command `h_trust ping -c 1 h50:`<br/>
![sample output](/images/snip-9.png)
![sample output](/images/snip-10.png)
<br/><br/>
Hosts 10 through 40 cannot send ICMP traffic to Hosts 50 - 80 and vice versa. For example, to verify that Host 10 cannot send ICMP traffic to Host 50, use the comand `h10 ping -c 1 h50`:<br/>
![sample output](/images/snip-11.png)
<br/><br/>
Hosts 10 through 80 are allowed to send other types of traffic between each other. Verify this using the command `iperf h10 h50`:<br/>
![sample output](/images/snip-12.png)
