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

there no resource two which its is associtated with
![image](https://github.com/user-attachments/assets/08d87750-3a21-4944-b114-af07f0f18fa5)

 
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

   
