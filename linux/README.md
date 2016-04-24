# Linux commands

### Mount drive with specific permissions

```bash
# replace <user>, the device sdxx and the mount directory
sudo mount -o uid=<user>,gid=<user> /dev/sdxx /dir/for/mount
```
