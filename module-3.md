
# Module 3: Setup SRM for Disaster Recovery

## Introduction

This module walks through the implementation of a disaster recovery solution for
Azure VMware Solution (AVS), based on VMware Site Recovery Manager (SRM). The
module can be completed in 60 minutes, as per the agenda below.

|    | **Action Plan**                                             | **Installation time** | **Time required for each step** |
|----|-------------------------------------------------------------|-----------------------|---------------------------------|
| 1  | Introduction and Session Walkthrough                        | NA                    | 5 mins                          |
| 2  | Cover SRM concepts for lab                                  | NA                    | 5 mins                          |
| 3  | Enable SRM Addon for both AVS clouds (primary and recovery) | 15-30 mins            | Preconfigured                   |
| 4  | Install the vSphere replication appliance                   | 15 mins               | Preconfigured                   |
| 5  | Configure protected site                                    |                       | 10 mins                         |
| 6  | Create a test VM to be replicated                           |                       | 5 mins                          |
| 7  | Configure recovery site                                     |                       | 5 mins                          |
| 8  | Configure site pairing                                      |                       | 20 mins                         |
| 9  | Configure inventory mappings                                |                       |                                 |
| 10 | Create Recovery Plan                                        |                       |                                 |
| 11 | Test Recovery Plan and Clean-up                             |                       |                                 |
| 12 | For Failover - Run Recovery Plan                            |                       |                                 |
| 13 | Enable Re-Protection                                        |                       |                                 |
| 14 | Failback                                                    |                       |                                 |
| 15 | Q/A                                                         |                       | 10 mins                         |
|    | Total                                                       | 60 mins               |                                 |

### What you will learn

In this module, you will learn how to:

-   Install Site Recovery Manager in an AVS Private Cloud

-   Create a site pairing between two AVS Private Clouds in different Azure
    regions

-   Configure replications for AVS Virtual Machines

-   Configure SRM protection groups and recovery plans

-   Test and execute recovery plans

-   Re-protect recovered Virtual Machines and execute fail back

### Prerequisite knowledge

-   AVS Private Cloud administration (Azure Portal)

-   AVS network architecture, including connectivity across private clouds in
    different regions based on Azure ExpressRoute Global Reach

-   Familiarity with disaster recovery DR concepts such as RPO and RTO

-   Basic concepts of Site Recovery Manager and vSphere Replication, covered in
    the next two sections

### Module scenario

In this module, two AVS Private Clouds are used. VMWare Site Recovery Manager
will be configured at both sites to replicate VMs in the protected site to the
recovery site.

| Private Cloud Name | Location         | Role               |
|--------------------|------------------|--------------------|
| GROUP\#-AVS1-SDDC  | East US 2        | **Protected** Site |
| GROUP\#-AVS2-SDDC  | South Central US | **Recovery** Site  |

**The two private clouds have been already interconnected with each other in
Module 1, using ExpressRoute Global Reach. The diagram below depicts the
topology of the lab environment**.

![](media/285abcfd08e365730976517140c3e2be.png)

### Site Recovery Manager

VMware Site Recovery Manager is a business continuity and disaster recovery
solution that helps you plan, test, and run the recovery of virtual machines
between a protected vCenter Server site and a recovery vCenter Server site. You
can use Site Recovery Manager to implement different types of recovery from the
protected site to the recovery site:

-   **Planned migration**: The orderly evacuation of virtual machines from the
    protected site to the recovery site. Planned migration prevents data loss
    when migrating workloads in an orderly fashion. For planned migration to
    succeed, both sites must be running and fully functioning.

-   **Disaster recovery**: Similar to planned migration except that disaster
    recovery does not require that both sites be up and running, for example if
    the protected site goes offline unexpectedly. During a disaster recovery
    operation, failure of operations on the protected site is reported but is
    otherwise ignored.

Site Recovery Manager **orchestrates the recovery process with VM replication
between the protected and the recovery site**, to minimize data loss and system
down time. At the protected site, Site Recovery Manager shuts down virtual
machines cleanly and synchronizes storage, if the protected site is still
running. Site Recovery Manager powers on the replicated virtual machines at the
recovery site according to a recovery plan. A recovery plan specifies the order
in which virtual machines start up on the recovery site. A recovery plan
specifies network parameters, such as IP addresses, and can contain
user-specified scripts that Site Recovery Manager can run to perform custom
recovery actions on virtual machines.

