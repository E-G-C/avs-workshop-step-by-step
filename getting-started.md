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

Size VM: 

| **Name**   | **Jumpbox Resource Group**   | **Virtual Network/Subnet**   |
|------------|------------------------------|------------------------------|
| AVS1 | GROUP1-AVS-SDDC-Jumpbox | GROUP1-AVS-SDDC-VNet/JumpBox |
| AVS2 | GROUP-2-AVS-SDDC-Jumpbox | GROUP-2-AVS-SDDC-VNet/JumpBox |
| AVS3 | GROUP3-AVS-SDDC-Jumpbox | GROUP3-AVS-SDDC-VNet/JumpBox |
| AVS4 | GROUP4-AVS-SDDC-Jumpbox | GROUP4-AVS-SDDC-VNet/JumpBox |
| AVS5 | GROUP-5-Jumpbox | GROUP-5-VNet/JumpBox |
| AVS6 | GROUP-6-Jumpbox | GROUP-6-VNet/JumpBox |
| AVS7 | GROUP-7-Jumpbox | GROUP-7-VNet/JumpBox |

Please use the following type of VM for the Jumpbox:

> Operating System: Windows 10

> Size: Standard D2s v3 (2vcpus, 8GiB memory)


## **AVS Environments**

| **Name**   | **Resource Name**   | **Resource Group**   | **vCenter Username**   | **vCenter Password**   | **NSX-T user**   | **NSX-T password**   |
|------------|---------------------|----------------------|------------------------|------------------------|------------------|----------------------|
| AVS1 | GROUP1-AVS-SDDC-SDDC | GROUP1-AVS-SDDC-PrivateCloud | cloudadmin@vsphere.local | 6aO@P*6fa69u | admin | *Za0^k21h7xO |
| AVS2 | GROUP-2-AVS-SDDC-SDDC | GROUP-2-AVS-SDDC-PrivateCloud | cloudadmin@vsphere.local | epB6j@E27k8% | admin | Y5zr9-#2m6nH |
| AVS3 | GROUP3-AVS-SDDC-SDDC | GROUP3-AVS-SDDC-PrivateCloud | cloudadmin@vsphere.local | *o4y91E1^ptS | admin | 8i1qY%1Shp-2 |
| AVS4 | GROUP4-AVS-SDDC-SDDC | GROUP4-AVS-SDDC-PrivateCloud | cloudadmin@vsphere.local | 03(V)4lB8nyk | admin | 6IO-s76jl3#n |
| AVS5 | GROUP-5-SDDC | GROUP-5-PrivateCloud | cloudadmin@vsphere.local | 5-1pr3SFv-4z | admin | u12%EF1#jfe6 |
| AVS6 | GROUP-6-SDDC | GROUP-6-PrivateCloud | cloudadmin@vsphere.local | )bH0x66pD@v1 | admin | k8g&01n)0xIH |
| AVS7 | GROUP-7-SDDC | GROUP-7-PrivateCloud | cloudadmin@vsphere.local | (6oae13)f5YR | admin | -4g871v)thAZ |


### **vCenter, HCX, and NSX-T URLs**

| **Name**   | **vCenter URL**   | **NSX-T URL**   | **HCX URL**   |
|------------|-------------------|-----------------|---------------|
| AVS1 | https://10.101.0.2/ | https://10.101.0.3/ | https://10.101.0.9/ |
| AVS2 | https://10.102.0.2/ | https://10.102.0.3/ | https://10.102.0.9/ |
| AVS3 | https://10.103.0.2/ | https://10.103.0.3/ | https://10.103.0.9/ |
| AVS4 | https://10.104.0.2/ | https://10.104.0.3/ | https://10.104.0.9/ |
| AVS5 | https://10.105.0.2/ | https://10.105.0.3/ | https://10.105.0.9/ |
| AVS6 | https://10.106.0.2/ | https://10.106.0.3/ | https://10.106.0.9/ |
| AVS7 | https://10.107.0.2/ | https://10.107.0.3/ | https://10.107.0.9/ |


