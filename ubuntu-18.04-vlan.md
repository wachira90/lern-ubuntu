# ubuntu-18.04-vlan

## install package
```
apt install vlan -y
```

## test temporary

```
sudo modprobe 8021q
sudo vconfig set_name_type VLAN_PLUS_VID_NO_PAD
sudo vconfig add enp2s0 7
sudo ip addr add 192.168.6.201/24 dev vlan7
sudo ip link set up vlan7
```

## add permanent

```
modprobe 8021q
```

## check mod

```
modinfo 8021q
```

## result

```
root@host1:~# modinfo 8021q
filename:       /lib/modules/4.15.0-112-generic/kernel/net/8021q/8021q.ko
version:        1.8
license:        GPL
alias:          rtnl-link-vlan
srcversion:     F58D0224081805F5E76DEB8
depends:        mrp,garp
retpoline:      Y
intree:         Y
name:           8021q
vermagic:       4.15.0-112-generic SMP mod_unload
signat:         PKCS#7
signer:
sig_key:
sig_hashalgo:   md4
root@host1:~#
```

## nano /etc/netplan/01-netcfg.yaml

```
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: no
      dhcp6: no
      addresses: [192.168.6.13/24]
      gateway4: 192.168.6.2
      nameservers:
          addresses: [192.168.6.2, 8.8.8.8]

    ens34:
      dhcp4: no
      dhcp6: no

  vlans:
    vlan2:
      id: 2
      link: ens34
      addresses: [10.10.10.1/24]

    vlan3:
      id: 3
      link: ens34
      addresses: [10.10.90.1/24]
```

## apply config

```
netplan apply
```


## network bridge interface on top of vlan

```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp2s0:
      dhcp4: no
      dhcp6: no

  bridges:
    br0:
      dhcp4: no
      dhcp6: no
      interfaces:
        - enp2s0
      addresses: [ 192.168.6.17/25 ]
      gateway4: 192.168.6.1
      nameservers:
          addresses:
              - "192.100.77.10"
  vlans:
    vlan7:
      id: 7
      link: enp2s0

  bridges:
    br1:
      dhcp4: no
      dhcp6: no
      interfaces:
        - vlan7
      addresses: [ 192.168.6.201/25 ]
      gateway4: 192.168.6.129
```
