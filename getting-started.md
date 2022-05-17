# Getting Started
- [Getting Started](#getting-started)
  - [**Training Environment**!](#training-environment)
  - [**Azure Credentials**](#azure-credentials)
  - [**Environment Details**](#environment-details)
  - [**Jumpbox Details**](#jumpbox-details)
  - [**AVS Environments**](#avs-environments)
  - [**On-Premises VMware Lab Environment**](#on-premises-vmware-lab-environment)
  - [**Module Configuration Details [Moderators Use]**](#module-configuration-details-moderators-use)
    - [**NSX-T Configuration to use in Module 1**](#nsx-t-configuration-to-use-in-module-1)
    - [**On-Premises HCX details to use in Module 2**](#on-premises-hcx-details-to-use-in-module-2)

## **Training Environment**

## **Azure Credentials**

**Replace “\#” with your group number**

Connect to [**https://portal.azure.com**](https://portal.azure.com) with the
following credentials:

| **Username** | Group**\#**@vmwaresales101outlook.onmicrosoft.com |
|--------------|---------------------------------------------------|
| **Password** | TO BE SUPPLIED                                 |



## **Environment Details**

## **Jumpbox Details**

Your first task should be to create a Jumpbox in your respective Jumpbox Resource group.

** Replace the word 'Name' with Partner name **

| **Group**   | **Jumpbox Resource Group**   | **Virtual Network/Subnet**   |
|------------|------------------------------|------------------------------|
| 1 | GPSUS-Name1-Jumpbox | GPSUS-Name1-VNet/JumpBox |
| 2 | GPSUS-Name2-Jumpbox | GPSUS-Name2-VNet/JumpBox |
| 3 | GPSUS-Name3-Jumpbox | GPSUS-Name3-VNet/JumpBox |
| 4 | GPSUS-Name4-Jumpbox | GPSUS-Name4-VNet/JumpBox |

Please use the following type of VM for the Jumpbox:

> Operating System: Windows 10

> Size: Standard D2s v3 (2vcpus, 8GiB memory)


## **AVS Environments**

### **vCenter, HCX, and NSX-T URLs**

Please refer to the Identity blade in the Azure portal for AVS vCenter, HCX, and NSX-T URLs and Login Information.
** PLEASE DO NOT CLICK GENERATE A NEW PASSWORD BUTTON UNDER CREDENTIALS IN AZURE PORTAL **

**Note**: In a real customer environment, the local
[cloudadmin@vsphere.local](mailto:cloudadmin@vsphere.local) account should be
treated as an emergency access account for "break glass" scenarios in your
private cloud. It's not for daily administrative activities or integration with
other services. For more information see
[here](https://docs.microsoft.com/en-us/azure/azure-vmware/concepts-identity)

## **On-Premises VMware Lab Environment**

If you are in a group with multiple participants you will be assigned a participant number.

### Generic information

| **Group**   | **Participant** | **vCenter IP**     | **Username**                | **Password** | **Web workload IP** | **App Workload IP** |
|-------------|-----------------|--------------------|-----------------------------|--------------|---------------------|---------------------|
| X | Y | 10.X.Y.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.X.101.1/25 | 10.X.10Y.129/25 |

### **Example for Group 1 with 4 participants**

| **Group**   | **Participant** | **vCenter IP**     | **Username**                | **Password** | **Web workload IP** | **App Workload IP** |
|-------------|-----------------|--------------------|-----------------------------|--------------|---------------------|---------------------|
| 1 | 1 | 10.1.1.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.101.1/25 | 10.1.101.129/25 |
| 1 | 2 | 10.1.2.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.102.1/25 | 10.1.102.129/25 |
| 1 | 3 | 10.1.3.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.103.1/25 | 10.1.103.129/25 |
| 1 | 4 | 10.1.4.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.104.1/25 | 10.1.104.129/25 |
  
