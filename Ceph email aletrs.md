# Ceph Email Alerts
The alerts module can send simple alert messages about cluster health via e-mail. 

There I am using gmail acoount for SMTP configuration 
## 1. Enable alert module
Enable the alert service from mgr module

    sudo ceph mgr module enable alerts
## 2. Configuration
These commands will enable alerts module and configure stmp server to use with sender and receiver information.

### SMTP configuration for gmail account

- Go to your [google account settings](https://myaccount.google.com/) and search for **app passwords**  

![image](https://github.com/kashinathshabu/Ceph/assets/67222565/6a0c6078-ac7e-4f4f-9e70-d851c16b7ae5)

- Type App name and click **Create**

![image](https://github.com/kashinathshabu/Ceph/assets/67222565/87e91e01-5f92-4cdc-8ccb-61c6f3851485)

- Copy the **Generated Password** . Dont forget to **remove** the **space in between** them while pasting it anywhere
  
![image](https://github.com/kashinathshabu/Ceph/assets/67222565/cb3ea34e-06c9-451e-8752-dcdbf0468de1)


```
sudo ceph config set mgr mgr/alerts/smtp_host [smtp host name]
sudo ceph config set mgr mgr/alerts/smtp_port [port number]
sudo ceph config set mgr mgr/alerts/smtp_ssl [True/False]
sudo ceph config set mgr mgr/alerts/smtp_destination [to@example.com]
sudo ceph config set mgr mgr/alerts/smtp_sender [from@example.com] 
sudo ceph config set mgr mgr/alerts/smtp_from_name [sender name]  #default name will be Ceph
sudo ceph config set mgr mgr/alerts/smtp_user [gmail account]
sudo ceph config set mgr mgr/alerts/smtp_password [app password]
```

Example:

```
sudo ceph config set mgr mgr/alerts/smtp_host smtp.gmail.com
sudo ceph config set mgr mgr/alerts/smtp_port 465
sudo ceph config set mgr mgr/alerts/smtp_ssl true
sudo ceph config set mgr mgr/alerts/smtp_destination kashinath@gmail.com
sudo ceph config set mgr mgr/alerts/smtp_sender cephadmin@gmail.com 
sudo ceph config set mgr mgr/alerts/smtp_from_name Ceph_Admin
sudo ceph config set mgr mgr/alerts/smtp_user cephadmin@gmail.com
sudo ceph config set mgr mgr/alerts/smtp_password 547896321458525
```
## 3. Sending a test email
Sent a test email to test its working or not 

    sudo ceph alerts send


## 4. To disable it :

    sudo ceph mgr module disable alerts
