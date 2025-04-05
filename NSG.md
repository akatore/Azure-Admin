# NSG
NSGs are region specific(can be used by different resources or different **resource group** in a single region), we can associate it to one or more NICs of VM, so they all following th same NSG rules.
![image](https://github.com/user-attachments/assets/929e0680-10c2-49de-ae81-a3407086ba70)


# **Lab: In a single network, we'll configure VMs from different RG to use NSG created in different RG in a single region.**
## Lets Create Two Resource Groups, one for VMs and one for NSGs.

### NSG-RG
![image](https://github.com/user-attachments/assets/d34e720d-ed6d-4fea-a9c1-7d7125ec4e72)
![image](https://github.com/user-attachments/assets/9b5fba47-23bd-499d-a91c-7cfbb28b9b7c)

### VM-RG
![image](https://github.com/user-attachments/assets/d2d918de-62db-4bf3-83f4-633f0506587c)
![image](https://github.com/user-attachments/assets/81a23106-91af-478d-b5d8-2a2a9d93f98d)


Lets create NSG first then we'll create VMs

![image](https://github.com/user-attachments/assets/7acf03e9-8d08-466c-8c34-b677419ad8cd)
![image](https://github.com/user-attachments/assets/48c961fa-5976-41d7-bf2c-eba102e9fb2a)
![image](https://github.com/user-attachments/assets/98b07eee-c4cb-4946-b627-edae85c649ef)


![image](https://github.com/user-attachments/assets/6c0f00c2-6a87-499c-a5d3-03d9498e70f8)
```
Custom security rules
0 inbound, 0 outbound
Associated with
0 subnets, 0 network interfaces
  
```

theres no resource two which its is associtated with
![image](https://github.com/user-attachments/assets/08d87750-3a21-4944-b114-af07f0f18fa5)

look closely we only have these 3 rules in inbound rule, so defauly deny is for all incomming traffic, so if we later try to assign it to a windows 16 VM, we wont be able to access the VM as no Inbond rule is created for RGP connection. Later point of time, we we have all VMs created and attached we'll explictly add one inbound rule to white list traffic comming from Internet or specific whitlisted IPs on RDP ports so to allow access to the VMs.

![image](https://github.com/user-attachments/assets/ee1e87e7-5b03-4ba8-a18c-8770dc608d22)


 
```json
{
    "name": "webservers-nsg",
    "id": "/subscriptions/e64b6c02-66fb-4acc-a0c0-68038660f611/resourceGroups/NSG-RG/providers/Microsoft.Network/networkSecurityGroups/webservers-nsg",
    "etag": "W/\"ca8c6d0d-b2f5-480c-b30e-304351e57fb4\"",
    "type": "Microsoft.Network/networkSecurityGroups",
    "location": "eastus",
    "tags": {},
    "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "94e65ea1-5c62-4abc-ad4c-b9e69b645a29",
        "securityRules": [],
        "defaultSecurityRules": [
            {
                "name": "AllowVnetInBound",
                "id": "/subscriptions/e64b6c02-66fb-4acc-a0c0-68038660f611/resourceGroups/NSG-RG/providers/Microsoft.Network/networkSecurityGroups/webservers-nsg/defaultSecurityRules/AllowVnetInBound",
                "etag": "W/\"ca8c6d0d-b2f5-480c-b30e-304351e57fb4\"",
                "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules",
                "properties": {
                    "provisioningState": "Succeeded",
                    "description": "Allow inbound traffic from all VMs in VNET",
                    "protocol": "*",
                    "sourcePortRange": "*",
                    "destinationPortRange": "*",
                    "sourceAddressPrefix": "VirtualNetwork",
                    "destinationAddressPrefix": "VirtualNetwork",
                    "access": "Allow",
                    "priority": 65000,
                    "direction": "Inbound",
                    "sourcePortRanges": [],
                    "destinationPortRanges": [],
                    "sourceAddressPrefixes": [],
                    "destinationAddressPrefixes": []
                }
            },
            {
                "name": "AllowAzureLoadBalancerInBound",
                "id": "/subscriptions/e64b6c02-66fb-4acc-a0c0-68038660f611/resourceGroups/NSG-RG/providers/Microsoft.Network/networkSecurityGroups/webservers-nsg/defaultSecurityRules/AllowAzureLoadBalancerInBound",
                "etag": "W/\"ca8c6d0d-b2f5-480c-b30e-304351e57fb4\"",
                "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules",
                "properties": {
                    "provisioningState": "Succeeded",
                    "description": "Allow inbound traffic from azure load balancer",
                    "protocol": "*",
                    "sourcePortRange": "*",
                    "destinationPortRange": "*",
                    "sourceAddressPrefix": "AzureLoadBalancer",
                    "destinationAddressPrefix": "*",
                    "access": "Allow",
                    "priority": 65001,
                    "direction": "Inbound",
                    "sourcePortRanges": [],
                    "destinationPortRanges": [],
                    "sourceAddressPrefixes": [],
                    "destinationAddressPrefixes": []
                }
            },
            {
                "name": "DenyAllInBound",
                "id": "/subscriptions/e64b6c02-66fb-4acc-a0c0-68038660f611/resourceGroups/NSG-RG/providers/Microsoft.Network/networkSecurityGroups/webservers-nsg/defaultSecurityRules/DenyAllInBound",
                "etag": "W/\"ca8c6d0d-b2f5-480c-b30e-304351e57fb4\"",
                "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules",
                "properties": {
                    "provisioningState": "Succeeded",
                    "description": "Deny all inbound traffic",
                    "protocol": "*",
                    "sourcePortRange": "*",
                    "destinationPortRange": "*",
                    "sourceAddressPrefix": "*",
                    "destinationAddressPrefix": "*",
                    "access": "Deny",
                    "priority": 65500,
                    "direction": "Inbound",
                    "sourcePortRanges": [],
                    "destinationPortRanges": [],
                    "sourceAddressPrefixes": [],
                    "destinationAddressPrefixes": []
                }
            },
            {
                "name": "AllowVnetOutBound",
                "id": "/subscriptions/e64b6c02-66fb-4acc-a0c0-68038660f611/resourceGroups/NSG-RG/providers/Microsoft.Network/networkSecurityGroups/webservers-nsg/defaultSecurityRules/AllowVnetOutBound",
                "etag": "W/\"ca8c6d0d-b2f5-480c-b30e-304351e57fb4\"",
                "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules",
                "properties": {
                    "provisioningState": "Succeeded",
                    "description": "Allow outbound traffic from all VMs to all VMs in VNET",
                    "protocol": "*",
                    "sourcePortRange": "*",
                    "destinationPortRange": "*",
                    "sourceAddressPrefix": "VirtualNetwork",
                    "destinationAddressPrefix": "VirtualNetwork",
                    "access": "Allow",
                    "priority": 65000,
                    "direction": "Outbound",
                    "sourcePortRanges": [],
                    "destinationPortRanges": [],
                    "sourceAddressPrefixes": [],
                    "destinationAddressPrefixes": []
                }
            },
            {
                "name": "AllowInternetOutBound",
                "id": "/subscriptions/e64b6c02-66fb-4acc-a0c0-68038660f611/resourceGroups/NSG-RG/providers/Microsoft.Network/networkSecurityGroups/webservers-nsg/defaultSecurityRules/AllowInternetOutBound",
                "etag": "W/\"ca8c6d0d-b2f5-480c-b30e-304351e57fb4\"",
                "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules",
                "properties": {
                    "provisioningState": "Succeeded",
                    "description": "Allow outbound traffic from all VMs to Internet",
                    "protocol": "*",
                    "sourcePortRange": "*",
                    "destinationPortRange": "*",
                    "sourceAddressPrefix": "*",
                    "destinationAddressPrefix": "Internet",
                    "access": "Allow",
                    "priority": 65001,
                    "direction": "Outbound",
                    "sourcePortRanges": [],
                    "destinationPortRanges": [],
                    "sourceAddressPrefixes": [],
                    "destinationAddressPrefixes": []
                }
            },
            {
                "name": "DenyAllOutBound",
                "id": "/subscriptions/e64b6c02-66fb-4acc-a0c0-68038660f611/resourceGroups/NSG-RG/providers/Microsoft.Network/networkSecurityGroups/webservers-nsg/defaultSecurityRules/DenyAllOutBound",
                "etag": "W/\"ca8c6d0d-b2f5-480c-b30e-304351e57fb4\"",
                "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules",
                "properties": {
                    "provisioningState": "Succeeded",
                    "description": "Deny all outbound traffic",
                    "protocol": "*",
                    "sourcePortRange": "*",
                    "destinationPortRange": "*",
                    "sourceAddressPrefix": "*",
                    "destinationAddressPrefix": "*",
                    "access": "Deny",
                    "priority": 65500,
                    "direction": "Outbound",
                    "sourcePortRanges": [],
                    "destinationPortRanges": [],
                    "sourceAddressPrefixes": [],
                    "destinationAddressPrefixes": []
                }
            }
        ]
    },
    "apiVersion": "2023-09-01"
}
```

Lets creata a VM,

![image](https://github.com/user-attachments/assets/708977af-b4c4-4d0d-a616-965d7bf5cdca)


Here comes the IMP part,

1. If we select None in NIC, we'll get VM created but no NIC associtate to NSG, we'll have to associtate NIC manually to the NSG.
   ![image](https://github.com/user-attachments/assets/2d4898ae-72db-4181-b1b1-eb6630ae8a1c)

2. Here, if we select the basic, we'll get new NSG created for out VM sith default NSG rules associated with our VM's NIC, and below that in inbound rule, you could see RGP port also can be selected in **basic** option
   ![image](https://github.com/user-attachments/assets/41ac0e77-869c-4f65-a2aa-b63d9ac09d2d)

3. And here, if selected Advanced we can associate NIC to an existing NSG also.

   ![image](https://github.com/user-attachments/assets/717af90b-ed5d-42d0-b170-422caa381813)

Lets select the existing NSGs craeted for the Lab and create+review.

We'll do this same configuration details for two more such VMs for our lab.

NOTE: Ensure use select details in **Network Interface** section 
ie, :
- Same Virtual Network(VNet) for all VMs, so that new Subnets under the same Vnet is allocated that is, next sets of IPs will be provided to use for resources
- NIC should be advances so that you can select the existing NSG.
- Here we are selecting the NSG created in different Resource Group so that we can later get the NIC's associated to the this existing NSG.
  
![image](https://github.com/user-attachments/assets/6222b6e2-557d-4aa7-9e99-19808b1e0e59)

![image](https://github.com/user-attachments/assets/b6842d26-df05-42f4-a55a-1619fd4d8339)

**Go and Hit Create:**

![image](https://github.com/user-attachments/assets/6a5f4bf0-c955-422b-ae32-cad0c8ed8c7d)

### DO the same for two others.

Here you can see along with VM creation we got,
NIC, and a Public IP created, 

The Vnet will be seen created for first VM, and for other 2 this same Vnet will be used (as mentioned in the NOTE.

Resource Created, lets do for others too.

Deployment 2 SS,
Here you could see that VNet is not created, that means it's using existing Vnet.
![image](https://github.com/user-attachments/assets/e0331077-2f7e-4f9f-82d3-a2d6e020c473)

in all the created VM you could se the IP allocated to he VM, its just next bit increamented for previous that is 10.0.0.5 which is next after 10.0.0.4 and this is due to same VNET we are using, lets GO! create other VMs and proceed.
![image](https://github.com/user-attachments/assets/6905b764-3eef-43a1-bb2e-7ee70be50f28)



![image](https://github.com/user-attachments/assets/7e209335-b672-4d0b-83a5-bfcf47be3141)

ROBOM:
NI details for 3rd Deployment:

![image](https://github.com/user-attachments/assets/55b5dae2-581c-4f99-9696-7c4e58ed36b7)


Here as well only NIC and Public IP is created along with the VM, COOL!
![image](https://github.com/user-attachments/assets/734b6907-af04-4bf9-87b1-437fd66dab84)


Lets refersh! and check the private IPs of each Vms.
Cool!

![image](https://github.com/user-attachments/assets/1dc72c6e-4c27-4f20-8c81-4b16fad83c00)

Lets click on Any VM, we'll see the same nsg that we selelcted at the time of creation of Vms.

![image](https://github.com/user-attachments/assets/2a9b6805-9169-410a-ba02-564e8570a24a)


And that all the NICs are associtated to this NSG, 

![image](https://github.com/user-attachments/assets/e31f8f84-2566-4309-a4b7-f17728edb32c)

![image](https://github.com/user-attachments/assets/1a57b782-1856-4547-ba37-5bbe085558cf)


## Head to the NSG and add a Inbound rule for RDP inbound access to port 3389 form any source and any destination.
Inbound Security rules -> Add rule
![image](https://github.com/user-attachments/assets/ec24038e-e74e-4815-bc31-f10979ff229c)

![image](https://github.com/user-attachments/assets/730edda4-f9f1-4d0b-baa6-f6d21ce8163b)

![image](https://github.com/user-attachments/assets/16a298e5-fc78-4c21-aeba-a1eb04077c56)

now RDP into one of there server hain do following chnags in server manager so that we can use Internet
![image](https://github.com/user-attachments/assets/2c18e012-f7c7-436b-9e5f-de023a9688c7)
lets access the internet.
![image](https://github.com/user-attachments/assets/df7364c0-f749-496e-8cae-e961fb2e62d2)

---

Second scenario, in OutBound rule, we are going to create a Deny Internet OutBound rule with lower Priority Number.
![image](https://github.com/user-attachments/assets/8e3753a4-a8c0-4fef-8396-67314c94876d)

and lets try to access the internet now.
![image](https://github.com/user-attachments/assets/c021288a-d30c-40e9-b43c-6d4c0a949b1f)


Rule created, and no internet

![image](https://github.com/user-attachments/assets/879d4b69-83df-44f2-a3e5-1d13d1100271)
![image](https://github.com/user-attachments/assets/3cbda83b-9217-419e-b809-7f1dddd1d149)

![image](https://github.com/user-attachments/assets/d92ae30f-50dc-4eba-b2df-0adff8a0de53)

Lets attache a NIC, and for that we need to craeta a NIC and before that also, we neeed to stop th OS, before attaching the NIC.
evenso when we tried to attach a NIC we got an error

![image](https://github.com/user-attachments/assets/903613b6-3b6a-43c5-930b-118b90f8c1df)
![image](https://github.com/user-attachments/assets/f937734b-8305-482a-84da-1705b6bf12f9)


The error is that we need to shut down the VM,
![image](https://github.com/user-attachments/assets/1077752b-9c11-49d2-9f33-26ca30cee557)

Now Stop from the servers also,
![image](https://github.com/user-attachments/assets/376d04f0-60f0-4256-a183-6dca8aa49d29)


Lets try to create a Network Interface now, 
![image](https://github.com/user-attachments/assets/35d29a9c-61cc-47e2-96ce-22e96c520fb7)
![image](https://github.com/user-attachments/assets/117be301-71ff-43af-aaeb-2c8b4d3fb54c)
and click create

now you can see our created NIC is also attached,
![image](https://github.com/user-attachments/assets/144f637b-b59a-44e8-863b-8a261d5b65e2)

lets start the VM and connect again to check the NIC
![image](https://github.com/user-attachments/assets/2e84786f-ae5e-49af-857d-785e319211bd)

![image](https://github.com/user-attachments/assets/382ebd91-6ba0-4c0a-9cff-60239caff267)
Now we can see that we have two NICs, 
![image](https://github.com/user-attachments/assets/d700a79f-28fe-4aad-a184-f913447564cd)

