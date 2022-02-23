## Task 2: Create a VM in the protected site

<span style="color:green">Remember X is your group number, Y is your participant number, Z is the SDDC you've been paired with.</span>

In this task you will create a test VM in the protected site.

*This task requires a VM template file to be available in the private cloud. A
template has been added to the private cloud’s Local Library in Module 1. If you
did not complete the corresponding steps in Module 1, please go back to it and
add a template to your protected site’s Local Library.*

Log into vCenter for the protected site GROUPX-AVS-SDDC. From the main menu
select **Content Libraries** and then click on **Local Library**. In the **Templates**
section, find the template **NetworkTest-VM**, right-click on it and select **New
VM from This Template** from the context menu.

![](media/e0eed977a780948438f1feabdadca181.png)

Follow the steps in the VM configuration wizard. First, set the VM name to **G-XY-SRM-VM1** and select the location **SDDC-Datacenter**.

![](media/af10b25e4315bbae52b4356e3b088d80.png)

Then, go through the **Review Details** step (no configuration is required here)
and, in the **Select storage** step, select **vSAN Default Storage Policy**.

![](media/fc5cc689dc8c6093f53c50f12c5f733a.png)

Finally, attach the VM to the network segment created in Task1, by selecting
**SRM-LAB-GROUP-XY** in the **Destination Network** drop-down menu. Deploy the VM by clicking on the **Finish** button.

![](media/bc719a8326876c91827c186e7b47183b.png)

In the main vCenter menu, select **VMs and Templates** and then click on the newly
created VM **GXY-SRM-VM1**. Power it on by clicking on the green **Power On** icon.

![](media/b354049252367e3210c7680337af984f.png)

When the VM starts, check that it has been assigned an IP address in the DHCP
range configured in Task 1.

![](media/96f56838bed0f88643da6f8f3a9770d1.png)

Test your network configuration by pinging the VM from the jump-box you are
working on.

![](media/e61ddb7e9c1c22afca8eacc835eba309.png)

## Next Steps

[Module 3, , Task 3](module-3-task-3.md)

[Module 3 Index](module-3-index.md)

[Main Index](index.md)