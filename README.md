PackStackSandBox
================

Nothing about this is good yet. You have been warned.
Currently have it running in 6GB of memory. 

Requirements
============
Get VirtualBox https://www.virtualbox.org/wiki/Downloads

Get Vagrant https://www.vagrantup.com/downloads.html

Install vagrant-vbguest

    vagrant plugin install vagrant-vbguest

Enable bridged mode on your local machine

    $ brctl show
    bridge name     bridge id               STP enabled     interfaces
    docker0         8000.28d244719f30       no              enp0s25

Get this repo

    git clone git@github.com:Aricg/PackStackSandBox.git && cd PackStackSandBox

Modify Vagrantfile.yml to reflect the name on your bridge and the ips you want to give the virtualbox instnaces 

    bridge: docker0
    controller:
      bridged_ip: 192.168.1.91
      private_ip: 192.168.22.92
    compute:
      bridged_ip: 192.168.1.93
      private_ip: 192.168.22.94

Launch Vagrant
    
    vagrant up

ssh into the vagrant controller (password is vagrant)

    eval $(./parse_yaml Vagrantfile.yml) && ssh root@$controller_bridged_ip

run packstack

    cd /vagrant && ./RunPackstack

I wont include any of the Networking or Launching images in this readme, you can refer to the README.questionable where I have some scripts that bring up and tear down networking
