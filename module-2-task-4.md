## **Task 4: Deploy the HCX OVA to On-Premises vCenter**

In this step, we will deploy the HCX VM with the configuration from the Getting
Started section

1.  Once the import is complete, Right Click this template \> New VM from This
    Template

    ![](media/f54edc0fc063b7ef5e77d029f9c7c0ce.png)

2.  Give the VM a **Name**, select the **Cluster**, **Datastore** and
    **Network**

    ![](media/5d4999057f9a933d2ecfd60d5df0eebd.png)

    ![](media/608845f587627296db79510c1b19e018.png)

    ![](media/27a77ab9fc09c2be93ac5837c6241c3e.png)

    ![](media/e9cec8fa672af325ba0046af989e6979.png)

    ![](media/6b7a3cb0e6041b14f66dbd5a692d67bc.png)

3.  In this step, we will configure the HCX appliance with the information from
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

    ![](media/b85bba096a40c43616f56c8adfbac9d9.png)

    ![](media/69b481bc44f0e0969b82ecf3e8023c81.png)

    ![](media/49535af268151cff5646fc54fc84a995.png)

    ![](media/2f6286c6041ed03162b6b6e76a120e5d.png)

4.  Once done, navigate to Menu \> VM’s and Templates \> Power on the newly
    created HCX Manager VM. The boot process will take 5-10 minutes to complete

## Next Steps

[Module 2 Task 5](module-2-task-5.md)

[Module 2 Index](module-2-index.md)

[Main Index](index.md)