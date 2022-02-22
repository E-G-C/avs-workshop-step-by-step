# Task 5: Configure Inventory Mappings

<span style="color:green">Remember X is your group number, Y is your participant number, Z is the SDDC you've been paired with.</span>

In this task you will configure inventory mappings, which define the resources
(networks, folders, compute resources, storage policies) that VMs must use when
moved to the recovery site. It is also possible to define reverse mappings,
which control resource allocation for failback processes.

## Network mappings

Open the **Site Pair** configuration pane in SRM and select **Network Mappings** in
the **Configure** section of the left-hand-side menu. Then click on the **NEW**
button to launch the configuration wizard.

![](media/850e44547c85fe48a4151e6fd7eed8b2.png)

Select **Prepare mappings manually** to define a custom mapping between the
network segments created for the SRM lab module in the previous tasks. Then
click on the **NEXT** button and map the **SRM-LAB-GROUP-XY** segment in the protected site
to the **SRM-LAB-RECOVERY-GROUP-XY** segment in the recovery site. Click on the **ADD
MAPPINGS** button to confirm.

![](media/2efdf93a054c742f7bb646c4dc6c6223.png)

In the **Reverse Mapping** step, enable the suggested reverse mapping.

![](media/27d7d8cde06f10747292ad75184dabc6.png)

In **Test Networks** step, accept the default setting. When later in the module
you will test your recovery plan, the protected VM will be instantiated in an
isolated network segment automatically created at the beginning of the test (and
automatically removed when the recovery plan test is cleaned up).

![](media/562687484b97b3263514f43493700ca6.png)

Click on the **NEXT** button and then commit your configuration by clicking on the
green **FINISH** button.

## Folder Mappings

Open the **Site Pair** configuration pane in SRM and select **Folder Mappings** in
the **Configure** section of the left-hand-side menu. Then click on the **NEW**
button to launch the configuration wizard.

![](media/59f2f3e76565bba79fe9fd9e27fe6f1e.png)

Select **Automatically prepare mappings for folders with the same name**, then
click on the **NEXT** button. Select **SDDC-Datacenter** on both sides of the
mapping and click on the **ADD MAPPINGS** button. Accept the automatically
prepared mappings.

![](media/9ced3b0f8b626c61b50364d9c5090d2d.png)

On step 3 **Reverse Mappings** accept the mappings proposed by the wizard. Then
click on the **NEXT** button and commit your configuration by clicking on the
green **FINISH** button.

![](media/b7930ecbdb992b6419aed0426908309a.png)

## Resource Mappings

Open the **Site Pair** configuration pane in SRM and select **Resource Mappings** in
the **Configure** section of the left-hand-side menu. Then click on the **NEW**
button to launch the configuration wizard.

![](media/420dd1c3327bb44786d1e4e4fe872f50.png)

On step 1 **Recovery Resources** expand the **SDDC-Datacenter** nodes on both the
primary and the recovery side and select **Cluster 1**. Click on the **ADD
MAPPINGS** button to confirm.

![](media/25fe495c757206ea9717e6f9a1320278.png)

Accept the reverse mapping proposed by the wizard, click on the **NEXT** button
and then confirm your settings by clicking on the green **FINISH** button.

![](media/0cb1fd060fb96745f45992f0779d169f.png)

## Storage Policy Mappings

Open the **Site Pair** configuration pane in SRM and select **Storage Policy
Mappings** in the **Configure** section of the left-hand-side menu. Then click on
the **NEW** button to launch the configuration wizard.

![](media/0eb20eaf58bbcf7f4f03b2c295c81c24.png)

Select **Automatically prepare mappings for storage policies with the same name**,
then click on the **NEXT** button. Select **vSAN Default Storage Policy** on both
sides of the mapping and click on the **ADD MAPPINGS** button. Accept the
automatically prepared mappings. Accept the automatically discovered mappings.

![](media/db8788f38475d84d72ee8b6e572f406e.png)

Accept the reverse mapping proposed by the wizard, click on the **NEXT** button
and then confirm your settings by clicking on the green **FINISH** button.

![](media/e80c270f4536be4eba1b004b39448cd9.png)

## Placeholder Datastores

When vSphere Replication is configured for a VM, a **placeholder VM** is created
in the target recovery site. Placeholder VMs represent, in the recovery site,
VMs that will be instantiated when a recovery plan is run. SRM requires you to
define which datastore to use for placeholder VMs. If you plan to use SRM for
failback, you need to define placeholder datastores at both the protected and
the recovery sites.

Open the **Site Pair** configuration pane in SRM and select **Placeholder
Datastores** in the **Configure** section of the left-hand-side menu. In the
**Placeholder Datastores** configuration tile, select your primary site’s vCenter
server (its FQDN ends with the suffix ****eastus2**.avs.azure.com**).

![](media/01f786a9886c37613a38e504d25f26a4.png)

Click on the **NEW** button to add a datastore. Select **vSAN Datastore** and click
on the **ADD** button.

![](media/f633376f0777f39351ce0507d6d1638f.png)

Repeat the same steps for the recovery site’s vCenter (its FQDN ends with the
suffix ****brazilsouth**.avs.azure.com**).

![](media/4cbe92d7e370b175e72f8c8ce9e0a458.png)

Click on the **NEW** button to add a datastore. Select **vSAN Datastore** and click
on the **ADD** button.

![](media/37cf2222e43de01f9dfdc16a68b122a3.png)

## Next Steps

[Module 3, Task 6](module-3-task-6.md)

[Module 3 Index](module-3-index.md)

[Main Index](index.md)