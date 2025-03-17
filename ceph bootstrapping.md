# Installetion of Ceph
Minimal installation of ceph and depending on podman for getting the clean host.

Here we uses parallel command execution - which enables us to parallely sent a command froma a single machone to multiple machines at the same time. `sudo apt install pdsh`

## 1. Install cephadm 
Before installing you have the update the system  `pdsh -R ssh -w 192.168.85.[1-5] sudo apt update && sudo apt -y upgrade`

    apt install cephadm

## 2. Install podman
Docker should be uninstalled only after installing cephadm. After that install podman on all the hosts at sam etime usingb pdsh 

    pdsh -R ssh -w 192.168.85.[1-5] apt remove docker.io && apt install podman
    
## 3. Bootstrapping

    cephadm --image quay.io/ceph/ceph:v17.2.7  bootstrap --mon-ip <ip of host>

 Or 
 If you has a cluster network add it also while bootstarpping

    cephadm --image quay.io/ceph/ceph:v17.2.7  bootstrap --mon-ip <ip of host> --cluster-network <cluster network ip address> 

After bootstrapping is comnpleted successfully, don't forget to note down the ip addess , username and password.
admin user password , ip add

Try to login to the dashboard using the username and password we got from the bootstrapping process.

## 4. Preparing other host

 All the machines should be able to ssh to root as passwordless login. 

- Enable **PermitRootLogin**  to  **yes** on sshd_config ' nano /etc/ssh/sshd_config '
- Set password for root user ' passwd '
- Restart ssh service 'sudo service ssh restart'
- copy generated ceph pub key to all other hosts
  ```
  for i in [1-5]
  do
	  ssh-copy-id -f -i /etc/ceph/ceph.pub root@192.168.85.$i
  done
  ```

- Pull ceph images from the docker

      podman pull quay.io/ceph/ceph:v17.2.0

## 5. Adding hosts

then add the nodes, use the private cluster network if any

```
for i in [1-5]
do
	ceph orch host add node$i 192.168.85.$i
done
```

## 6. Adding OSD
- To add all the available osd to add. Use the command:

      ceph orch apply osd --all-available-devices
- To add the OSD specifically. Run the command:

      ceph orch daemon add osd cephtest:/dev/sdb

### Remove OSD

- It is needed to clean up the removed OSD by executing:
 
		ceph orch daemon rm osd.<id>
 
- If needed, also wipe the disk:
 
		cephadm ceph-volume lvm zap --destroy --osd-id <id>
