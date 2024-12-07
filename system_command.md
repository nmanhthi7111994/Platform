# Identify the resource used on system
[+]To identify which service is using the port 

```
sudo lsof -i :3306
sudo netstat -tuln | grep 3306
sudo ss -tuln | grep 3306

```
# Increase disk space usage
[+]Identify Large Files and Directories
```
sudo du -ahx / | sort -rh | head -n 20

```

[+]Check for Old Log Files
```
sudo find /var/log -type f -exec du -h {} + | sort -rh | head -n 20

```

[+]Remove Unused Packages
```
sudo apt-get autoremove

```

[+]Remove Temporary Files
```
sudo rm -rf /tmp/*

```
# Connect the target vìa private ssh key

```
chmod 600 /root/.ssh/id_rsa
ssh -i /root/.ssh/id_rsa admin@192.168.1.100

```

## Disable Host Key Checking (if necessary): To prevent prompts for unknown hosts (use cautiously):
```
ssh -i /root/.ssh/id_rsa -o StrictHostKeyChecking=no admin@192.168.1.100
ssh -i /root/.ssh/id_rsa -v admin@192.168.1.100
ssh -A -i /root/.ssh/id_rsa admin@192.168.1.100
```

##  Convert the Key to OpenSSH Format

```
ssh-keygen -p -f id_rsa -m PEM
```
##  Test with Verbose Mode
```
ssh -v -i id_rsa root@10.1.1.1
```

