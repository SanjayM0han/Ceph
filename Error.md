# Errors
## 13 Jul 2024
### Dashboard is only availing in floating Ip 


![cba4ac2b-eff8-4a1c-a41e-5b443c96e95c](https://github.com/user-attachments/assets/31d8a807-8596-433e-b355-007144a9de38)

## 16 Jul 2024
## Upgrade Redeploy Daemon error
[ERR] Upgrade: Paused due to UPGRADE_REDEPLOY_DAEMON: Upgrading daemon mgr.cephtest-3.okswrg on host cephtest-3 failed.
This error persists in the upgradation process after getting this error the whole upgradation process will be stuck trying to figure out what is the error

![image](https://github.com/user-attachments/assets/82df3f4b-7488-41c9-abf7-9cec7c169fa0)

## 17 Jul 2024
### Solution Upgrade Redeploy Daemon error
Actually the update to mgr daemon is successful but it shows error since it can't be restarted . Daemon restart and systemctl doesn't work here , after rebooting the host it shows the daemon is updated.Rest of the update is done by specifying the daemon and the host machines


