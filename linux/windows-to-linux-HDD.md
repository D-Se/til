I want to use my HDD in linux, but it *isnt there*.

```bash
# view all "block devices". Found "sda" is my HDD.
lsblk

# re-build file system
sudo mkfs -t ext4 /dev/sda

# puts a directory inside /media folder
sudo mount /dev/sda

# found the path of the mountpoint
lsblk | grep -e "sda" | awk '{print $7}'

# Claim ownership to actually use the drive
sudo chown username:username /media/username/mountpoint
```