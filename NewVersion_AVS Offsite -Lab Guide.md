# Few Things before we start

1.  We will record this call & Moderators will be recording the breakout rooms
    sessions

2.  Break Out Rooms – will be closed 1 hour 5 min

3.  Every session will start with a quick discussion on what will be build and
    we move to break out rooms.

4.  Timelines for each module6

5.  Each login please let us know when you utilize

6.  Please all of you chime in to proceed with the steps

7.  Group Assignment, Lab setup and 4 modules

8.  We have a packed agenda so I would ask that you type your questions in the
    chat so the presenter can follow up or address during planned Q&A

9.  We have planned breaks but if you need to step out for a few minutes no
    worries.

10. We are hoping you have completed prerequisites

11. Customer references which are being mentioned during the presentation are
    internal purpose only

12. Provide feedback pre and post session à Links will be pasted in the Teams
    chat

13. Teams channel Link à
    <https://teams.microsoft.com/l/team/19%3asRKiNjNlQWinpCcbAiZHNI1zbOgaXbNhLk2D7wEE_aE1%40thread.tacv2/conversations?groupId=ac67fefa-a196-461e-80ae-205bda9666c3&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>




17. 

# **Module 2: Deploy HCX for VM Migration**

## Scenario

![](media/136c89b977956b39969c42626cbd4711.png)Customer would like to migrate
workloads from On-Prem VMware environment to AVS Cloud Migration

## Introduction

VMware HCX™ is an application mobility platform designed for simplifying
application migration, workload rebalancing and business continuity across data
centres and clouds. HCX supports the following types of migrations:

-   Cold Migration - Offline migration of VMs

-   Bulk Migration - scheduled bulk VM (vSphere, KVM, Hyper-V) migrations with
    reboot – low downtime

-   HCX vMotion - Zero-downtime live migration of VMs – limited scale

-   Cloud to Cloud Migrations – direct migrations between VMware Cloud SDDCs
    moving workloads from region to region or between cloud providers

-   OS Assisted Migration – bulk migration of KVM and Hyper-V workloads to
    vSphere (HCX Enterprise feature)

-   Replication Assisted vMotion - Bulk live migrations with zero downtime
    combining HCX vMotion and Bulk migration capabilities (HCX Enterprise
    feature)

In this module, we will go through the steps to Install HCX, configure and
migrate a test VM to AVS

**For more information on HCX, please visit**
<https://www.vmware.com/products/hcx.html>

**Prerequisites:**

-   Ensure that Module 1 has been completed successfully as this will be
    required to connect HCX from AVS to the On-Premises Lab.  
    Jumphost from AVS1&2 should be able to ping following ip addresses:

    -   AVS1 vCenter: get from the Azure Portal

    -   AVS2 vCenter: get from the Azure Portal

    -   On-prem vCenter: 10.211.**\#**.2/24

**Important: Make a note of Latency number from jumpbox to on-prem VM. We’ll use
that number for comparison after VM is moved from on-prem to AVS**

