# ansible-VM

## Description
This is the playbook for configuring nginx and deploying from control machine to remote/host machine using virtual machines.

## Setting up Virtual machines 
- Create two VMs in Virtual Box and install ubuntu.
- Configure network settings on both VMs as 'host only ethernet adapter' and also attach NAT.

## Configuring Control machine
Control machine requires ansible to provision on target or remote machine.
### Install ansible
- `sudo apt-get update`
- `sudo apt-install software-properties-common`
- `sudo apt-add-repository ppa:ansible/ansible`
- `sudo apt-get update`
- `sudo apt-get install ansible`

## Configuring Remote/Host machine
- Remote machine requires python. To install python `sudo apt-get install python`
- It also needs ssh server because remote nodes communicates via ssh, `sudo apt-get install openssh-server`

## Create ssh connection
- On control machine generate ssh keys as `ssh-keygen`
- Then you need to copy the public key into remote machine by `ssh-copy-id -i host@192.168.56.103`. *Hostname and ip address can be diffrent to mine*.

## Add inventory host
- Go to host file.`sudo nano /etc/ansible/hosts`
- Add host/remote machine's ip address in order to deploy playbook.for eg: 
  ``` [test-server]
      host@192.168.56.103
  ```
 - Above 'test-server' is the name of web-server. It can contain group of servers and can be used to deploy on multiple machines        respective to IP addresses. To check *IP adress*of a machine,type `ifconfig`on terminal.
 
 ## To check if control machine connects to remote through ansible(test if 'test-server' is running)
 `ansible -m ping 'test-server`
 
 ## Use the playbook as above and run it as `ansible-playbook nginx.yml`
 
 If it is successful with no failures, you can check on remote machine if nginx is installed by `ps waux | grep nginx`
 
          


