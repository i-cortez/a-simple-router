# A Simple Router - Final Project for CSE 150
## Description
This project simulates a production network for a small company. The company has a 2 floor building with each floor having its own switches and subnets. In addition, there is a switch and subnet for all the servers in the data center, and a core switch connecting everything together. The goal is to protect the company network from outside access and to allow or block traffic between the internal hosts and servers. This is achieved by implementing routing between devices on different subnets and implementing firewalls for certain subnets.
## How to Run the Project
* Install Mininet: http://mininet.org/download/#important-note-python-2-and-python-3-mininet
* Once on the Mininet VM clone the project
* The `finalcontroller_skel.py` file needs to be placed in `~/pox/pox/misc` and `final_skel.py` should be placed in the home directory (~)
* Launch the controller with the command `sudo ~/pox/pox.py misc.finalcontroller_skel
* In a separate terminal, run the Mininet file with the command `sudo python ~/final_skel.py`
* The Mininet file should now be running and we can enter commands at `mininet>` to verify the network configuration
## Testing the Network
