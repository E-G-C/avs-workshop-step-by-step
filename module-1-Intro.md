## Introduction

Azure VMware Solution offers a private cloud environment accessible from
On-Premises and Azure-based resources. Services such as Azure ExpressRoute, VPN
connections, or Azure Virtual WAN deliver the connectivity.

## Scenario

Customer needs to have connectivity between their workloads in AVS, existing services and workloads in
Azure, and access to the internet.

![](media/457693efe56f5acc79bd76ef52f829ee.png)

## Agenda for next 60 mins:

This hands-on lab will show you how to configure the Networking components of an
Azure VMware Solution for:

-   Connecting Azure VNet’s to AVS over an ExpressRoute circuit

-   Peering with remote environments using Global Reach

-   Configuring NSX-T (check DNS and configure DHCP, Segments, and Gateway) to
    manage connectivity within AVS

| **Action Plan**                                         | **Expected Time**      |
|---------------------------------------------------------|------------------------|
| Create AVS environment                                  | Preconfigured          |
| [Connect to Azure Virtual Networks](#_Task_1:_Connect)  | 10 mins                |
| [Connect to On-Premises Environments](#_Task_2:_Peer)   | 10 mins                |
| Configure DNS                                           | Preconfigured – 2 mins |
| Configure DHCP                                          | 5 mins                 |
| Configure Tier-1 Gateway                                | Preconfigured - 2 mins |
| [Configure network Segments](#_Step_4:_Create)          | 5 mins                 |

The lab environment has a preconfigured VMware in Azure environment with an
Express Route circuit. An additional VMware on Azure is configured to simulate
an On-Premises environment. Both environments are accessible through Bastions
and JumpBoxes.

After this lab is complete, you will have built out this scenario below

1.  ExpressRoute, or SD-WAN for connectivity between Azure VMware Solution

2.  Connectivity to remote environments using Global Reach

3.  Configure NSX-T to establish connectivity within the AVS environment

\*For this lab, a secondary AVS environment is provided to simulate a datacenter
or co-location. In real world scenarios, using Global Reach facilitates
connectivity between AVS and On-Premises environments

## Next Steps

[Task 1](module-1-task-1)

[Module 1 Index](module-1-index)

[Main Index](index)