# Linux commands

### Mount drive with specific permissions

```bash
# replace <user>, the device sdxx and the mount directory
sudo mount -o uid=<user>,gid=<user> /dev/sdxx /dir/for/mount
# if you want an fstab entry
/dev/sda1       /dir/for/mount    ntfs-3g <user>,uid=1000,gid=<user>,umask=0022   0 0
```

### Prevent automount by de deskenv

```bash
gsettings set org.gnome.desktop.media-handling automount false
```
