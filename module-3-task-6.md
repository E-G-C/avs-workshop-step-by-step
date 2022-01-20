# Task 6: Configure vSphere Replication and Recovery Plan

In this task you will configure vSphere replication for the test VM created in
Task 2 and a recovery plan to protect it. This task is performed from the
primary site’s vCenter client. In the main menu, select **VM and Templates** and
then right-click on your test VM named GX-SRM-VM1. From the context menu, select
**All Site Recovery Actions** and then **Configure replication**.

>*Note: Check pop-up blocker if stuck.*

![](media/1044498d505fba36f9621e504fef8401.png)

## vSphere Replication

![](media/4178918f64a3ec52800aa8b91985bda8.png)

Follow the steps in the configuration wizard. Select the recovery site (FDQN
ending with the suffix **southcentralus.avs.azure.com**) as the target site.
Provide credentials for the recovery site’s vCenter. The credentials are
available in the Azure portal. Select **Auto-assign replication server**.

![](media/921e6c47831001cec93fa0b1cb0cbb2b.png)

Check that the test VM is ready for replication, then click on the **NEXT** button
and select **vSAN Datastore** as the target datastore. In the **Replication
Settings** step, select the RPO you want to have for the protected VM (15 mins in
the screenshot below).

![](media/ed04edab49abb4c8ebf49ec2440e7745.png)

## SRM Protection Group and Recovery Plan

The last two steps in the configuration wizard allow you to create an SRM
Protection Group and a Recovery Plan. Please note that this is needed because
you are configuring SRM protection for the first VM. Additional VMs can leverage
existing protection groups and recovery plans. In step 5 **Protection Group**
enter a name for your protection group, such as **SRM-LAB-PROTECTION-GROUP**. In
step 6 **Recovery Plan** enter a name for your recovery plan, such as
**SRM-LAB-REC-PLAN**. Confirm your settings by clicking on the green **FINISH**
button.![Graphical user interface, table Description automatically generated
with medium confidence](media/456e8f584cc78a9b7a95f1963c641cd6.png)

Wait until the replication status for your test VM is reported to be **OK** (use
the **Refresh** button in SRM’s console).

![](media/29a104a28bda920bc3bdb24cfd2a6d6d.png)

To confirm that replication and SRM protection have been successfully
configured, log into the recovery site’s vCenter and check that a placeholder VM
has been created.

![](media/589542c3eaf085fcca44f07bd46d2979.png)

## Next Steps

[Module 3, Task 7](module-3-task-7.md)

[Module 3 Index](module-3-index.md)

[Main Index](index.md)