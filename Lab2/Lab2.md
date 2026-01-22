# CST8921 Lab 2: Cloud Security
## Elizabeth Kaganovsky (040956095)
Note: The following explanations are somewhat verbose for the purpose of reinforcing my own knowledge through repetition. Also, my initial attempt at this lab did not succeed, so there may be some inconsistencies regarding naming of resources in the screenshots since some are reused to save me the effort of recreating them repeatedly.

### Task 1. Create an Azure Policy
Azure Policy is a tool used for setting internal rules on resource deployments to prevent resources from being created in prohibited regions or with disallowed configurations. Policies are subscription-wide and apply to all resources, including resource groups. When deploying a virtual machine, validation will fail after attempting to select an option which defies this policy.
![](/Lab2/Screenshots/Step_1_1.png)
![](/Lab2/Screenshots/Step_1_2.png)

### Task 2. Create a Virtual Network (Canada Central)
A virtual network is an essential component of cloud-based applications, facilitating secure communication between resources. Virtual networks can be partitioned into subnets and secured with network security groups. In this scenario the vnet is created but not split into subnets yet.
![](/Lab2/Screenshots/Step_2_1.png)
![](/Lab2/Screenshots/Step_2_2.png)

### Task 3. Create Subnets & Enable Storage Service Endpoint 
Subnets are used for isolating workloads into logically associated groupings for various purposes--precise traffic control, integration with specific Azure services that require subnet delegation, and strong security enforced through network security groups. Typically, services may have public endpoints where internet traffic can access the service. A service endpoint "wraps" a public endpoint and allows requests to travel over the Azure backbone network to the public endpoint for added security.

The storage service endpoint used here is a particular service intended to allow connectivity to storage accounts. Notably, service endpoints are free, while private endpoints are not.

![](/Lab2/Screenshots/Step_3_1.png)
![](/Lab2/Screenshots/Step_3_2.png)

### Task 4. Create Network Security Group (NSG)
Network security groups are groupings of security rules that can be applied to VNets, restricting traffic based on source/destination, protocol and ports. Network security groups can be associated to a subnet, applying their rules to it. Two network security groups are created here, one for private-subnet and one for public-subnet.
![](/Lab2/Screenshots/Step_4_1.png)

### Task 5. Configure NSG Rules (Private Subnet) 
The NSG for private-subnet is configured to allow outbound traffic with the service tag "Storage," meaning that outbound traffic is allowed if it comes from a designated storage-related service, and to disallow inbound traffic from the public internet. The latter rule is given higher priority, so if outbound traffic from a storage service attempts to access the greater internet, it is disallowed. However, outbound traffic from a storage service attempting to travel through the storage service endpoint across the Azure backbone network is allowed.
![](/Lab2/Screenshots/Step_5_1.png)
![](/Lab2/Screenshots/Step_5_2.png)

### Task 6. Configure NSG for Public Subnet (RDP Access)
A second NSG is created to allow incoming connections over RDP into public-subnet.

![](/Lab2/Screenshots/Step_6_1.png)

### Task 7. Create a Storage Account with File Share 
Storage accounts act like containers for various storage services, in this case for a file share. A file share is a specific service for storing data which can be directly mounted by an OS and treated as network attached storage (NAS) regardless of the file share's location. The storage account created in this step is configured to only allow access from private-subnet.

Notably, backups were disabled for the file share to ease the deletion process.

![](/Lab2/Screenshots/Step_7_1.png)
![](/Lab2/Screenshots/Step_7_2.png)
![](/Lab2/Screenshots/Step_7_3.png)

### Task 8. Deploy Virtual Machines 
Two virtual machines are deployed as testing tools for exploring the VNet's security features.

![](/Lab2/Screenshots/Step_8_5.png)
![](/Lab2/Screenshots/Step_8_6.png)

### Task 9. Test Storage Access from Private Subnet (Allowed) 
An issue arose here and I unfortunately could not manage this connection and I elected to skip this step to avoid accumulating any more charges on my Azure account. Theoretically, what should have happened here is the connection should have been allowed. 

The private subnet had an NSG (CST8921_Lab2_NSG_Private) applied that allowed outbound traffic from inside the network to exit the subnet as long as it was addressed to an Azure storage service, and disallowed outbound traffic to the internet. When the private VM CST8921-Lab2-private-VM was created, it should have been allowed to send the command to the storage service, but for whatever reason this did not go through.

### Task 10. Test Storage Access from Public Subnet (Denied) 
The VM on public-subnet (CST8921-Lab2-public-VM) was, as expected, unable to access the file share. This is due to the fact that CST8921-Lab2-public-VM does not have a service endpoint enabled for the storage account. The service endpoint created on private-subnet in task 5 is what allows CST8921-Lab2-private-VM to access and mount it as a drive.

![](/Lab2/Screenshots/Step_10_1.png)

### Task X. Cleanup
Notes on cleanup. Common mistakes are:
- Only using default settings when creating resources, leading to extra security protections preventing easy deletion.
- Using regional default resource groups, which cannot be delected.
- Failing to disassociate/delete resources in the proper order. Some resources have sub-resources that require deletion first--note that VMs should have the "Delete public IP and NIC when VM is deleted" setting activated to prevent orphaned resources.