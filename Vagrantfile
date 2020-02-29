# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.
  config.vm.define "master" do |master|
      # Every Vagrant development environment requires a box. You can search for
      # boxes at https://vagrantcloud.com/search.
      master.vm.box = "packer/ver3.box"

      master.vm.box_check_update = false
   
      # Create a forwarded port mapping which allows access to a specific port
      # within the machine from a port on the host machine. In the example below,
      # accessing "localhost:8080" will access port 80 on the guest machine.
      master.vm.network "forwarded_port", guest: 6443, host: 6443

      # Create a private network, which allows host-only access to the machine
      # using a specific IP.
      master.vm.network "private_network", ip: "192.168.33.10"

      # config.vm.synced_folder "../data", "/vagrant_data"
    
      master.vm.provider "virtualbox" do |vb|
         vb.memory = "2048"
         vb.cpus = 1
      end
 
      master.vm.provision "file", source: "config/hosts", destination: "/tmp/hosts"

      master.vm.provision "shell", inline: <<-SHELL
	hostnamectl set-hostname kubeadm-master
	hostnamectl status
	sudo mv /tmp/hosts /etc/hosts
        sudo yum -y install epel-release
        sudo yum -y install htop
        sudo bash -c 'echo "echo 1 > /proc/sys/net/bridge/bridge-nf-call-iptables" >> /etc/rc.local'
	sudo chmod a+x /etc/rc.local
        sudo systemctl enable kubelet
      SHELL
  end

  config.vm.define "worker1" do |w1|
      # Every Vagrant development environment requires a box. You can search for
      # boxes at https://vagrantcloud.com/search.
      w1.vm.box = "packer/ver3.box"

      w1.vm.box_check_update = false
   
      # Create a forwarded port mapping which allows access to a specific port
      # within the machine from a port on the host machine. In the example below,
      # accessing "localhost:8080" will access port 80 on the guest machine.
      #w1.vm.network "forwarded_port", guest: 6443, host: 6443

      # Create a private network, which allows host-only access to the machine
      # using a specific IP.
      w1.vm.network "private_network", ip: "192.168.33.11"

      # config.vm.synced_folder "../data", "/vagrant_data"
    
      w1.vm.provider "virtualbox" do |vb|
         vb.memory = "2048"
         vb.cpus = 1
      end
 
      w1.vm.provision "file", source: "config/hosts", destination: "/tmp/hosts"

      w1.vm.provision "shell", inline: <<-SHELL
	hostnamectl set-hostname kubeadm-worker1
	hostnamectl status
	sudo mv /tmp/hosts /etc/hosts
        sudo yum -y install epel-release
        sudo yum -y install htop
        sudo bash -c 'echo "echo 1 > /proc/sys/net/bridge/bridge-nf-call-iptables" >> /etc/rc.local'
	sudo chmod a+x /etc/rc.local
        sudo systemctl enable kubelet
      SHELL
  end

  config.vm.define "worker2" do |w1|
      # Every Vagrant development environment requires a box. You can search for
      # boxes at https://vagrantcloud.com/search.
      w1.vm.box = "packer/ver3.box"

      w1.vm.box_check_update = false
   
      # Create a forwarded port mapping which allows access to a specific port
      # within the machine from a port on the host machine. In the example below,
      # accessing "localhost:8080" will access port 80 on the guest machine.
      #w1.vm.network "forwarded_port", guest: 6443, host: 6443

      # Create a private network, which allows host-only access to the machine
      # using a specific IP.
      w1.vm.network "private_network", ip: "192.168.33.12"

      # config.vm.synced_folder "../data", "/vagrant_data"
    
      w1.vm.provider "virtualbox" do |vb|
         vb.memory = "2048"
         vb.cpus = 1
      end
      
      w1.vm.provision "file", source: "config/hosts", destination: "/tmp/hosts"

      w1.vm.provision "shell", inline: <<-SHELL
	hostnamectl set-hostname kubeadm-worker2
	hostnamectl status
	sudo mv /tmp/hosts /etc/hosts
        sudo yum -y install epel-release
        sudo yum -y install htop
        sudo bash -c 'echo "echo 1 > /proc/sys/net/bridge/bridge-nf-call-iptables" >> /etc/rc.local'
	sudo chmod a+x /etc/rc.local
        sudo systemctl enable kubelet
      SHELL
  end

end
