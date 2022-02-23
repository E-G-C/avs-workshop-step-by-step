## **Task 8: Create Site Pairing from On-premises HCX to AVS HCX**

In this task, we will be creating the Site Pairing to connect the On-Premises
HCX appliance to the AVS HCX appliance

1.  Sign into your On-Premises vCenter

    1.1.  URL: https://10.X.Y.2

    1.2.  Username:
        administrator@vsphere.local

    1.3.  Password: 0hDG3VqFyTd!


2.  You may see a banner item to Refresh the browser, this will load the newly
    installed HCX modules. If you do not see this, log out and log back into
    vCenter

    ![](media/dd7b93947a327aa2cf9b8c36b7257f3f.png)

3.  Under **Menu**, Select **HCX**

4.  Navigate to Site Pairing \> Connect to Remote Site

    ![](media/a431f8293cc49c568b3f58570bdf9dc2.png)

5.  Enter remote site AVS HCX IP address and login credentials from the Azure
    Portal. See Getting Started section for more details.

    **Note** Ideally the identity provided in this step should be an AD based
    credential with delegation instead of the cloudadmin account.

    ![](media/c31b338dc6e4e88226af7721e2494ab0.png)

6.  Accept certificate warning and Import. Connection to the remote site will be
    established

    ![](media/0d505a16d2c3ac2eae84d5e610b889aa.png)

## Next Steps

[Module 2, Task 9](module-2-task-9.md)

[Module 2 Index](module-2-index.md)

[Main Index](index.md)