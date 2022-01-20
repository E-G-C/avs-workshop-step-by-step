## **Task 10: Create compute profiles**

A compute profile contains the compute, storage, and network settings that HCX
uses on this site to deploy the interconnected dedicated virtual appliances when
service mesh is added. For more information on compute profile and creating
please refer to [VMware
documentation](https://docs.vmware.com/en/VMware-HCX/4.2/hcx-user-guide/GUID-BBAC979E-8899-45AD-9E01-98A132CE146E.html#:~:text=A%20Compute%20Profile%20contains%20the%20compute%2C%20storage%2C%20and,virtual%20appliances%20when%20a%20Service%20Mesh%20is%20added.)

1.  Under **Infrastructure**, select **Interconnect** \> **Compute Profiles** \>
    **Create Compute Profile**.

    ![](media/14bf1d3e53de1e67901370ed152929cc.png)

2.  Enter a name for the profile and select **Continue**.

3.  Review the selected services, by default all the below are selected.
    **Continue** to go to the next page

    ![](media/83993bf3b6b6cdc4568522f54795d197.png)

4.  In **Select Service Resources**, select one or more service resources
    (clusters) to enable the selected VMware HCX services.

5.  When you see the clusters in your On-Premises datacenter, select
    **Continue**.

    ![](media/4bfee349bbb901385987cda83f5b86cd.png)

6.  From **Select Datastore**, select the datastore storage resource for
    deploying the VMware HCX Interconnect appliances. Then select **Continue**.

    **Note**: Best practice would be to set resource reservations here as per
    requirements

    ![](media/9c010cd9b5983134d1e1d4b5d403a438.png)

7.  From **Select Management Network Profile**, select the management network
    profile that you created in previous steps. Then select **Continue**.

    ![](media/4fd686bec346e45231950c9be11180f4.png)

8.  From **Select Uplink Network Profile**, select the uplink network profile
    you created in the previous procedure. Then select **Continue**.

    ![](media/0f27f76b88758dd05bb0e59d0a183972.png)

9.  From **Select vMotion Network Profile**, select the vMotion network profile
    that you created in previous steps. Then select **Continue**.

    ![](media/5b7770225f6cdb4e876b689a2cb7a983.png)

10.  From **Select vSphere Replication Network Profile**, select the replication
    network profile that you created in previous steps. Then select
    **Continue**.

   ![](media/9b1d33857a6497a0ebd98ebd19a44de2.png)

   ![](media/71f42562d499887699ecf479fddb1082.png)


11.  Review the connection rules and select **Continue**.

   ![](media/fc1f92b27f97eac6510cc90d5bfbb535.png)

12.  Select **Finish** to create the compute profile.

   ![](media/67209a050ee1d372864b7965d80d1995.png)


## Next Steps

[Module 2 Task 11](module-2-task-11)

[Module 2 Index](module-2-index)

[Main Index](index)