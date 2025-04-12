Azure, FE-configuration-subnet BE-configuration-subnet


NSG on Subnet Level to restrict traffic on subnet level

Create a Vnet, with 3 subnets(prod,dev,qa), create 1 VM under each subnet-> total 3 VMs in same Vnet.

IMP: Okey the VMs can have any NSG(default etc) that'll be on NIC level.

On these 3 subnets we'll be configuring single NSG to restrict traffic (every server should not communicate to each other)

Note: if NSG is not on NSG level they can have communication 
with each other which is a default behaviour.


Now that all VMs are created create a NSG.

then in subnets associate all 3 subnets to this NSG.

this'll block communication, because by default NSG has no rule inbound RDP rule created. (although they were earlier be able to get public asses configuring NSG inbound rules on interface level, means without NSG on NIC level Vms could have been acssible)


So without subnet NSG the traffic will be directly routed to the VMs using public IPS,
And using this single NSG we can managed the traffic rule for all by configuring them on subnet level.



BACK TO THE TOPIC,

lets create a RDP rule in NSG( the one created on subnet level)
connect to all the servers and off the firewall and 

1. Ping production machine from dev machine( ping will work)
2. ping development machine from prod machine


Lets create a rule on subnet level to create a restrict rule to restrict internal communications.

(source) subnet 1 cannot talk to (destination) subnet 2 on any port

later you can add both the subnets in source and destination fields to restrict communication from both sides.

later again if needed do it for all the subnet in a network to restrict inter communication










