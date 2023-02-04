# lern-ubuntu
lerning ubuntu

## setting ipaddress

NetworkManager = GUI

networkd = TEXTMODE

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
````

## 2 interface


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
      addresses: [192.168.150.1/24]
````


## install agent kvm

````
apt install qemu-guest-agent -y

systemctl status qemu-guest-agent

systemctl enable qemu-guest-agent
````

## change hostname

````
hostnamectl

sudo hostnamectl set-hostname git-push-pda

nano /etc/hosts

reboot
````

## boot with gui

````
systemctl set-default graphical.target
````

## boot with text mode

````
systemctl set-default multi-user.target
````
