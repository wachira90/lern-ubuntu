# lern-ubuntu
lerning ubuntu

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