Site Recovery Manager lets you **test recovery plans**. You conduct tests by
using a temporary copy of the replicated data in a way that does not disrupt
ongoing operations at either site.

Site Recovery Manager supports both hybrid (protected site on-prem, recovery
site on AVS) and cloud-to-cloud scenarios (protected and recovery sites on AVS,
in different Azure regions). This lab covers the cloud-to-cloud scenario only.

Site Recovery Manager is installed by deploying the **Site Recovery Manager
Virtual Appliance** on an ESXi host in a vSphere environment. The Site Recovery
Manager Virtual Appliance is a preconfigured virtual machine that is optimized
for running Site Recovery Manager and its associated services. After you deploy
and configure Site Recovery Manager instances on both sites, the Site Recovery
Manager plug-in appears in the vSphere Web Client or the vSphere Client. The
figure below shows the high-level architecture for a SRM site pair.

![](media/eb6490e5af96d0baf0e7b0971e1e3025.png)

### vSphere replication

SRM can work with multiple replication technologies: Array-based replication,
vSphere (aka host-based) replication, vVols replication and a combination of
array-based and vSphere replication ([learn
more](https://docs.vmware.com/en/Site-Recovery-Manager/8.3/com.vmware.srm.admin.doc/GUID-35BBE965-ADC3-4E6E-A094-3D0037DA8528.html)).
AVS Private Clouds run on hyperconverged physical infrastructure powered by
VMWare’s first-party storage virtualization software, vSAN. As such, **the only
replication technology that can be used with SRM in AVS is vSphere replication,
which does not require storage arrays**. With vSphere replication, the storage
source and target can be any storage device. vSphere Replication is configured
on a per-VM basis, allowing you to control which VMs are duplicated.

![](media/4390100ec5e84088fcdaad8dce762258.png)

vSphere Replication requires a virtual appliance to be deployed from an Open
Virtualization Format (OVF) file using the vSphere Web Client. The first virtual
appliance deployed at each site is referred to as the **vSphere Replication
management server**. It contains the necessary components to receive replicated
data, manage authentication, maintain mappings between the source virtual
machines and the replicas at the target location and provide support for Site
Recovery Manager. Additional vSphere Replication appliances can be deployed to
support larger-scale deployments and topologies with multiple target locations.
These additional virtual appliances are referred to as **vSphere Replication
servers**.

The components that transmit replicated data (the **vSphere Replication agent**
and a **vSCSI filter**) are built into vSphere. They provide the plug-in
interfaces for configuring and managing replication, track the changes to VMDKs,
automatically schedule replication to achieve the RPO for each protected virtual
machine, and transmit the changed data to one or more vSphere Replication
virtual appliances. There is no need to install or configure these components,
further simplifying vSphere Replication deployment.

When the target is a vCenter Server environment, data is transmitted from the
source vSphere host to either a vSphere Replication management server or vSphere
Replication server and is written to storage at the target location.

![](media/d95f6098d2f1f96765ebd76e5d24fab7.png)

vSphere Replication begins the initial full synchronization of the source
virtual machine to the target location, using TCP port 31031. A copy of the
VMDKs to be replicated can be created and shipped to the target location and
used as **seeds,** reducing the time and network throughput. Changes to the
protected virtual machine are tracked and replicated on a regular basis. The
transmissions of these changes are referred to as **lightweight delta syncs.**
Their frequency is determined by the RPO that was configured for the virtual
machine. A lower RPO requires more-frequent replication and network bandwidth
consumed by the initial full synchronization.

The replication stream can be encrypted. As data is being replicated, the
changes are first written to a file called a redo log, which is separate from
the base disk. After all changes for the current replication cycle have been
received and written to the redo log, the data in the redo log is consolidated
into the base disk. This process helps ensure the consistency of each base disk
so virtual machines can be recovered at any time, even if replication is in
progress or network connectivity is lost during transmission.

### Site Recovery Concepts

-   **Inventory Mappings.** For array-based protection and vSphere Replication
    protection, Site Recovery Manager applies inventory mappings to all virtual
    machines in a protection group when you create that group. Inventory
    mappings provide default objects in the inventory on the recovery site for
    the recovered virtual machines to use when you run recovery. Site Recovery
    Manager cannot protect a virtual machine unless it has valid inventory
    mappings. However, configuring site-wide inventory mappings is not mandatory
    for array-based replication protection groups and vSphere Replication
    protection groups. If you create vSphere Replication protection group
    without having defined site-wide inventory mappings, you can configure each
    virtual machine in the group individually. You can override site-wide
    inventory mappings by configuring the protection of the virtual machines in
    a protection group. You can also create site-wide inventory mappings after
    you create a protection group, and then apply those site-wide mappings to
    that protection group.

-   **Protection Groups**. A protection group is a collection of virtual
    machines that Site Recovery Manager protects together. After you create a
    vSphere Replication protection group, Site Recovery Manager creates
    placeholder virtual machines on the recovery site and applies the inventory
    mappings to each virtual machine in the group. If Site Recovery Manager
    cannot map a virtual machine to a folder, network, or resource pool on the
    recovery site, Site Recovery Manager sets the virtual machine to the Mapping
    Missing status, and does not create a placeholder for it

-   **Recovery Plan.** A recovery plan is like an automated run book. It
    controls every step of the recovery process, including the order in which
    Site Recovery Manager powers on and powers off virtual machines, the network
    addresses that recovered virtual machines use, and so on. Recovery plans are
    flexible and customizable. A recovery plan includes one or more protection
    groups. You can include a protection group in more than one recovery plan.
    For example, you can create one recovery plan to handle a planned migration
    of services from the protected site to the recovery site for the whole
    organization, and another set of plans per individual departments. **You can
    run only one recovery plan at a time to recover a particular protection
    group.**

-   **Reprotection.** After a recovery, the recovery site becomes the primary
    site, but the virtual machines are not protected yet. If the original
    protected site is operational, you can reverse the direction of protection
    to use the original protected site as a new recovery site to protect the new
    protected site. Manually re-establishing protection in the opposite
    direction by recreating all protection groups and recovery plans is time
    consuming and prone to errors. **Site Recovery Manager provides the
    reprotect function, which is an automated way to reverse protection.**
    Reprotect uses the protection information that you established before a
    recovery to reverse the direction of protection. You can initiate the
    reprotect process only after recovery finishes without any errors. You can
    conduct tests after a reprotect operation completes, to confirm that the new
    configuration of the protected and recovery sites is valid.


## **Task 0 (preconfigured): Install SRM add-on in the protected and the recovery sites**

**In the lab environment, this task has been already completed**, as it can take
up to 30 minutes to complete.

In the Azure portal, browse to the primary AVS Private Cloud
(GROUP\#-AVS1-SDDC), select the **Add-ons** item from the menu and the click on
the **Get Started** button in the **Disaster Recovery** tile.

![](media/9ed4b5667c42384d2105f50d61508087.png)

Verify that SRM and vSphere replication are already installed (**BOTH** buttons
read **Uninstall…**).

![](media/85da7c550ec14ea7f3c734a60cc95294.png)

## **Task 1**: Configure the production site (GROUP\#-AVS1-SDDC)

In this task you will create a network segment in the production site and deploy
a test VM to be protected with Site Recovery Manager.

*This task requires a DHCP profile to be available in the private cloud. DHCP
profiles have been configured in Module 1 for both GROUP\#-AVS1-SDDC and
GROUP\#-AVS2-SDDC. If you did not complete the corresponding steps in Module 1,
please go back to it and configure DHCP profiles before proceeding.*

Log into NSX-T client for the protected/primary site GROUP\#-AVS1-SDDC. Click on
the **Segments** item in the left-hand menu and then click the **ADD SEGMENT**
button in the main tile. Enter the following configuration settings:

-   Segment Name: **SRM-LAB**

-   Connected gateway: Select the private cloud’s default Tier1 gateway

-   Transport Zone: Select the private cloud’s default **overlay** transport
    zone

-   Gateway CIDR IPv4: **10.\#.60.1/24**

![](media/367712fc63544d3aac43e67cd75c5220.png)

Click on the **SET DHCP CONFIG** button and provide the following settings:

-   DHCP Type: **Gateway DHCP Server**

-   DHCP Profile: Select the profile created in Module 1

-   DHCP Config: Set the toggle to **Enabled**

-   DHCP Ranges: **10.\#.60.100-10.\#.60.120**

![](media/3fc2f1868be7edaa9625e29e5b5efe32.png)

When done, click on the **APPLY** button to close the DHCP Configuration window.
Then scroll down and click on the **SAVE** button to commit the segment
configuration.

![Graphical user interface, text, application, email, website Description
automatically generated](media/27e39ac4a19c0d7b2200f30f7b9f0605.png)

Click **NO** to close the configuration window. Confirm the segment is
successfully configured by checking that it appears in the segments list.

![A computer screen capture Description automatically generated with medium
confidence](media/cee6bdc13e1efc967011ebbe78b0a1f8.png)

Optionally, you can confirm that the newly created segment is also visible in
the Azure portal. It may take up to 2-3 mins to show up in the portal.

Navigate to GROUP\#-AVS1-SDDC AVS Private Cloud and select the **Segments** item
in the Workload Networking menu on the left-hand side.

![](media/c44d19dd3dac0b8ba66c71197309b9a6.png)

## Task 2: Create a VM in the protected site

In this task you will create a test VM in the protected site.

*This task requires a VM template file to be available in the private cloud. A
template has been added to the private cloud’s Local Library in Module 1. If you
did not complete the corresponding steps in Module 1, please go back to it and
add a template to your protected site’s Local Library.*

Log into vCenter for the protected site GROUP\#-AVS1-SDDC. From the main menu
select **Content Libraries** and then click on **Local Library**. In the **Templates**
section, find the template **NetworkTest-VM**, right-click on it and select **New
VM from This Template** from the context menu.

![](media/e0eed977a780948438f1feabdadca181.png)

Follow the steps in the VM configuration wizard. First, set the VM name to **GX-SRM-VM1** and select the location **SDDC-Datacenter**.

![](media/af10b25e4315bbae52b4356e3b088d80.png)

Then, go through the **Review Details** step (no configuration is required here)
and, in the **Select storage** step, select **vSAN Default Storage Policy**.

![](media/fc5cc689dc8c6093f53c50f12c5f733a.png)

Finally, attach the VM to the network segment created in Task1, by selecting
**SRM-LAB** in the **Destination Network** drop-down menu. Deploy the VM by clicking on the **Finish** button.

![](media/bc719a8326876c91827c186e7b47183b.png)

In the main vCenter menu, select **VMs and Templates** and then click on the newly
created VM **GX-SRM-VM1**. Power it on by clicking on the green **Power On** icon.

![](media/b354049252367e3210c7680337af984f.png)

When the VM starts, check that it has been assigned an IP address in the DHCP
range configured in Task 1.

![](media/96f56838bed0f88643da6f8f3a9770d1.png)

Test your network configuration by pinging the VM from the jump-box you are
working on.

![](media/e61ddb7e9c1c22afca8eacc835eba309.png)

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

## Task 4: Configure a Site Pairing in Site Recovery Manager

In this task you will pair the protected site GROUP\#-AVS1-SDDC and the recovery
site GROUP\#-AVS2-SDDC.

Site pairing can be configured from vCenter on either the primary or the
recovery private cloud. You will work on the primary site’s vCenter. If needed,
log into vCenter in the primary AVS private cloud GROUP\#-AVS1-SDDC and select
**Site Recovery** from the main menu. Click on the **OPEN Site Recovery** button.

![](media/31c387a424cd9ac00e00f5b1f46ec7d5.png)

Site Recovery Manager opens in a new browser tab.

>**Note: Web page may perpetually get stuck into loading status. In this case, go
back to main page and click **Open Site Recovery** button again.**

Click on the **NEW SITE PAIR** button to launch the configuration wizard.

![](media/2846f78785bf7bc7f6b5a4906ef0b335.png)

Select the local vCenter server that you want to pair. The only option is the
protected site’s vCenter (GROUP\#-AVS1-SDDC). Provide the IP address and the
credentials of the recovery site’s vCenter (GROUP\#-AVS2-SDDC), which can be
obtained from the Azure portal. Ensure that you remove *https and/or any
slashes* after pasting the vCenter value.

![](media/47c5c80246569ab43d588f1d041e256f.png)

Click on the **NEXT** button. The security alert(s) that you receive are due to
the usage of certificates issued by an untrusted CA in the lab. In real,
production environments certificates issued by a trusted CA should be used
instead. In this lab, you can ignore the security warning and click on the
**CONNECT** button.

![](media/7fd8b7be48eb293420088b5ce16b654a.png)

Configure the site pairing with both the SRM and the vSphere replication
services. Again, you can ignore the security warnings due to untrusted
certificates and proceed by clicking on the **CONNECT** button.

![](media/157d9ea5d2c9d933aebb494ee08af686.png)

When the configuration process completes, the SRM main page displays the new
site pairing.

![](media/a78bc6bd597184e555fa5572994e75a7.png)

## Task 5: Configure Inventory Mappings

In this task you will configure inventory mappings, which define the resources
(networks, folders, compute resources, storage policies) that VMs must use when
moved to the recovery site. It is also possible to define reverse mappings,
which control resource allocation for failback processes.

### Network mappings

Open the **Site Pair** configuration pane in SRM and select **Network Mappings** in
the **Configure** section of the left-hand-side menu. Then click on the **NEW**
button to launch the configuration wizard.

![](media/850e44547c85fe48a4151e6fd7eed8b2.png)

Select **Prepare mappings manually** to define a custom mapping between the
network segments created for the SRM lab module in the previous tasks. Then
click on the **NEXT** button and map the **SRM-LAB** segment in the protected site
to the **SRM-LAB-RECOVERY** segment in the recovery site. Click on the **ADD
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

### Folder Mappings

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

### Resource Mappings

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

### Storage Policy Mappings

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

### Placeholder Datastores

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
suffix ****southcentralus**.avs.azure.com**).

![](media/4cbe92d7e370b175e72f8c8ce9e0a458.png)

Click on the **NEW** button to add a datastore. Select **vSAN Datastore** and click
on the **ADD** button.

![](media/37cf2222e43de01f9dfdc16a68b122a3.png)

## Task 6: Configure vSphere Replication and Recovery Plan

In this task you will configure vSphere replication for the test VM created in
Task 2 and a recovery plan to protect it. This task is performed from the
primary site’s vCenter client. In the main menu, select **VM and Templates** and
then right-click on your test VM named GX-SRM-VM1. From the context menu, select
**All Site Recovery Actions** and then **Configure replication**.

>*Note: Check pop-up blocker if stuck.*

![](media/1044498d505fba36f9621e504fef8401.png)

### vSphere Replication

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

### SRM Protection Group and Recovery Plan

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

## Task 7: Test Recovery Plan

In this task you will test the recovery plan created in the previous one.

In the protected site’s SRM console, select the **Recovery Plans** tab, click on
the recovery plan you created and select the **TEST** action.

![](media/a054d39d7062275307af98d7baf77143.png)

Follow the steps in the wizard to launch the recovery plan test.

![](media/98c7cb7e3203d03971963ce584afc5fa.png)

Monitor progress in the SRM console and wait until the test completes
successfully.

![](media/c5d6a0bc5e94f1a8c20fe600112b5b4e.png)

Now log into the recovery site’s vCenter and confirm that the test VM has been
successfully powered on in the recovery site.

![](media/2c0dcb7c63919e37dc6f7a67dffef9cb.png)

As this was a recovery plan **test**:

-   The VM in the protected site has NOT been shut down;

-   The VM in the recovery site has been attached to an isolated network
    segment, as per the configuration you created in Task 5 (click on the
    **Networks** tab to double check).

You can now complete your recovery plan testing process by cleaning up the
recovery site. In the SRM console, select your recovery plan and click on the
**CLEANUP** button.

![](media/150c8d916f2ac294768954a472f24c7f.png)

Follow the steps in the wizard to launch the clean-up process.

## Task 8: Run Recovery Plan

In this task you will execute the recovery plan you configured in the previous
tasks. For planned migrations, a recovery plan can be run from either the
primary or the protected site. In case of an actual disaster at the protected
site, it must be triggered from the recovery site (the only one that is still
online). The steps to run a recovery plan are the same in both cases. In this
task, we will run a recovery plan from the recovery site to simulate a disaster
recovery scenario.

Log into the recovery site’s vCenter, select **Site Recovery** from the main menu
and then click on the **OPEN SITE RECOVERY** button.

![](media/6298644b3c2ce6c468bcb7180c3c242b.png)

In the SRM console, open the already configured site pair by clicking on the
**VIEW DETAILS** button.

![](media/72c14be77e2a9704bb8bf532fbfde88d.png)

When prompted for the credentials to log into the protected site, click on the
**CANCEL** button – we are assuming that the protected site is no longer online,
because of a disaster.

Select **Recovery Plans** tab, select the recovery plan defined in the previous
tasks and click on the **RUN** button.

![](media/e4f9251addacb0419bf6a1b68d22b433.png)

Follow the steps in the wizard. Select **Disaster recovery** as the recovery type.

![](media/983099f790d5c5fbc6f6ead4ce7797a9.png)

Monitor progress in the SRM console.

![](media/29fe754125734784267785cdc277877b.png)

When the recovery process is marked complete, go to the recovery site’s vCenter
and verify that the test VM GX-SRM-VM1 is powered on and attached to the
**SRM-LAB-RECOVERY** network segment.

![](media/f68b43883ab5bc938e33ddac1c96f63d.png)

Confirm that the VM migrated to the recovery site is functional by pinging it
from your jump-box. The VM’s IP address is shown in vCenter (it might be not the
same as the one shown in the screenshots).

## Task 9: Reprotect the Migrated VM

In this task, we assume that the primary site has been brought back online.
Reprotection is the SRM feature that allows migrated VMs in the recovery site to
be synchronized back to the protected site.

In the recovery site’s SRM console, select your recovery plan. Click on **…** in
the actions bar to display additional available actions and select **Reprotect**.

![](media/c96a72b031fb253eaebbd5411b753087.png)

Follow the steps in the wizard.

![](media/be2996bb8d802698d382c1e754a3b82c.png)

Monitor progress. When the reprotection process completes, go to the protected
site’s vCenter and confirm that a placeholder VM has been created.

![](media/6815bce344efb0679d96364e908a62e8.png)

## Task 10: Run Recovery Plan

In this task, you will move the test VM back to the original protected site.
This task can be performed either from the protected site’s or the recovery
site’s SRM console. The steps are identical in both cases.

In the recovery site’s SRM console, provide credentials for the protected site,
by clicking on the **LOGIN** button.

![](media/bbc48c93c42a5d7ca108d5467488a473.png)

Select your recovery plan and select **RUN**.

![](media/45faf1d7335366a3f88250dcfbb5f936.png)

Follow the steps in the wizard. As you are now performing a planned failback to
the original protected site, select **Planned Migration** as the recovery type.

![](media/6d625f59d1fe1c74ce6b8785247570fb.png)

Monitor progress. When the recovery plan run completes, go to the primary site’s
vCenter and confirm that the test VM is back online and attached to the
**SRM-LAB** network segment.

![](media/5aa9178ac0d1b963948f0c202463cc1b.png)

Confirm that the test VM is fully operational by pinging it from your jump-box
(please note that the VM’s IP address might not be the same as shown in the
screenshots).

Now that the test VM is running in the protected site, you need to also restore
replication towards the recovery site. This is done by reprotecting the VM
again. In the protected site’s SRM console, select your recovery plan, click on
the **…** item in the actions bar and select **Reprotect**.

![](media/fd102a3e30838c8cf75dcaf0a6566351.png)

Follow the steps in the wizard, which are exactly the same as those described in
Task 9. This completes the lab for SRM Disaster Recovery scenario.
