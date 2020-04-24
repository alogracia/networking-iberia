# Overview

### Considerations

When building a multi-VPC and/or multi-account architecture, there are several services that we need to consider to provide seamless integration between our AWS environment and the existing infrastrucuture in our datacenter.
Foundationally we need to provide robust connectivity and routing between the datacenter and all the VPCs but we also need to provide and control routing between those VPCs. For example, we may have a 'Shared Services' VPC that every other VPC needs access to and in which we place common resources that everyone needs, such as a NAT Gateway service to access the internet. At the same time, we don't want just any VPC talking to any other VPC. In particular, we don't want our 'Non-Production' VPCs talking to our 'Production' VPCs.

### Connectivity

In the past, customers used third-party solutions and/or transit VPCs that they built and managed on their own. In order to remove much of that undifferentiated heavy lifting, we will use the **AWS Transit Gateway** Service to provide this connectivity and routing. **AWS Transit Gateway** is a service that enables customers to connect their Amazon Virtual Private Clouds (VPCs) and their on-premise networks to a highly-available gateway. **AWS Transit Gateway** provides easier connectivity, better visibility, more control and on-demand bandwidth.

### DNS Resolution

After we have established connectivity and routing, we need to provide seamless DNS resolution between our Datacenter and the VPCs. Our on-prem devices will want to reach our resources in the cloud using DNS names, not IP addresses, and the resources in the cloud will want to do the same for the servers back in our datacenter. To accomplish this we will use **Amazon Route53 Resolver**. **Amazon Route53 Resolver** for hybrid clouds allows us to create highly available endpoints in our VPCs to integrate with the Amazon-provided DNS (sometimes referred to as the .2 resolver, since it is always 2 addresses up from the VPC CIDR block, i.e. 172.16.0.2 for VPC CIDR 172.16.0.0/24).
