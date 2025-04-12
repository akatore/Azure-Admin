create a VNET
under same Vnet, create 3 Subnets

select same Vnet for all the VMs and just assign the created subnets to the VMs
dev-server <- dev-Subnet
qa-server <- qa-Subnet
prod-server <- prod-Subnet

RDP to Prod server
and RDP to Dev server

their respective using its Public IP, 
if try to ping the private IP of dev-server RTO will occur, but during mstsc you'll get connection 

then try turning off the dev-server's firewall

and then on again pinging dev-server's Private IP communication will happen 

