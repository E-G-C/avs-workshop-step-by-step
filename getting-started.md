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

| **Name**                    | **Resource Group**          | **Username** | **Password** |
|-----------------------------|-----------------------------|--------------|--------------|
| GROUP-\#-AVS-jumpbox | GROUP-\#-AVS-JUMPBOX | avsjump      | AVS\#r0cks!    |




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
| AVS8 | GROUP08-SDDC | GROUP08-PrivateCloud | cloudadmin@vsphere.local | 8@z$792OfIno | admin | trrHx0E8%83* |
| AVS9 | GROUP9-SDDC | GROUP9-PrivateCloud | cloudadmin@vsphere.local | $yjRy5902n-A | admin | 6z8^9uvj#9WP |
| AVS10 | GROUP10-SDDC | GROUP10-PrivateCloud | cloudadmin@vsphere.local | &g097D4b!Pnq | admin | yc3jP1%N4#b7 |

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
| AVS8 | https://10.108.0.2/ | https://10.108.0.3/ | https://10.108.0.9/ |
| AVS9 | https://10.109.0.2/ | https://10.109.0.3/ | https://10.109.0.9/ |
| AVS10 | https://10.110.0.2/ | https://10.110.0.3/ | https://10.110.0.9/ |

**Note**: In a real customer environment, the local
[cloudadmin@vsphere.local](mailto:cloudadmin@vsphere.local) account should be
treated as an emergency access account for "break glass" scenarios in your
private cloud. It's not for daily administrative activities or integration with
other services. For more information see
[here](https://docs.microsoft.com/en-us/azure/azure-vmware/concepts-identity)

## **On-Premises VMware Lab Environment**

If you are in a group with multiple participants you will be assigned a participant number. For example, Group 1, Participant 4, will be equivalent to 14 for the third octate in the IP addresses (where the X is the group number, Y is the participant number)

<span style="color:green">X = Group Number</span>
<span style="color:green">Y = Participant Number</span>

| **Name**   | **vCenter IP**     | **Username**                | **Password** |
|------------|--------------------|-----------------------------|--------------|
| GROUP **X** | 192.168.**X**.2/24 | administrator@vsphere.local | 0hDG3VqFyTd! |
