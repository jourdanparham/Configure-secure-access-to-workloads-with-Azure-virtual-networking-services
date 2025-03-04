---
lab:
    title: 'Exercise: Protect the web application from malicious traffic and block unauthorized access'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---

# Lab: Protect the web application from malicious traffic and block unauthorized access


## Scenario
Your organization is looking to protect the web application from malicious traffic and block unauthorized access.

In addition to NSG and ASG, a firewall can be configured to add an extra layer of security to the web application. A firewall protects the web application from malicious traffic and blocks unauthorized access with policies you configure. Network Traffic is subject to the firewall rules when you route your network traffic to the firewalll as the subnet default gateway. 


### Architecture diagram

![Diagram that shows one virtual network with a firewall and route table.](../Media/task-3.png)

### Skilling tasks
- Create an Azure Firewall.
- Create and configure a firewall policy.
- Create and configure a route table.
- Link a route table to a subnet.


## Exercise instructions

1.  Create a subnet named **AzureFirewallSubnet** in the **app-vnet** virtual network by using a subnet address range of **10.1.63.0/24**.

1.  Create a firewall by using the values in the following table. For any property that is not specified, use the default value.

    | Property | Value    |
    |:---------|:---------|
    |Resource group   | **RG1**  |
    |Name	   | **app-vnet-firewall**|
    |Firewall SKU |	Standard|
    |Firewall management | Use a Firewall Policy to manage this firewall|
    |Firewall policy| select **Add new**| 
    |Policy name| **fw-policy**|
    |Region| **East US**|
    |Policy Tier| **Standard**|
    |Choose a virtual network |	Use existing|
    |Virtual network | **app-vnet** (RG1)|
    |Public IP address | Add new: **fwpip**|

    [Learn more on creating a firewall](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal), [creating route tables](https://docs.microsoft.com/azure/virtual-network/manage-route-table) and [associating a route table to a subnet](https://docs.microsoft.com/azure/virtual-network/tutorial-create-route-table-portal#associate-a-route-table-to-a-subnet).

1. Record the private and public IP address of **app-vnet-firewall**.

1. Create a route table named **app-vnet-firewall-rt** in the **RG1** resource group by using the East US region.

1. Associate the **app-vnet-firewall-rt** route table to the **frontend** and **backend** subnets in **app-vnet**. 

1. Create a route in the **app-vnet-firewall-rt** named **outbound-firewall** with address prefix **0.0.0.0/0** and **Next hop type**  **Virtual Appliance**. Use the private IP address of the firewall for the **Next hop address**. [Learn more on creating route tables](https://docs.microsoft.com/azure/virtual-network/manage-route-table) and [associating a route table to a subnet](https://docs.microsoft.com/azure/virtual-network/tutorial-create-route-table-portal#associate-a-route-table-to-a-subnet).


Now the outbound traffic from the front end and backend subnet will route to the firewall. 
