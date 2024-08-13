# extend disk lvm

https://packetpushers.net/blog/ubuntu-extend-your-default-lvm-space/

```
df -h 

vgdisplay

lvdisplay

lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv

lvdisplay

resize2fs /dev/ubuntu-vg/ubuntu-lv
```