-   Review HCX documentation on VMware site. ([About the VMware HCX User
    Guide)](https://docs.vmware.com/en/VMware-HCX/4.0/hcx-user-guide/GUID-BFD7E194-CFE5-4259-B74B-991B26A51758.html)

## Agenda for next 60 mins:

| **Action Plan**                              | **Time required for each step** |
|----------------------------------------------|---------------------------------|
| Install VMWare HCX on AVS Private Cloud      | Preconfigured                   |
| Download HCX OVA to On-Premises vCenter      | Preconfigured                   |
| Import OVA to On-Premises vCenter            | Preconfigured                   |
| Deploy HCX to On-Premises vCenter            | 15 mins                         |
| Obtain HCX License Key                       | 5 mins                          |
| Activate VMWare HCX                          | 5 mins                          |
| Configure HCX and connect to vCenter         | 15 mins                         |
| Create Site Pairing from On-Premises to AVS  | 5 mins                          |
| Create network profiles                      | 5 mins                          |
| Create compute profiles                      | 5 mins                          |
| Create service mesh                          | 5 mins                          |
| Extend a Network                             | 10 mins                         |
| Create network extension                     | 5 mins                          |
| Migrate a VM                                 | 10 mins                         |

## **Task 1 (Preconfigured) : Install VMware HCX on AVS Private Cloud**

In the following task, we will be installing HCX on our AVS Private Cloud. This
is a simple process from the Add-Ins section in the Azure Portal, or via
Bicep/ARM/PowerShell

**NOTE: This task has been completed for you in your AVS environment**

1.  Navigate to the Azure Portal, search for *Azure VMware Solution* in the
    search bar and select

    ![Graphical user interface, text, application, email Description
    automatically generated](media/b9fae3e51ccd456a7110b2af919a7aa7.png)

2.  Select your Private Cloud – GROUP\#-AVS1-SDDC

    ![](media/86d92da2e33914305ff1cb84d939fce8.png)

3.  Select **Add-ons** \> Migration using HCX

    ![Graphical user interface, application Description automatically
    generated](media/1d9de387e6965797508ffb08ae2d7001.png)

4.  Accept the terms and conditions and “**Enable and deploy”. T**his process
    will take about 30 minutes to complete.

    **Note: This step has already been done for you**

## **Task 2 (Preconfigured): Download the HCX OVA to On-Premises vCenter**

The next step is to download HCX onto our On-Premises VMware solution, this will
allow us to setup the connectivity to AVS and allow us to migrate. The HCX
appliance is provided by VMware and has to be requested from within the AVS HCX
Manager

**NOTE: This task has been completed for you in lab environment**

1.  Obtain the AVS vCenter credentials by going to the AVS Private Cloud,
    selecting Identity. Note this down for next steps

    ![Graphical user interface, application, email Description automatically
    generated](media/271a0e1edceab23f71faf345f2d8c108.png)

2.  Navigate to the Azure portal to the Virtual Machines blade, select the
    **GROUP\#-AVS1-jumpbox** which is in the **GROUP\#-AVS1-Jumpbox** Resource
    Group.

3.  Then click **Connect \> Bastion**  
    Reminder: This is only possible since we have connected AVS to our VNet via
    our Virtual Network Gateway (Module 1, Task 1)

    ![Graphical user interface, text, application Description automatically
    generated](media/ab8635354901fcba63bdec79adf12baf.png)

1.  Use the Credentials provided to login:

    1.  username: avsjump

    2.  password: see Getting Started section

2.  Once logged in, browse to the AVS HCX Manager URL

    1.  <https://HCXCloudManagerIP> (see screenshot below)

    2.  Enter the [cloudadmin@vsphere.local](mailto:cloudadmin@vsphere.local)
        credentials from Step 1

        You can get this URL from your AVS as shown below

        ![](media/f7be2402b660477535a3c6f057e71a3c.png)T

3.  Once logged in, Go to System Updates

    ![A screenshot of a computer Description automatically
    generated](media/320602e86fa6ea6eb30d24068635f686.png)

    The Request Download Link button will be Greyed out initially but will be
    live after a minute or two. Do not navigate away from this page

    Once available, you will have an option to Download the OVA or Copy a Link.
    This link is valid for 1 week

## **Task 3 (**Preconfigured**) : Import the OVA file to the On-Premises vCenter**

In this step we will import the HCX appliance into the on premises vCenter

**NOTE: This task is already completed in your lab environment**

1.  From the Jumpbox, browse to the On-Premises vCenter URL, See [Getting
    Started](#_On-Premises_VMware_Lab) section for more information and login
    details

2.  Go to Menu \> Content Libraries

    ![Graphical user interface, application Description automatically
    generated](media/f0521b4c3bb4b3a7207f9b24e01a2620.png)

1.  Create a new content library if one doesn’t exist

2.  Once done, select Actions \> Import Item

3.  Enter HCX URL copied from Task 3, Step 6

    ![Graphical user interface, text, application, email Description
    automatically generated](media/aa0df7163b5265bbb9b5dffe036f1797.png)

4.  Accept any prompts and actions and Proceed. The HCX OVA will download to the
    library in the background

## **Task 4: Deploy the HCX OVA to On-Premises vCenter**

In this step, we will deploy the HCX VM with the configuration from the Getting
Started section

1.  Once the import is complete, Right Click this template \> New VM from This
    Template

    ![A screenshot of a computer Description automatically
    generated](media/f54edc0fc063b7ef5e77d029f9c7c0ce.png)

1.  Give the VM a **Name**, select the **Cluster**, **Datastore** and
    **Network**

    ![Graphical user interface, text, application, email Description
    automatically generated](media/5d4999057f9a933d2ecfd60d5df0eebd.png)

    ![Graphical user interface, text, application, email Description
    automatically generated](media/608845f587627296db79510c1b19e018.png)

    ![Graphical user interface, text, application, email Description
    automatically generated](media/27a77ab9fc09c2be93ac5837c6241c3e.png)

![Graphical user interface, text, application Description automatically
generated](media/e9cec8fa672af325ba0046af989e6979.png)

![Graphical user interface, text, application, email Description automatically
generated](media/6b7a3cb0e6041b14f66dbd5a692d67bc.png)

1.  In this step, we will configure the HCX appliance with the information from
    the Getting Started page. This is important as we need to specify the HCX
    manager password, hostname, and network information. In the real world,
    careful planning would have been done to identity the network and ranges to
    be used for HCX.

Enter the following details next

| **Property**                            | **Value**                                                                                                              |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Hostname                                | Any name (Suggestion: HCXGROUP**\#**) **Note: Do not leave a space in the name as this causes the webserver to fail)** |
| CLI "admin" User Password/root Password | 0hDG3VqFyTd!                                                                                                           |
| Network 1 IPv4 Address                  | 10.211.**X**.9                                                                                                         |
| Network 1 IPv4 Prefix Length            | 27                                                                                                                     |
| Default IPv4 Gateway                    | 10.211.**X**.1                                                                                                         |
| DNS Server list                         | 1.1.1.1                                                                                                                |

![Graphical user interface, application, email Description automatically
generated](media/b85bba096a40c43616f56c8adfbac9d9.png)

![Graphical user interface, application, email Description automatically
generated](media/69b481bc44f0e0969b82ecf3e8023c81.png)

![Graphical user interface, text, application, email Description automatically
generated](media/49535af268151cff5646fc54fc84a995.png)

![Graphical user interface, text, application, email Description automatically
generated](media/2f6286c6041ed03162b6b6e76a120e5d.png)

1.  Once done, navigate to Menu \> VM’s and Templates \> Power on the newly
    created HCX Manager VM. The boot process will take 5-10 minutes to complete

## **Task 5: Obtain HCX License Key**

While the HCX installation runs, we will need to obtain a license key to
activate HCX. This is available from the AVS environment.

1.  Navigate to AVS1, go to Add-ons \> Migration using HCX

2.  Select Add to enter a key name, once added a new Activation Key will appear

    ![Graphical user interface, text, application Description automatically
    generated](media/4463e97db04230bd46ea52283020fd2f.png)

## **Task 6: Activate VMware HCX**

In this task, we will activate the On-Premises HCX appliance that we just
deployed in Task 5

1.  Browse to the On-Premises HCX Manager IP specified in Task 4 on port 9443 IP
    and login (Make sure you use https:// in the address bar in the browser)

    1.  <https://10.211.x.9:9443>

2.  Login using the **HCX Credentials** specified in Task 4

    1.  Username: admin

    2.  Password: Specified earlier in Task 4 (step 3).

3.  Obtain and Copy the HCX license from the AVS1 Private Cluster in Azure (See
    Module 2, Task 2)

    ![Graphical user interface Description automatically generated with low
    confidence](media/6a9381a61a3b579d1892f89da6aa9808.png)

4.  Once logged in, In **Licensing**, enter your key for **HCX Advanced Key**
    and select **Activate**. This process can take several minutes.

    ![Graphical user interface, application, website Description automatically
    generated](media/b0e4b0b21e314ba7ac9429d66a648ba3.png)

5.  In **Datacenter Location**, provide the nearest location for installing the
    VMware HCX Manager On-Premises. Then select **Continue**.

6.  In **System Name**, modify the name or accept the default and select
    **Continue**.

![Graphical user interface, application, Teams Description automatically
generated](media/b87de655ec5a6836dd1c6863fb2c916f.png)

1.  Click “**Yes,** **Continue”** for completing next task.

![Graphical user interface, text, application Description automatically
generated](media/d9463e719a8f57fabcdf0bbf9ec8fccf.png)

## **Task 7: Configure HCX and connect to vCenter**

In this section, we will integrate HCX Manager with the On-Premises vCenter

1.  In **Connect your vCenter**, provide the FQDN or IP address of on-premise
    vCenter server and the appropriate credentials, and then select
    **Continue**., see Getting Started Section for more details

    1.  In this lab, this is <https://10.211.X.2>

    2.  Username:
        [administrator@vsphere.local](mailto:administrator@vsphere.local)

    3.  Password: 0hDG3VqFyTd!

        ![Graphical user interface, application Description automatically
        generated](media/0a34329d4d0c9980b0d59faf964df212.png)

2.  In **Configure SSO/PSC**, provide the same vCenter IP address, and select
    **Continue**.

    1.  https://10.211.X.2

        ![Graphical user interface, text, application Description automatically
        generated](media/5a9f978cbd67220a76f703daf0a27a58.png)

3.  Verify that the information entered is correct and select **Restart**..

    ![Graphical user interface, text, application Description automatically
    generated](media/56d1acedec32851aff081d76449169e1.png)

    The restart may take up to 5 minutes

4.  After the services restart, you'll see vCenter showing as **Green** on the
    screen that appears. Both vCenter and SSO must have the appropriate
    configuration parameters, which should be the same as the previous screen.

    ![Graphical user interface, application Description automatically
    generated](media/d9c3ff0b3daed977841b865b30fb338d.png)

    **Note**: It may take an additional 5-10 minutes for the HCX plugins to be
    installed in vCenter, log back out and log back in if it does not show up
    automatically

## **Task 8: Create Site Pairing from On-premises HCX to AVS HCX**

In this task, we will be creating the Site Pairing to connect the On-Premises
HCX appliance to the AVS HCX appliance

1.  Sign into your On-Premises vCenter

    1.  URL: https://10.211.x.2

    2.  Username:
        [administrator@vsphere.local](mailto:administrator@vsphere.local)

    3.  Password: 0hDG3VqFyTd!

2.  You may see a banner item to Refresh the browser, this will load the newly
    installed HCX modules. If you do not see this, log out and log back into
    vCenter

    ![A screenshot of a computer Description automatically
    generated](media/dd7b93947a327aa2cf9b8c36b7257f3f.png)

3.  Under **Menu**, Select **HCX**

4.  Navigate to Site Pairing \> Connect to Remote Site

    ![Graphical user interface Description automatically
    generated](media/a431f8293cc49c568b3f58570bdf9dc2.png)

1.  Enter remote site AVS HCX IP address and login credentials from the Azure
    Portal. See Getting Started section for more details.

    **Note** Ideally the identity provided in this step should be an AD based
    credential with delegation instead of the cloudadmin account.

    ![Graphical user interface, application Description automatically
    generated](media/c31b338dc6e4e88226af7721e2494ab0.png)

2.  Accept certificate warning and Import. Connection to the remote site will be
    established

    ![Graphical user interface, text, application, email Description
    automatically generated](media/0d505a16d2c3ac2eae84d5e610b889aa.png)

## **Task 9: Create network profiles**

VMware HCX Connector deploys a subset of virtual appliances (automated) that
require multiple IP segments. You’ll create four network profiles.

**Note**: Customer’s environments may vary and have not have separate networks.

-   Management

-   vMotion

-   Replication

-   Uplink

These networks have been defined for you, please see below section

In the real customer environment, these will have been planned and identified
previously, see here for the [planning
phase](https://docs.microsoft.com/en-us/azure/azure-vmware/plan-private-cloud-deployment#define-vmware-hcx-network-segments)

1.  Select Interconnect \> Network Profiles

    ![Graphical user interface, text, application Description automatically
    generated](media/2337f18be916d512a8639018b833907f.png)

1.  Create a network profile, use IP addresses allocated during the planning
    phase. In this lab, these are in the [Getting
    Started](#_On-Premises_HCX_details_1) section. We will create 4 separate
    network profiles:

    1.  Management

    2.  vMotion

    3.  Replication

    4.  Uplink

2.  Create Management network profiles

    1.  Select “Distributed Port Groups”

    2.  Select Management Network

**Replace “X” with your group number**

Management Network Profile

| **Property**               | **Value**                       |
|----------------------------|---------------------------------|
| Management Network IP      | 10.211.**X**.10-10.211.**X**.16 |
| Prefix Length              | 27                              |
| Management Network Gateway | 10.211.**X**.1                  |

![Graphical user interface, application Description automatically
generated](media/1c9f63a7f34234d5f5ca099053d5b2be.png)

1.  Repeat the similar steps for “Replication”, “vMotion” and “Uplink”. Use the
    configuration details provided below.

**Replace “X” with your group number**

vMotion Network Profile

| **Property**            | **Value**                       |
|-------------------------|---------------------------------|
| vMotion Network IP      | 10.211.**X**.74-10.211.**X**.77 |
| Prefix Length           | 27                              |
| vMotion Network Gateway | 10.211.**X**.65’                |
| DNS                     | 1.1.1.1                         |

Replication Network Profile

| **Property**                | **Value**                         |
|-----------------------------|-----------------------------------|
| Replication IP              | 10.211.**X**.106-10.211.**X**.109 |
| Prefix Length               | 27                                |
| Replication Network Gateway | 10.211.**X**.97                   |
| DNS                         | 1.1.1.1                           |

Uplink Network Profile

| **Property**           | **Value**                       |
|------------------------|---------------------------------|
| Uplink Network IP      | 10.211.**X**.34-10.211.**X**.40 |
| Prefix Length          | 28                              |
| Uplink Network Gateway | 10.211.**X**.33                 |
| DNS                    | 1.1.1.1                         |

![Graphical user interface, application Description automatically
generated](media/d8a7f813510d8141d0b1277071c2e94e.png)

![Graphical user interface, application Description automatically
generated](media/3e5f90bff1089d4a82b711452cacee90.png)

**  
**

## **Task 10: Create compute profiles**

A compute profile contains the compute, storage, and network settings that HCX
uses on this site to deploy the interconnected dedicated virtual appliances when
service mesh is added. For more information on compute profile and creating
please refer to [VMware
documentation](https://docs.vmware.com/en/VMware-HCX/4.2/hcx-user-guide/GUID-BBAC979E-8899-45AD-9E01-98A132CE146E.html#:~:text=A%20Compute%20Profile%20contains%20the%20compute%2C%20storage%2C%20and,virtual%20appliances%20when%20a%20Service%20Mesh%20is%20added.)

1.  Under **Infrastructure**, select **Interconnect** \> **Compute Profiles** \>
    **Create Compute Profile**.

    ![Graphical user interface, text, application, Word Description
    automatically generated](media/14bf1d3e53de1e67901370ed152929cc.png)

2.  Enter a name for the profile and select **Continue**.

3.  Review the selected services, by default all the below are selected.
    **Continue** to go to the next page

    ![Graphical user interface, application Description automatically
    generated](media/83993bf3b6b6cdc4568522f54795d197.png)

4.  In **Select Service Resources**, select one or more service resources
    (clusters) to enable the selected VMware HCX services.

5.  When you see the clusters in your On-Premises datacenter, select
    **Continue**.

    ![Graphical user interface Description automatically
    generated](media/4bfee349bbb901385987cda83f5b86cd.png)

1.  From **Select Datastore**, select the datastore storage resource for
    deploying the VMware HCX Interconnect appliances. Then select **Continue**.

    **Note**: Best practice would be to set resource reservations here as per
    requirements

    ![Graphical user interface, application Description automatically
    generated](media/9c010cd9b5983134d1e1d4b5d403a438.png)

1.  From **Select Management Network Profile**, select the management network
    profile that you created in previous steps. Then select **Continue**.

![Graphical user interface Description automatically
generated](media/4fd686bec346e45231950c9be11180f4.png)

1.  From **Select Uplink Network Profile**, select the uplink network profile
    you created in the previous procedure. Then select **Continue**.

    ![Graphical user interface Description automatically
    generated](media/0f27f76b88758dd05bb0e59d0a183972.png)

1.  From **Select vMotion Network Profile**, select the vMotion network profile
    that you created in previous steps. Then select **Continue**.

    ![Graphical user interface, diagram Description automatically
    generated](media/5b7770225f6cdb4e876b689a2cb7a983.png)

2.  From **Select vSphere Replication Network Profile**, select the replication
    network profile that you created in previous steps. Then select
    **Continue**.

    ![Graphical user interface Description automatically generated with low
    confidence](media/9b1d33857a6497a0ebd98ebd19a44de2.png)

![Diagram Description automatically
generated](media/71f42562d499887699ecf479fddb1082.png)

1.  Review the connection rules and select **Continue**.

    ![Graphical user interface Description automatically generated with medium
    confidence](media/fc1f92b27f97eac6510cc90d5bfbb535.png)

2.  Select **Finish** to create the compute profile.

    ![Graphical user interface, text, application Description automatically
    generated](media/67209a050ee1d372864b7965d80d1995.png)

## **Task 11: Create a service mesh**

In this section, we will be creating the service mesh

**Important Note -** Make sure ports UDP 500/4500 are open between your
On-Premises VMware HCX Connector 'uplink' network profile addresses and the
Azure VMware Solution HCX Cloud 'uplink' network profile addresses.

1.  Create a Service Mesh

    ![Graphical user interface, text, application, email Description
    automatically generated](media/a6e7c6bd61e635bdb676045c8b3c3eb8.png)

2.  Select the source and remote compute profiles from the drop-down lists, and
    then select **Continue**.

![A picture containing graphical user interface Description automatically
generated](media/1e4fb7c3ea61eca87023844cbd7161e6.png)

1.  Select the source and remote compute profiles from the drop-down lists, and
    then click **Continue**. Leave “Select Services to be activated” as default,
    click **Continue**.

    ![Graphical user interface, application, Word Description automatically
    generated](media/bd05e8cc2b61ca92bf4d5d758e82492c.png)

2.  In **Advanced Configuration - Override Uplink Network profiles**, select the
    uplink profile created earlier and **Continue**.

    Uplink network profiles connect to the network through which the remote
    site's interconnect appliances can be reached.

    ![Graphical user interface Description automatically generated with medium
    confidence](media/8b4db6e24421225707124b7dc74e452c.png)

3.  **In Advanced Configuration – Network Extension Appliance Scale Out**, keep
    1 as default appliance and the click **Continue**.

    ![Graphical user interface Description automatically
    generated](media/fcff2a6b621256036b2515f4abc0ea4a.png)

4.  **In Advanced Configuration – Traffic Engineering**, review and select
    **Continue**.

![Graphical user interface Description automatically
generated](media/6c62979f16c358450a7fd83419080037.png)

1.  Review the topology preview and select **Continue. En**ter a user-friendly
    name for this service mesh and select **Finish** to complete.

    **Note** the appliance names are derived from service mesh name (it's the
    appliance prefix, essentially).

![Diagram Description automatically
generated](media/b44f4a3e490362ea9c938640cf70844a.png)

1.  The Service Mesh deployment will take 5-10 minutes to complete. Once
    successful, you will see the services as green

    ![Graphical user interface, text, application, chat or text message, email
    Description automatically
    generated](media/65b54016fd86d97b552ab4d80cad96b2.png)

2.  Select **Interconnect \> Appliances**

    ![Graphical user interface, text, application Description automatically
    generated](media/ae9326d87a11b8545920e0db715e71e3.png)

    The HCX interconnect tunnel status should indicate **UP** and in green.
    You're ready to migrate and protect Azure VMware Solution VMs using VMware
    HCX. Azure VMware Solution supports workload migrations (with or without a
    network extension). So you can still migrate workloads in your vSphere
    environment, along with On-Premises creation of networks and deployment of
    VMs onto those networks. For more information, see the [VMware HCX
    Documentation](https://docs.vmware.com/en/VMware-HCX/index.html)

**While we wait, let’s discuss the migration options**

## **Task 12 Setup the Network Extension**

Once the Service Mesh appliances have been deployed, the next important step is
to extend the on-premise network to AVS, so that any migrated VM’s will be able
to retain their existing IP address and be accessible from all locations

1.  Navigate to **Network Extension,** Create a Network Extension

    ![Graphical user interface, text, website Description automatically
    generated](media/f9faed0da1836acad9fcfea26682da5a.png)

2.  Select the service mesh and segment to extend. In this lab, we will extend
    **workload-web**

    ![Graphical user interface, application Description automatically
    generated](media/4279fd1dd752bcb12e57d5d44c8725a1.png)

3.  Select the First Hop Router, in this Lab there is only 1 option –
    **TNTXX-TI**

4.  Enter the Workload Web Gateway IP as 10.211.10**X**.1/25 or
    10.211.1**XX**.1/25 (Group 10+)

    ![Graphical user interface, text, application, email Description
    automatically generated](media/e9731ade07f7a8bf3ee8172fc72ae6b6.png)

5.  Submit, this will start the process of extending the network by creating a
    remote stretch record and network bridges on the remote AVS side. This will
    take about 3-5 minutes to complete

    ![Graphical user interface, text, application Description automatically
    generated](media/41ee30763f7c89fcfe7c427d25d12837.png)

## **Task 13: Migrate a VM using HCX and vMotion**

Now that the Service Mesh appliances have been deployed successfully, we can now
migrate workloads from on-premises to AVS. In this lab, we will migrate a Test
VM using vMotion

As part of the on-premises lab, you will see a VM folder named **Workloads** and
a VM called **SampleApp-AppA-Standalone** already connected to our
**workload-web** network

![Graphical user interface, text, application Description automatically
generated](media/8d8377951355a4fdf93a9a0ca8fbc114.png)

1.  **To test a migration of this VM, from the HCX Menu, select Migration and
    the Migrate button**

    ![Graphical user interface, text, application, email Description
    automatically generated](media/d195c68b3a7a95a5182e031eb07db2bc.png)

2.  **Select the SampleApp-AppA-Standalone VM and Add**

    ![Graphical user interface, text, application, email Description
    automatically generated](media/fc1b4a25b1674b1b327c1d393d024185.png)

3.  **Here we have to specify our destination AVS settings and where to migrate
    this VM**

    1.  **Computer Container – Select Cluster-1**

    2.  **Destination Folder – Any folder**

    3.  **Destination Storage – vsanDatastore**

    4.  **Migration Profile – vMotion**

![A screenshot of a computer Description automatically
generated](media/6afd5c30810b6d6edd7a7800aa83f086.png)

1.  **Validation step, expand “VM for Migration”, note the Network Adapter is
    automatically filled in. This is the network extension adapter that was
    created in the previous task (optional)**

    ![Graphical user interface, text, application, email Description
    automatically generated](media/4af2de468d09f150cea0b9e44f80f0bf.png)

2.  **Select Validate and Go – This will migrate the VM to AVS. Since this is
    vMotion, there is no downtime experienced and the VM is moved without any
    disruption**

**  
**

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

![Diagram Description automatically
generated](media/285abcfd08e365730976517140c3e2be.png)

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

![Diagram Description automatically
generated](media/eb6490e5af96d0baf0e7b0971e1e3025.png)

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

![Graphical user interface, application Description automatically
generated](media/4390100ec5e84088fcdaad8dce762258.png)

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

![Diagram Description automatically
generated](media/d95f6098d2f1f96765ebd76e5d24fab7.png)

vSphere Replication begins the initial full synchronization of the source
virtual machine to the target location, using TCP port 31031. A copy of the
VMDKs to be replicated can be created and shipped to the target location and
used as “seeds,” reducing the time and network throughput. Changes to the
protected virtual machine are tracked and replicated on a regular basis. The
transmissions of these changes are referred to as “lightweight delta syncs.”
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

**  
**

## **Task 0 (preconfigured): Install SRM add-on in the protected and the recovery sites**

**In the lab environment, this task has been already completed**, as it can take
up to 30 minutes to complete.

In the Azure portal, browse to the primary AVS Private Cloud
(GROUP\#-AVS1-SDDC), select the “Add-ons” item from the menu and the click on
the “Get Started” button in the “Disaster Recovery” tile.

![Graphical user interface, text, application Description automatically
generated](media/9ed4b5667c42384d2105f50d61508087.png)

Verify that SRM and vSphere replication are already installed (**BOTH** buttons
read “Uninstall…”).

![Graphical user interface, text, application, email Description automatically
generated](media/85da7c550ec14ea7f3c734a60cc95294.png)

## **Task 1**: Configure the production site (GROUP\#-AVS1-SDDC)

In this task you will create a network segment in the production site and deploy
a test VM to be protected with Site Recovery Manager.

*This task requires a DHCP profile to be available in the private cloud. DHCP
profiles have been configured in Module 1 for both GROUP\#-AVS1-SDDC and
GROUP\#-AVS2-SDDC. If you did not complete the corresponding steps in Module 1,
please go back to it and configure DHCP profiles before proceeding.*

Log into NSX-T client for the protected/primary site GROUP\#-AVS1-SDDC. Click on
the “Segments” item in the left-hand menu and then click the “ADD SEGMENT”
button in the main tile. Enter the following configuration settings:

-   Segment Name: “SRM-LAB”

-   Connected gateway: Select the private cloud’s default Tier1 gateway

-   Transport Zone: Select the private cloud’s default **overlay** transport
    zone

-   Gateway CIDR IPv4: “10.\#.60.1/24”

![Graphical user interface, text, application Description automatically
generated](media/367712fc63544d3aac43e67cd75c5220.png)

Click on the “SET DHCP CONFIG” button and provide the following settings:

-   DHCP Type: “Gateway DHCP Server”

-   DHCP Profile: Select the profile created in Module 1

-   DHCP Config: Set the toggle to “Enabled”

-   DHCP Ranges: “10.\#.60.100-10.\#.60.120”

![Graphical user interface, application Description automatically
generated](media/3fc2f1868be7edaa9625e29e5b5efe32.png)

When done, click on the “APPLY” button to close the DHCP Configuration window.
Then scroll down and click on the “SAVE” button to commit the segment
configuration.

![Graphical user interface, text, application, email, website Description
automatically generated](media/27e39ac4a19c0d7b2200f30f7b9f0605.png)

Click “NO” to close the configuration window. Confirm the segment is
successfully configured by checking that it appears in the segments list.

![A computer screen capture Description automatically generated with medium
confidence](media/cee6bdc13e1efc967011ebbe78b0a1f8.png)

Optionally, you can confirm that the newly created segment is also visible in
the Azure portal. It may take up to 2-3 mins to show up in the portal.

Navigate to GROUP\#-AVS1-SDDC AVS Private Cloud and select the “Segments” item
in the Workload Networking menu on the left-hand side.

![Graphical user interface, text, application, email Description automatically
generated](media/c44d19dd3dac0b8ba66c71197309b9a6.png)

## Task 2: Create a VM in the protected site

In this task you will create a test VM in the protected site.

*This task requires a VM template file to be available in the private cloud. A
template has been added to the private cloud’s Local Library in Module 1. If you
did not complete the corresponding steps in Module 1, please go back to it and
add a template to your protected site’s Local Library.*

Log into vCenter for the protected site GROUP\#-AVS1-SDDC. From the main menu
select “Content Libraries” and then click on “Local Library”. In the “Templates”
section, find the template “NetworkTest-VM”, right-click on it and select “New
VM from This Template” from the context menu.

![Graphical user interface Description automatically
generated](media/e0eed977a780948438f1feabdadca181.png)

Follow the steps in the VM configuration wizard. First, set the VM name to
“GX-SRM-VM1” and select the location “SDDC-Datacenter”.

![Graphical user interface, text, application, email Description automatically
generated](media/af10b25e4315bbae52b4356e3b088d80.png)

Then, go through the “Review Details” step (no configuration is required here)
and, in the “Select storage” step, select “vSAN Default Storage Policy”.

![Graphical user interface, text, application, email Description automatically
generated](media/fc5cc689dc8c6093f53c50f12c5f733a.png)

Finally, attach the VM to the network segment created in Task1, by selecting
“SRM-LAB” in the “Destination Network” drop-down menu. Deploy the VM by clicking
on the “Finish” button.

![Graphical user interface, application, email Description automatically
generated](media/bc719a8326876c91827c186e7b47183b.png)

In the main vCenter menu, select “VMs and Templates” and then click on the newly
created VM “GX-SRM-VM1”. Power it on by clicking on the green “Power On” icon.

![Graphical user interface, application, table Description automatically
generated](media/b354049252367e3210c7680337af984f.png)

When the VM starts, check that it has been assigned an IP address in the DHCP
range configured in Task 1.

![Graphical user interface, text, application, website Description automatically
generated](media/96f56838bed0f88643da6f8f3a9770d1.png)

Test your network configuration by pinging the VM from the jump-box you are
working on.

![Graphical user interface, application Description automatically
generated](media/e61ddb7e9c1c22afca8eacc835eba309.png)

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

Click on the “Network” menu item on the taskbar at the top of the window, select
“Segments” from the menu on the left and click the “ADD SEGMENT” button.

![Graphical user interface, website Description automatically
generated](media/49e2aea5074a27e19d5f8244b73bdf14.png)

In the segment configuration tile, enter the following settings:

-   Segment Name: “SRM-LAB-RECOVERY”

-   Connected gateway: Select the private cloud’s default Tier1 gateway

-   Transport Zone: Select the private cloud’s default overlay transport zone

-   Gateway CIDR IPv4: “10.\#.160.1/24” (please note that this IP subnet is not
    the same as the primary site’s)

![Graphical user interface, application Description automatically
generated](media/1079bccfca90baf5c459fe5e28a2bc29.png)

Click on the “SET DHCP CONFIG” button and provide the following settings:

-   DHCP Type: “Gateway DHCP Server”

-   DHCP Profile: Select the profile created in Module 1

-   DHCP Config: Set the toggle to “Enabled”

-   DHCP Ranges: “10.\#.160.100-10.\#.160.120”

![Graphical user interface, text, application, email Description automatically
generated](media/2c58686a0ee8dd395cbd66dd35545924.png)

When done, click on the “APPLY” button to close the DHCP Configuration window.
Then scroll down and click on the “SAVE” button to commit the segment
configuration.

![Graphical user interface, application, email Description automatically
generated](media/d572a8a2d7a2879100971ce1e8b27b0b.png)

Confirm that the segment has been created successfully.

![Graphical user interface, application, table, Word Description automatically
generated](media/5f22e72b7e51403fbfaea81cf0aa0a07.png)

Optionally, you can confirm that the newly created segment is also visible in
the Azure portal (navigate to GROUP\#-AVS2-SDDC Private Cloud and select the
“Segments” item in the Workload Networking menu on the left-hand side.

![Graphical user interface, text, application Description automatically
generated](media/da0bcd9932febb3eba083afac1db3712.png)

## Task 4: Configure a Site Pairing in Site Recovery Manager

In this task you will pair the protected site GROUP\#-AVS1-SDDC and the recovery
site GROUP\#-AVS2-SDDC.

Site pairing can be configured from vCenter on either the primary or the
recovery private cloud. You will work on the primary site’s vCenter. If needed,
log into vCenter in the primary AVS private cloud GROUP\#-AVS1-SDDC and select
“Site Recovery” from the main menu. Click on the “OPEN Site Recovery” button.

![Graphical user interface, text, website Description automatically
generated](media/31c387a424cd9ac00e00f5b1f46ec7d5.png)

Site Recovery Manager opens in a new browser tab.

**Note: Web page may perpetually get stuck into loading status. In this case, go
back to main page and click “Open Site Recovery” button again.**

Click on the “NEW SITE PAIR” button to launch the configuration wizard.

![Graphical user interface, application, table, Word Description automatically
generated](media/2846f78785bf7bc7f6b5a4906ef0b335.png)

Select the local vCenter server that you want to pair. The only option is the
protected site’s vCenter (GROUP\#-AVS1-SDDC). Provide the IP address and the
credentials of the recovery site’s vCenter (GROUP\#-AVS2-SDDC), which can be
obtained from the Azure portal. Ensure that you remove *https and/or any
slashes* after pasting the vCenter value.

![A screenshot of a computer Description automatically
generated](media/47c5c80246569ab43d588f1d041e256f.png)

Click on the “NEXT” button. The security alert(s) that you receive are due to
the usage of certificates issued by an untrusted CA in the lab. In real,
production environments certificates issued by a trusted CA should be used
instead. In this lab, you can ignore the security warning and click on the
“CONNECT” button.

![A picture containing text, screenshot, monitor Description automatically
generated](media/7fd8b7be48eb293420088b5ce16b654a.png)

Configure the site pairing with both the SRM and the vSphere replication
services. Again, you can ignore the security warnings due to untrusted
certificates and proceed by clicking on the “CONNECT” button.

![Graphical user interface, application, Word Description automatically
generated](media/157d9ea5d2c9d933aebb494ee08af686.png)

When the configuration process completes, the SRM main page displays the new
site pairing.

![Graphical user interface, application, table, Word Description automatically
generated](media/a78bc6bd597184e555fa5572994e75a7.png)

## Task 5: Configure Inventory Mappings

In this task you will configure inventory mappings, which define the resources
(networks, folders, compute resources, storage policies) that VMs must use when
moved to the recovery site. It is also possible to define reverse mappings,
which control resource allocation for failback processes.

### Network mappings

Open the “Site Pair” configuration pane in SRM and select “Network Mappings” in
the “Configure” section of the left-hand-side menu. Then click on the “NEW”
button to launch the configuration wizard.

![Graphical user interface, application, table Description automatically
generated](media/850e44547c85fe48a4151e6fd7eed8b2.png)

Select “Prepare mappings manually” to define a custom mapping between the
network segments created for the SRM lab module in the previous tasks. Then
click on the “NEXT” button and map the “SRM-LAB” segment in the protected site
to the “SRM-LAB-RECOVERY” segment in the recovery site. Click on the “ADD
MAPPINGS” button to confirm.

![Graphical user interface, application, Word Description automatically
generated](media/2efdf93a054c742f7bb646c4dc6c6223.png)

In the “Reverse Mapping” step, enable the suggested reverse mapping.

![Graphical user interface, application, Word Description automatically
generated](media/27d7d8cde06f10747292ad75184dabc6.png)

In “Test Networks” step, accept the default setting. When later in the module
you will test your recovery plan, the protected VM will be instantiated in an
isolated network segment automatically created at the beginning of the test (and
automatically removed when the recovery plan test is cleaned up).

![Graphical user interface, application, Word Description automatically
generated](media/562687484b97b3263514f43493700ca6.png)

Click on the “NEXT” button and then commit your configuration by clicking on the
green “FINISH” button.

### Folder Mappings

Open the “Site Pair” configuration pane in SRM and select “Folder Mappings” in
the “Configure” section of the left-hand-side menu. Then click on the “NEW”
button to launch the configuration wizard.

![Graphical user interface, application Description automatically
generated](media/59f2f3e76565bba79fe9fd9e27fe6f1e.png)

Select “Automatically prepare mappings for folders with the same name”, then
click on the “NEXT” button. Select “SDDC-Datacenter” on both sides of the
mapping and click on the “ADD MAPPINGS” button. Accept the automatically
prepared mappings.

![Graphical user interface, application, Word Description automatically
generated](media/9ced3b0f8b626c61b50364d9c5090d2d.png)

On step 3 “Reverse Mappings” accept the mappings proposed by the wizard. Then
click on the “NEXT” button and commit your configuration by clicking on the
green “FINISH” button.

![Graphical user interface, text, application, Word Description automatically
generated](media/b7930ecbdb992b6419aed0426908309a.png)

### Resource Mappings

Open the “Site Pair” configuration pane in SRM and select “Resource Mappings” in
the “Configure” section of the left-hand-side menu. Then click on the “NEW”
button to launch the configuration wizard.

![Graphical user interface, application Description automatically
generated](media/420dd1c3327bb44786d1e4e4fe872f50.png)

On step 1 “Recovery Resources” expand the “SDDC-Datacenter” nodes on both the
primary and the recovery side and select “Cluster 1”. Click on the “ADD
MAPPINGS” button to confirm.

![Graphical user interface, text, application, Word Description automatically
generated](media/25fe495c757206ea9717e6f9a1320278.png)

Accept the reverse mapping proposed by the wizard, click on the “NEXT” button
and then confirm your settings by clicking on the green “FINISH” button.

![Graphical user interface, text, application Description automatically
generated](media/0cb1fd060fb96745f45992f0779d169f.png)

### Storage Policy Mappings

Open the “Site Pair” configuration pane in SRM and select “Storage Policy
Mappings” in the “Configure” section of the left-hand-side menu. Then click on
the “NEW” button to launch the configuration wizard.

![Graphical user interface, application, table, Word Description automatically
generated](media/0eb20eaf58bbcf7f4f03b2c295c81c24.png)

Select “Automatically prepare mappings for storage policies with the same name”,
then click on the “NEXT” button. Select “vSAN Default Storage Policy” on both
sides of the mapping and click on the “ADD MAPPINGS” button. Accept the
automatically prepared mappings. Accept the automatically discovered mappings.

![Graphical user interface, application Description automatically
generated](media/db8788f38475d84d72ee8b6e572f406e.png)

Accept the reverse mapping proposed by the wizard, click on the “NEXT” button
and then confirm your settings by clicking on the green “FINISH” button.

![Graphical user interface, text, application Description automatically
generated](media/e80c270f4536be4eba1b004b39448cd9.png)

### Placeholder Datastores

When vSphere Replication is configured for a VM, a “placeholder VM” is created
in the target recovery site. Placeholder VMs represent, in the recovery site,
VMs that will be instantiated when a recovery plan is run. SRM requires you to
define which datastore to use for placeholder VMs. If you plan to use SRM for
failback, you need to define placeholder datastores at both the protected and
the recovery sites.

Open the “Site Pair” configuration pane in SRM and select “Placeholder
Datastores” in the “Configure” section of the left-hand-side menu. In the
“Placeholder Datastores” configuration tile, select your primary site’s vCenter
server (its FQDN ends with the suffix “**eastus2**.avs.azure.com”).

![Graphical user interface, text, application, Word Description automatically
generated](media/01f786a9886c37613a38e504d25f26a4.png)

Click on the “NEW” button to add a datastore. Select “vSAN Datastore” and click
on the “ADD” button.

![Graphical user interface, application, Word Description automatically
generated](media/f633376f0777f39351ce0507d6d1638f.png)

Repeat the same steps for the recovery site’s vCenter (its FQDN ends with the
suffix “**southcentralus**.avs.azure.com”).

![Graphical user interface, text, application, Word Description automatically
generated](media/4cbe92d7e370b175e72f8c8ce9e0a458.png)

Click on the “NEW” button to add a datastore. Select “vSAN Datastore” and click
on the “ADD” button.

![Graphical user interface, application, Word Description automatically
generated](media/37cf2222e43de01f9dfdc16a68b122a3.png)

## Task 6: Configure vSphere Replication and Recovery Plan

In this task you will configure vSphere replication for the test VM created in
Task 2 and a recovery plan to protect it. This task is performed from the
primary site’s vCenter client. In the main menu, select “VM and Templates” and
then right-click on your test VM named GX-SRM-VM1. From the context menu, select
“All Site Recovery Actions” and then “Configure replication”.

*Note: Check pop-up blocker if stuck.*

![Graphical user interface, text, application Description automatically
generated](media/1044498d505fba36f9621e504fef8401.png)

### vSphere Replication

![Graphical user interface, application, table Description automatically
generated](media/4178918f64a3ec52800aa8b91985bda8.png)

Follow the steps in the configuration wizard. Select the recovery site (FDQN
ending with the suffix **southcentralus.avs.azure.com**) as the target site.
Provide credentials for the recovery site’s vCenter. The credentials are
available in the Azure portal. Select “Auto-assign replication server”.

![Graphical user interface, application, Word Description automatically
generated](media/921e6c47831001cec93fa0b1cb0cbb2b.png)

Check that the test VM is ready for replication, then click on the “NEXT” button
and select “vSAN Datastore” as the target datastore. In the “Replication
Settings” step, select the RPO you want to have for the protected VM (15 mins in
the screenshot below).

![Graphical user interface, text, application Description automatically
generated](media/ed04edab49abb4c8ebf49ec2440e7745.png)

### SRM Protection Group and Recovery Plan

The last two steps in the configuration wizard allow you to create an SRM
Protection Group and a Recovery Plan. Please note that this is needed because
you are configuring SRM protection for the first VM. Additional VMs can leverage
existing protection groups and recovery plans. In step 5 “Protection Group”
enter a name for your protection group, such as “SRM-LAB-PROTECTION-GROUP”. In
step 6 “Recovery Plan” enter a name for your recovery plan, such as
“SRM-LAB-REC-PLAN”. Confirm your settings by clicking on the green “FINISH”
button.![Graphical user interface, table Description automatically generated
with medium confidence](media/456e8f584cc78a9b7a95f1963c641cd6.png)

Wait until the replication status for your test VM is reported to be “OK” (use
the “Refresh” button in SRM’s console).

![Graphical user interface, text, application, email Description automatically
generated](media/29a104a28bda920bc3bdb24cfd2a6d6d.png)

To confirm that replication and SRM protection have been successfully
configured, log into the recovery site’s vCenter and check that a placeholder VM
has been created.

![A screenshot of a computer Description automatically
generated](media/589542c3eaf085fcca44f07bd46d2979.png)

## Task 7: Test Recovery Plan

In this task you will test the recovery plan created in the previous one.

In the protected site’s SRM console, select the “Recovery Plans” tab, click on
the recovery plan you created and select the “TEST” action.

![Graphical user interface, text, application Description automatically
generated](media/a054d39d7062275307af98d7baf77143.png)

Follow the steps in the wizard to launch the recovery plan test.

![Graphical user interface, application, table Description automatically
generated](media/98c7cb7e3203d03971963ce584afc5fa.png)

Monitor progress in the SRM console and wait until the test completes
successfully.

![Graphical user interface, application Description automatically
generated](media/c5d6a0bc5e94f1a8c20fe600112b5b4e.png)

Now log into the recovery site’s vCenter and confirm that the test VM has been
successfully powered on in the recovery site.

![Graphical user interface, application, table Description automatically
generated](media/2c0dcb7c63919e37dc6f7a67dffef9cb.png)

As this was a recovery plan **test**:

-   The VM in the protected site has NOT been shut down;

-   The VM in the recovery site has been attached to an isolated network
    segment, as per the configuration you created in Task 5 (click on the
    “Networks” tab to double check).

You can now complete your recovery plan testing process by cleaning up the
recovery site. In the SRM console, select your recovery plan and click on the
“CLEANUP” button.

![Graphical user interface, application, table Description automatically
generated](media/150c8d916f2ac294768954a472f24c7f.png)

Follow the steps in the wizard to launch the clean-up process.

## Task 8: Run Recovery Plan

In this task you will execute the recovery plan you configured in the previous
tasks. For planned migrations, a recovery plan can be run from either the
primary or the protected site. In case of an actual disaster at the protected
site, it must be triggered from the recovery site (the only one that is still
online). The steps to run a recovery plan are the same in both cases. In this
task, we will run a recovery plan from the recovery site to simulate a disaster
recovery scenario.

Log into the recovery site’s vCenter, select “Site Recovery” from the main menu
and then click on the “OPEN SITE RECOVERY” button.

![Graphical user interface, application, Word Description automatically
generated](media/6298644b3c2ce6c468bcb7180c3c242b.png)

In the SRM console, open the already configured site pair by clicking on the
“VIEW DETAILS” button.

![Graphical user interface, application, Word Description automatically
generated](media/72c14be77e2a9704bb8bf532fbfde88d.png)

When prompted for the credentials to log into the protected site, click on the
“CANCEL” button – we are assuming that the protected site is no longer online,
because of a disaster.

Select “Recovery Plans” tab, select the recovery plan defined in the previous
tasks and click on the “RUN” button.

![Graphical user interface, text, application, Word Description automatically
generated](media/e4f9251addacb0419bf6a1b68d22b433.png)

Follow the steps in the wizard. Select “Disaster recovery” as the recovery type.

![Graphical user interface Description automatically
generated](media/983099f790d5c5fbc6f6ead4ce7797a9.png)

Monitor progress in the SRM console.

![Graphical user interface, application, table Description automatically
generated](media/29fe754125734784267785cdc277877b.png)

When the recovery process is marked complete, go to the recovery site’s vCenter
and verify that the test VM GX-SRM-VM1 is powered on and attached to the
“SRM-LAB-RECOVERY” network segment.

![Graphical user interface, application Description automatically
generated](media/f68b43883ab5bc938e33ddac1c96f63d.png)

Confirm that the VM migrated to the recovery site is functional by pinging it
from your jump-box. The VM’s IP address is shown in vCenter (it might be not the
same as the one shown in the screenshots).

## Task 9: Reprotect the Migrated VM

In this task, we assume that the primary site has been brought back online.
Reprotection is the SRM feature that allows migrated VMs in the recovery site to
be synchronized back to the protected site.

In the recovery site’s SRM console, select your recovery plan. Click on “…” in
the actions bar to display additional available actions and select “Reprotect”.

![Graphical user interface, text, application, email Description automatically
generated](media/c96a72b031fb253eaebbd5411b753087.png)

Follow the steps in the wizard.

![Graphical user interface, text, application Description automatically
generated](media/be2996bb8d802698d382c1e754a3b82c.png)

Monitor progress. When the reprotection process completes, go to the protected
site’s vCenter and confirm that a placeholder VM has been created.

![Graphical user interface, text, application, email Description automatically
generated](media/6815bce344efb0679d96364e908a62e8.png)

## Task 10: Run Recovery Plan

In this task, you will move the test VM back to the original protected site.
This task can be performed either from the protected site’s or the recovery
site’s SRM console. The steps are identical in both cases.

In the recovery site’s SRM console, provide credentials for the protected site,
by clicking on the “LOGIN” button.

![Graphical user interface, text, application, email Description automatically
generated](media/bbc48c93c42a5d7ca108d5467488a473.png)

Select your recovery plan and select “RUN”.

![Graphical user interface, application, table Description automatically
generated](media/45faf1d7335366a3f88250dcfbb5f936.png)

Follow the steps in the wizard. As you are now performing a planned failback to
the original protected site, select “Planned Migration” as the recovery type.

![Graphical user interface, application Description automatically
generated](media/6d625f59d1fe1c74ce6b8785247570fb.png)

Monitor progress. When the recovery plan run completes, go to the primary site’s
vCenter and confirm that the test VM is back online and attached to the
“SRM-LAB” network segment.

![Graphical user interface, text, application, website Description automatically
generated](media/5aa9178ac0d1b963948f0c202463cc1b.png)

Confirm that the test VM is fully operational by pinging it from your jump-box
(please note that the VM’s IP address might not be the same as shown in the
screenshots).

Now that the test VM is running in the protected site, you need to also restore
replication towards the recovery site. This is done by reprotecting the VM
again. In the protected site’s SRM console, select your recovery plan, click on
the “…” item in the actions bar and select “Reprotect”.

![Graphical user interface, text Description automatically
generated](media/fd102a3e30838c8cf75dcaf0a6566351.png)

Follow the steps in the wizard, which are exactly the same as those described in
Task 9. This completes the lab for SRM Disaster Recovery scenario.

# Module 4: Create and configure a Secure Hub to route traffic to the internet

**Section Overview:**

Now that the Tier-0 and Tier-1 routers are configured, it’s time to see if
workloads can access the internet. The key takeaway here is to setup a Secured
vWAN Hub to allow internet egress and ingress (if necessary) for the VMs on AVS.

In this section you will learn how to:

-   Create a secure VWAN hub

-   Configure Azure Firewall with a public IP

-   Configure Azure Firewall

![](media/e9b7bd3e015aa202ea6169f446d49e2c.png)

Before we start the steps, let’s validate if the AVS VMs can access internet. In
the previous section, you accessed VM1 from the vCenter portal. Verify that from
VM1 that you can not

-   Access [www.google.com](http://www.google.com) by name. On the server,
    **type** wget [www.google.com](http://www.google.com)

-   Access [www.google.com](http://www.google.com) by IP. On the server,
    **type** wget <https://142.250.9.101>

You may also use utilities such as ping or nslookup to validate.

**Deployment Steps:**

## Task 1: Deploy Virtual WAN

1.  Sign into the Azure portal and then search for and select Azure VMware
    Solution.

2.  Select the Azure VMware Solution private cloud.

3.  Under Manage, select Connectivity.

4.  Select the Public IP tab and then select Configure.

![Graphical user interface, application Description automatically
generated](media/940de2ea4f975fdd88235093f29267f1.png)

1.  Accept the default values, modify the Virtual hub address block and Number
    of Public Ips fields. Select Create.

| Field                         | Value                                                                                                                 |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Virtual WAN resource group    | Auto-populated and can not be modified in the poral                                                                   |
| Virtual WAN name              | Leave default auto-populated                                                                                          |
| Virtual hub address block     | Use the following value 10.**[Your Group Number]**.4.0/24 to avoid conflict with other networks used in this training |
| Number of public IPs (1-100): | 1                                                                                                                     |

![Graphical user interface, text, application, email Description automatically
generated](media/6295fbcd7f543b20d04c2dbdfb5bf43e.png)

It takes about one hour to complete the deployment of all components. This
deployment only must occur once to support all future public IPs for this Azure
VMware Solution environment.

![Graphical user interface, text, application, email Description automatically
generated](media/7edc575f5739614c0749fc11eefb53c4.png)

## Task 2: Configure Public IP Option

1.  ![Graphical user interface, application, Word Description automatically
    generated](media/1c41d58397fa44bf1060ec12d6da9998.png)

## Task 3: Configure Azure Firewall policies

Once Azure vWAN is configured, you will see both Azure Firewall

**![Graphical user interface, text, application, email Description automatically
generated](media/1338fdc5a5507051b303c08de98504a5.png)**

1.  In the Azure portal, search for and select **Firewall**.

2.  Select a deployed firewall and then select **Visit Azure Firewall Manager to
    configure and manage this firewall**.

**![Graphical user interface, application, Teams Description automatically
generated](media/9b093e8d6f2f8db7b6be11023942a1d4.png)**

1.  ![Graphical user interface, application Description automatically
    generated](media/a0cd005269a3e269268bd4a82eb056bd.png)Select Azure Firewall
    Policies and then select Create Azure Firewall Policy.

1.  Under the **Basics** tab, provide the required details.

| Field          | Value                        |
|----------------|------------------------------|
| Subscription   | Auto-populated               |
| Resource Group | Leave default auto-populated |
| Name           | “Internet Enabled”           |
| Region         | Pre-Populated                |
| Policy Tier    | Standard                     |
| Parent Policy  | None                         |

1.  Select Next: DNS Settings.

2.  Under the **DNS** tab, select **Enable**. For **DNS Servers** Select the
    Default (Azure provided). For the **DNS Proxy** select **Enabled**

    ![Graphical user interface, application Description automatically generated
    with medium confidence](media/4b4d9977a47254264b7f9423b9c256e5.png)

3.  and then select Next: **Rules**.

4.  Select **Add a rule collection**, provide the below details, and select Add.

5.  

| Field                  | Value                                    |
|------------------------|------------------------------------------|
| Name                   | “Internet Outbound Enabled”              |
| Rule collection type   |  Network                                 |
| Priority               | Select a numeric value between 100-65000 |
| Rule collection action | Allow                                    |
| Rule collection group  | Pre-populated                            |
| Name of Rule           | Optional                                 |
| Source Type            | IPaddress                                |
| Source                 | \*                                       |
| Protocol               | TCP                                      |
| Destination port       | 80,443                                   |
| Destination Type       | IP Address                               |
| Destination            | \*                                       |

**![Graphical user interface, application Description automatically
generated](media/ab61733e496d70a297bd8ca5823ee425.png)**

1.  Select Next: **Tags**.

2.  (Optional) Create name and value pairs to categorize your resources.

3.  Select Next: **Review** + **create** and then select **Create**.

Log back into vCenter and retest VM1’s internet connectivity