**Note**: In a real customer environment, the local
[cloudadmin@vsphere.local](mailto:cloudadmin@vsphere.local) account should be
treated as an emergency access account for "break glass" scenarios in your
private cloud. It's not for daily administrative activities or integration with
other services. For more information see
[here](https://docs.microsoft.com/en-us/azure/azure-vmware/concepts-identity)

## **On-Premises VMware Lab Environment**

If you are in a group with multiple participants you will be assigned a participant number.

<span style="color:green">X = Group Number</span>
<span style="color:green">Y = Participant Number</span>

### **Group 1**

| **Group**   | **Participant** | **vCenter IP**     | **Username**                | **Password** | **Web workload IP** | **App Workload IP** |
|-------------|-----------------|--------------------|-----------------------------|--------------|---------------------|---------------------|
| 1 | 1 | 10.1.1.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.11.1/25 | 10.1.11.129/25 |
| 1 | 2 | 10.1.2.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.12.1/25 | 10.1.12.129/25 |
| 1 | 3 | 10.1.3.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.13.1/25 | 10.1.13.129/25 |
| 1 | 4 | 10.1.4.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.14.1/25 | 10.1.14.129/25 |
| 1 | 5 | 10.1.5.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.15.1/25 | 10.1.15.129/25 |
| 1 | 6 | 10.1.6.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.16.1/25 | 10.1.16.129/25 |
| 1 | 7 | 10.1.7.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.17.1/25 | 10.1.17.129/25 |
| 1 | 8 | 10.1.8.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.18.1/25 | 10.1.18.129/25 |
| 1 | 9 | 10.1.9.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.19.1/25 | 10.1.19.129/25 |
| 1 | 10 | 10.1.10.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.1.20.1/25 | 10.1.20.129/25 |

### **Group 2**

| **Group**   | **Participant** | **vCenter IP**     | **Username**                | **Password** | **Web workload IP** | **App Workload IP** |
|-------------|-----------------|--------------------|-----------------------------|--------------|---------------------|---------------------|
| 2 | 1 | 10.2.1.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.2.11.1/25 | 10.2.11.129/25 |
| 2 | 2 | 10.2.2.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.2.12.1/25 | 10.2.12.129/25 |
| 2 | 3 | 10.2.3.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.2.13.1/25 | 10.2.13.129/25 |
| 2 | 4 | 10.2.4.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.2.14.1/25 | 10.2.14.129/25 |
| 2 | 5 | 10.2.5.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.2.15.1/25 | 10.2.15.129/25 |
| 2 | 6 | 10.2.6.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.2.16.1/25 | 10.2.16.129/25 |
| 2 | 7 | 10.2.7.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.2.17.1/25 | 10.2.17.129/25 |
| 2 | 8 | 10.2.8.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.2.18.1/25 | 10.2.18.129/25 |
| 2 | 9 | 10.2.9.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.2.19.1/25 | 10.2.19.129/25 |
| 2 | 10 | 10.2.10.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.2.20.1/25 | 10.2.20.129/25 |

### **Group 3**

| **Group**   | **Participant** | **vCenter IP**     | **Username**                | **Password** | **Web workload IP** | **App Workload IP** |
|-------------|-----------------|--------------------|-----------------------------|--------------|---------------------|---------------------|
| 3 | 1 | 10.3.1.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.3.11.1/25 | 10.3.11.129/25 |
| 3 | 2 | 10.3.2.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.3.12.1/25 | 10.3.12.129/25 |
| 3 | 3 | 10.3.3.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.3.13.1/25 | 10.3.13.129/25 |
| 3 | 4 | 10.3.4.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.3.14.1/25 | 10.3.14.129/25 |
| 3 | 5 | 10.3.5.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.3.15.1/25 | 10.3.15.129/25 |
| 3 | 6 | 10.3.6.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.3.16.1/25 | 10.3.16.129/25 |
| 3 | 7 | 10.3.7.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.3.17.1/25 | 10.3.17.129/25 |
| 3 | 8 | 10.3.8.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.3.18.1/25 | 10.3.18.129/25 |
| 3 | 9 | 10.3.9.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.3.19.1/25 | 10.3.19.129/25 |
| 3 | 10 | 10.3.10.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.3.20.1/25 | 10.3.20.129/25 |

### **Group 4**

| **Group**   | **Participant** | **vCenter IP**     | **Username**                | **Password** | **Web workload IP** | **App Workload IP** |
|-------------|-----------------|--------------------|-----------------------------|--------------|---------------------|---------------------|
| 4 | 1 | 10.4.1.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.4.11.1/25 | 10.4.11.129/25 |
| 4 | 2 | 10.4.2.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.4.12.1/25 | 10.4.12.129/25 |
| 4 | 3 | 10.4.3.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.4.13.1/25 | 10.4.13.129/25 |
| 4 | 4 | 10.4.4.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.4.14.1/25 | 10.4.14.129/25 |
| 4 | 5 | 10.4.5.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.4.15.1/25 | 10.4.15.129/25 |
| 4 | 6 | 10.4.6.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.4.16.1/25 | 10.4.16.129/25 |
| 4 | 7 | 10.4.7.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.4.17.1/25 | 10.4.17.129/25 |
| 4 | 8 | 10.4.8.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.4.18.1/25 | 10.4.18.129/25 |
| 4 | 9 | 10.4.9.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.4.19.1/25 | 10.4.19.129/25 |
| 4 | 10 | 10.4.10.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.4.20.1/25 | 10.4.20.129/25 |

### **Group 5**

| **Group**   | **Participant** | **vCenter IP**     | **Username**                | **Password** | **Web workload IP** | **App Workload IP** |
|-------------|-----------------|--------------------|-----------------------------|--------------|---------------------|---------------------|
| 5 | 1 | 10.5.1.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.5.11.1/25 | 10.5.11.129/25 |
| 5 | 2 | 10.5.2.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.5.12.1/25 | 10.5.12.129/25 |
| 5 | 3 | 10.5.3.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.5.13.1/25 | 10.5.13.129/25 |
| 5 | 4 | 10.5.4.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.5.14.1/25 | 10.5.14.129/25 |
| 5 | 5 | 10.5.5.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.5.15.1/25 | 10.5.15.129/25 |
| 5 | 6 | 10.5.6.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.5.16.1/25 | 10.5.16.129/25 |
| 5 | 7 | 10.5.7.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.5.17.1/25 | 10.5.17.129/25 |
| 5 | 8 | 10.5.8.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.5.18.1/25 | 10.5.18.129/25 |
| 5 | 9 | 10.5.9.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.5.19.1/25 | 10.5.19.129/25 |
| 5 | 10 | 10.5.10.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.5.20.1/25 | 10.5.20.129/25 |

### **Group 6**

| **Group**   | **Participant** | **vCenter IP**     | **Username**                | **Password** | **Web workload IP** | **App Workload IP** |
|-------------|-----------------|--------------------|-----------------------------|--------------|---------------------|---------------------|
| 6 | 1 | 10.6.1.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.6.11.1/25 | 10.6.11.129/25 |
| 6 | 2 | 10.6.2.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.6.12.1/25 | 10.6.12.129/25 |
| 6 | 3 | 10.6.3.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.6.13.1/25 | 10.6.13.129/25 |
| 6 | 4 | 10.6.4.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.6.14.1/25 | 10.6.14.129/25 |
| 6 | 5 | 10.6.5.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.6.15.1/25 | 10.6.15.129/25 |
| 6 | 6 | 10.6.6.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.6.16.1/25 | 10.6.16.129/25 |
| 6 | 7 | 10.6.7.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.6.17.1/25 | 10.6.17.129/25 |
| 6 | 8 | 10.6.8.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.6.18.1/25 | 10.6.18.129/25 |
| 6 | 9 | 10.6.9.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.6.19.1/25 | 10.6.19.129/25 |
| 6 | 10 | 10.6.10.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.6.20.1/25 | 10.6.20.129/25 |

### **Group 7**

| **Group**   | **Participant** | **vCenter IP**     | **Username**                | **Password** | **Web workload IP** | **App Workload IP** |
|-------------|-----------------|--------------------|-----------------------------|--------------|---------------------|---------------------|
| 7 | 1 | 10.7.1.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.7.11.1/25 | 10.7.11.129/25 |
| 7 | 2 | 10.7.2.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.7.12.1/25 | 10.7.12.129/25 |
| 7 | 3 | 10.7.3.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.7.13.1/25 | 10.7.13.129/25 |
| 7 | 4 | 10.7.4.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.7.14.1/25 | 10.7.14.129/25 |
| 7 | 5 | 10.7.5.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.7.15.1/25 | 10.7.15.129/25 |
| 7 | 6 | 10.7.6.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.7.16.1/25 | 10.7.16.129/25 |
| 7 | 7 | 10.7.7.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.7.17.1/25 | 10.7.17.129/25 |
| 7 | 8 | 10.7.8.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.7.18.1/25 | 10.7.18.129/25 |
| 7 | 9 | 10.7.9.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.7.19.1/25 | 10.7.19.129/25 |
| 7 | 10 | 10.7.10.2 |administrator@vsphere.local | 0hDG3VqFyTd! | 10.7.20.1/25 | 10.7.20.129/25 |
