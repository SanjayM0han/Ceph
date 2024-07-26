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

**Do this step only if you are using LSI/SATA connection (SATA cable conncetion not directly from the motherboard but by LSI module for additional SATA ports for connecting more HDD's).**

* By executing the below we can see the current status of SAS/SATA controller information. check weather it states the status of HDD **Unconfigured(bad)**, if it states like this we have to make it **Unconfigured(good)**.

      ./megaclisas-status

* To make it good we have to excecute the below command. 252 is the LSI card ID,, 7 is the LSI slot number (starts in zero). If it fales to make it good, try rebooting and run the command again.

       megacli -PDMakeGood -PhysDrv[252:7] -a0

* After the HDD status in disk information chnages to **Unconfigured(good)**, the next step is to import the RAID configuration. 
In the LSI card , in order to make them visible to the system as a device (e.g. /dev/sda) each HDD has to be put in RAID0 mode.

        megacli -CfgForeing -Import -a0

* Check the status of the recently HDD `./megaclisas-status` to  confirm **status** is changes to **online**.

* After successfully completing this we can see th HDD is showing in the system `lsblk`.

## 5. Mark OSD IN

After some time… the OSD is changed from the previous host to the new host if you are using **cephadm orchestrator manager**.

Then manually mark **in** to the recently added OSD. 

![image](https://github.com/user-attachments/assets/71b6b735-9b7d-4862-bc0e-b25a48746e79)

![image](https://github.com/user-attachments/assets/22f7aeb0-6d95-4451-a570-00e0af8ca00f)

## 7. Remove NoOut flag       

After all the procedure is over remove the noout flag from cluster wide configuration on the OSD menu

![image](https://github.com/user-attachments/assets/c936900a-b095-44a6-baaa-58316f97df5d)

