# Placing HDD from a host to another host

*If we want interchange or to place a using HDD on another host without changing the osd number and the other details, we have to do some couple of steps.*  

## 1. Change flag

Firstly we want to mark **No Out** flag from the cluster wise configuaration option on the OSD menu.   

![image](https://github.com/user-attachments/assets/458b9919-254d-4651-9607-1cbf2153e71e)

![image](https://github.com/user-attachments/assets/cd8f1e30-f3f3-45a8-a440-4fbfa1a307c8)


## 2. Disconnect HDD 

Then, we want to remove the HDD from the host for placing it on another host. 

## 3. Connect it to the new host machine

Connect the previously removed HDD to this new host by Connecting the SATA cable and the SATA power cables.

## 4. Additional (LSI/SATA) !

**Do this step only if you are using LSI/SATA connection (SATA cable conncetion not directly from the motherboard but by LSI module for adding SATA ports to connecting more HDD's).**

By executing the below we can see the current status of SAS/SATA controller information 

    ./megaclisas-status

252 is the LSI card ID,, 7 is the LSI slot number (starts in zero)

    megacli -PDMakeGood -PhysDrv[252:7] -a0

If it fales to make it good, try rebooting
