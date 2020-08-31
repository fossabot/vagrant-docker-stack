# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/bionic64"
  config.vm.box_check_update = true

  # Bridge the interface here
  config.vm.network "public_network", bridge: "en0: Wi-Fi (Wireless)"
  config.vm.synced_folder "workspace", "/home/vagrant/data"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "vagrant-docker-devstack"
    vb.gui = false
    vb.memory = "4096"
  end
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get upgrade -y
    apt-get install -y apt-transport-https ca-certificates curl software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
    add-apt-repository -y "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
    apt-get update
    apt-cache policy docker-ce
    apt-get install -y docker-ce
    systemctl enable docker
    systemctl start docker
    usermod -aG docker vagrant
    systemctl restart docker
    systemctl status docker
    docker -v
    reboot
  SHELL
end