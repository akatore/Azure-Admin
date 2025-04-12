VNET Peering between 2 vnet from same location / subscription / tenant / account

VNET Peering between 2 vnet from different location / same subscription / same tenant / same account

VNET Peering between 2 vnet from same or different location / same or diff subscription / same tenant / same account


when we create a Vnet Peering, MS on the backend updates route table in the system route gets updated.
UDR (user defined routes: that can overcome system routes)


if we have network in same region why we need different network?
to segregate the infrastructure.

(subnet level segregation is not recommended way in to the production, so segregation is done on Network level)


To create VNet Peering, just have TWO VNets and in setting of one of the VNet click on peering and you'll have to select the Vent to which you want to create connection with.

there two field Remote peering link and local peering link.
