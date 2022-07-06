$script = <<-SCRIPT
sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
dnf -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
timedatectl set-timezone America/Sao_Paulo
dnf -y update
dnf -y install htop
dnf -y install nginx
systemctl start nginx
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.define "centos" do |centos|
    centos.vm.box = "centos/8"
    centos.vm.network "public_network", ip: "192.168.1.100"
     #centos.vm.network "forwarded_port", guest: 80, host:8080
    #centos.vm.network "private_network", ip: "192.168.56.5"
    #centos.vm.network "private_network", type: "dhcp"
    #centos.vm.synced_folder "./scripts", "/scripts"
    centos.vm.provision "shell", inline: $script
    centos.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
      v.name = "centos8"
    end
  end
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/focal64"
    ubuntu.vm.network "public_network", ip: "192.168.1.100"
    #ubuntu.vm.network "forwarded_port", guest: 80, host:8080
    #ubuntu.vm.network "private_network", ip: "192.168.1.200"
    #ubuntu.vm.network "private_network", type: "dhcp"
    #ubuntu.vm.synced_folder "./scripts", "/scripts"
    #ubuntu.vm.provision "shell", path: "/home/jl/vagrant/scripts/provisioner.sh"
    ubuntu.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
      v.name = "server01"
     end
  end
end