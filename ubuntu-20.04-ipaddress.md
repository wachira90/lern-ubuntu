# 


## netplan config

### text mode

````
renderer: networkd
````

### gui mode

````
renderer: NetworkManager
````

## /etc/netplan/01-netcfg.yaml

````
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: no
      dhcp6: no
      optional: true
      addresses: [192.168.6.13/24]
      gateway4: 192.168.6.2
      nameservers:
          addresses: [192.168.6.2, 8.8.8.8]

    ens34:
      dhcp4: no
      dhcp6: no
      optional: true

  vlans:
    vlan2:
      id: 2
      link: ens34
      addresses: [10.10.10.1/24]

    vlan3:
      id: 3
      link: ens34
      addresses: [10.10.90.1/24]
````      
