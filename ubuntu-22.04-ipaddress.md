# ubuntu 22.04 ipaddress

```yml
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: false
      dhcp6: false
      optional: true
      addresses: [192.168.6.119/24]
      routes:
         - to: default
           via: 192.168.6.2
      nameservers:
          addresses: [192.168.6.2, 8.8.8.8]
```          

## production office

```yml
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: false
      dhcp6: true
      optional: true
      addresses: [192.168.1.11/24]
      routes:
         - to: default
           via: 192.168.1.1
      nameservers:
          addresses: [8.8.8.8, 192.168.1.1]
```
