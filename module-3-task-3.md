## Task 3: Create an NSX-T segment in the recovery site GROUP\#-AVS2-SDDC

In this task you will configure the recovery site GROUP\#-AVS2-SDDC with a
network segment for the VMs moved by SRM from the primary site. In this lab, we
focus on a basic scenario where the VMs protected by SRM do not need to retain
their IP address when moved to the recovery site. A DHCP service is used both in
the protected and in the recovery site to assign IP addresses to VMs when they
boot.

*This task requires a DHCP profile to be available in the recovery private
cloud. DHCP profiles have been configured in Module 1 for both GROUP\#-AVS1-SDDC
and GROUP\#-AVS2-SDDC. If you did not complete the corresponding steps in Module
1, please go back to it and configure DHCP profiles before proceeding.*

Log into NSX-T for the recovery site GROUP\#-AVS2-SDDC. Please note that,
because of the Global Reach connectivity that has been configured in Module 1
between the protected and the recovery private clouds, you can access vCenter
and NSX-T for both from the same jump-box.

Click on the **Network** menu item on the taskbar at the top of the window, select
**Segments** from the menu on the left and click the **ADD SEGMENT** button.

![Graphical user interface, website Description automatically
generated](media/49e2aea5074a27e19d5f8244b73bdf14.png)

In the segment configuration tile, enter the following settings:

-   Segment Name: **SRM-LAB-RECOVERY**

-   Connected gateway: Select the private cloud’s default Tier1 gateway

-   Transport Zone: Select the private cloud’s default overlay transport zone

-   Gateway CIDR IPv4: **10.\#.160.1/24** (please note that this IP subnet is not
    the same as the primary site’s)

![](media/1079bccfca90baf5c459fe5e28a2bc29.png)

Click on the **SET DHCP CONFIG** button and provide the following settings:

-   DHCP Type: **Gateway DHCP Server**

-   DHCP Profile: Select the profile created in Module 1

-   DHCP Config: Set the toggle to **Enabled**

-   DHCP Ranges: **10.\#.160.100-10.\#.160.120**

![](media/2c58686a0ee8dd395cbd66dd35545924.png)

When done, click on the **APPLY** button to close the DHCP Configuration window.
Then scroll down and click on the **SAVE** button to commit the segment
configuration.

![](media/d572a8a2d7a2879100971ce1e8b27b0b.png)

Confirm that the segment has been created successfully.

![](media/5f22e72b7e51403fbfaea81cf0aa0a07.png)

Optionally, you can confirm that the newly created segment is also visible in
the Azure portal (navigate to GROUP\#-AVS2-SDDC Private Cloud and select the
**Segments** item in the Workload Networking menu on the left-hand side.

![](media/da0bcd9932febb3eba083afac1db3712.png)

## Next Steps

[Module 3](module-3-task-4.md)

[Module 3 Index](module-3-index.md)

[Main Index](index.md)