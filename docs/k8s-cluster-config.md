# Network Adapter, Ansible controller Node and Kubernetes Cluster configuration on Virtalbox


## Configure network between hosts

### Configure network adapter

    1. Open VirtualBox
    2. Select "Tools" in left pane
    3. Select Host-only Networks
    4. Click on "Create" in right pane
    5. Select Newly Created Host-only Network
    6. Click on "Properties" in right pane
    7. Select "Configure Adapter Manually" in the Adapter Tab from the bottom pane.
    8. Put IP Address and netmask manually ( i.e IP: 192.168.60.1 Netmask: 255.255.255.0)
    9. Don't enable DHCP

### Configure network in VM

    1. Select VM 2 Click Settings on right pane
    2. Select Network
    3. Adapter 1 attached to NAT // it is for internet
    4. Adapter 2 attached to Host-only Adapter and choose your pre configured Host-only adapter name


# Hosts Hardware Configuration


# Check sudo access in all node
It will show the all access 
pkjana@control-plane-1:~$ sudo -l
[sudo] password for pkjana:
Matching Defaults entries for pkjana on control-plane-1:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, use_pty

User pkjana may run the following commands on control-plane-1:
    (ALL : ALL) ALL
pkjana@control-plane-1:~$

# IP and Hostname assign to the host

## Ansible controller Node    
	
	192.168.60.10 ansible-controller
	
## Ansible Managed Nodes ( A Kubernetes Cluster)	

    192.168.60.101 control-plane-1
	192.168.60.102 control-plane-2
	192.168.60.103 control-plane-3
		
	192.168.60.201 worker-node-1
	192.168.60.202 worker-node-2
	192.168.60.203 worker-node-3
	192.168.60.204 worker-node-4
	
	
Modify the IP Addresses in each node as per above in the file below. 	

pkjana@control-plane-1:~$ sudo cat /etc/netplan/50-cloud-init.yaml

root@control-plane-1:~# cat /etc/netplan/50-cloud-init.yaml
# This file is generated from information provided by the datasource.  Changes
# to it will not persist across an instance reboot.  To disable cloud-init's
# network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
```yaml
network:
    ethernets:
        enp0s3:
            dhcp4: true
        enp0s8:
            addresses:
            - 192.168.60.101/24
            nameservers:
                addresses: []
                search: []
    version: 2
```
root@control-plane-1:~# vi /etc/netplan/50-cloud-init.yaml


Testing the Configuration
	
    $ sudo netplan try
	
The New configuration can then be applied using the netplan command.
	
    $ sudo netplan apply

Confirm the IP configured successfully or not

    $ ip a


# Configure Hostname for each host

## Configure Hostname by CLI Command

Check Current Hostname
$ hostname
$ hostnamectl    //To display both the hostname and additional information about your system

Change Hostname on Ubuntu via CLI (No Reboot required)
$ sudo hostnamectl set-hostname <host-name>

Confirm the Change
S hostname

## Change Hostname on Ubuntu via CLI (Reboot Required)

Step 1: Open /etc/hostname and Change the Hostname

    $ sudo vim /etc/hostname

Step 2: Open /etc/hosts and Change the Hostname

$ sudo vim /etc/hosts
127.0.0.1    localhost
127.0.0.1    <new hostname>

Save the edits and exit. Reboot the System to apply the changes

# Change Hostname on Ubuntu via GUI
 Settings -> About -> Click on Device Name -> Rename Device 

# Temporarily Change Hostname on Ubuntu (optional)
$ sudo hostname <new-hostname>


# Add the ip hostname mappiing in the all host which will communicate each other. As per above ip hostname mapping.
$ sudo nano /etc/hosts
<ip> <host-name>
<ip> <host-name>

Ping each node successfully
$ ping <ip>
$ ping <host-name>

