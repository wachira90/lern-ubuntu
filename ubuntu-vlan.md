# ubuntu vlan

## backup old config 

````
sudo cp /etc/netplan/01-network-manager-all.yaml /etc/netplan/01-network-manager-all.yaml.bak
# OR
sudo cp /etc/netplan/50-cloud-init.yaml /etc/netplan/50-cloud-init.yaml.bak
````

## default config 

````
network:
    ethernets:
        ens33:
            dhcp4: true
    version: 2
````

````
network:
  version: 2
  renderer: NetworkManager
````  
  

## new setting

````
network:
        version: 2
        renderer: NetworkManager
        ethernets:
             eno2:
              dhcp4: no
              addresses: [192.168.0.100/24]
              gateway4: 192.168.0.1
              nameservers:
                search: [local]
                addresses: [4.2.2.2, 8.8.8.8]
````

## apply config 

````
sudo netplan apply
````

## routing

````
enp0s3:
          dhcp4: no
          dhcp6: no
          addresses: [172.16.1.10/24]
          addresses: [10.1.1.10/24]
          nameservers:
                search: [local]
                addresses: [4.2.2.2, 8.8.8.8]
          routes:
             - to: 0.0.0.0/0
               via: 172.16.1.1
               metric: 10
             - to: 0.0.0.0/0
               via: 10.1.1.1
               metric: 100
````


# Bond interface with VLAN tagged

VLAN ID as 10

````
network:
 version: 2
 renderer: networkd
 ethernets:
     eports:
       match:
         name: ens*
 bonds:
   bond0:
     interfaces: [eports]
     dhcp4: no
     parameters:
       mode: 802.3ad
       lacp-rate: fast
       mii-monitor-interval: 100
 vlans:
   bond0.10:
     id: 10
     link: bond0
     addresses: [10.1.1.10/24]
     gateway4: 10.1.1.1
     nameservers:
       search: [local]
       addresses: [4.2.2.2]
````

## vlan normal

````
network:
  ethernets:
    enp1s0:
      dhcp4: false
      addresses:
        - 192.168.122.201/24
      gateway4: 192.168.122.1
      nameservers:
          addresses: [8.8.8.8, 1.1.1.1]
    vlans:
        enp1s0.100:
            id: 100
            link: enp1s0
            addresses: [192.168.100.2/24]
````

## tag multiple VLAN’s in a Bond using netplan

````
network:
 version: 2
 renderer: networkd
 ethernets:
     eports:
       match:
         name: ens*
 bonds:
   bond0:
     interfaces: [eports]
     dhcp4: no
     parameters:
       mode: 802.3ad
       lacp-rate: fast
       mii-monitor-interval: 100
 vlans:
   bond0.10:
     id: 10
     link: bond0
     addresses: [10.1.1.10/24]
     gateway4: 10.1.1.1
     nameservers:
       search: [local]
       addresses: [4.2.2.2]
 vlans:
   bond0.20:
     id: 20
     link: bond0
     addresses: [10.2.2.10/24]
     gateway4: 10.2.2.1
     nameservers:
       search: [local]
       addresses: [4.2.2.2]
 vlans:
   bond0.30:
     id: 30
     link: bond0
     addresses: [10.3.3.10/24]
     gateway4: 10.3.3.1
     nameservers:
       search: [local]
       addresses: [4.2.2.2]
````



