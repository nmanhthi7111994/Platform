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







