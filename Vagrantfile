# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|  
  config.vm.box = "centos-7.0-64"

  config.vbguest.auto_update = false
   
  config.vm.provision "file",
    source: "C:\\dev\\vagrant\\vagrant-init\\files\\git-config",
    destination: "~/.gitconfig"

  config.vm.provision "shell",
    path: "https://raw.githubusercontent.com/runnerdave/vagrant-init/master/scripts/centos-common.sh"

  config.vm.define "web" do |web|
    web.vm.hostname = "web-server"
    web.vm.network "forwarded_port", guest: 80, host: 8899

    web.vm.network "private_network", ip: "192.168.10.2"

    web.vm.provision "shell",
    path: "https://raw.githubusercontent.com/runnerdave/vagrant-init/master/scripts/centos-web.sh"
  end

  config.vm.define "db" do |db|
    db.vm.hostname = "database-server"

    db.vm.network "private_network", ip: "192.168.10.3"

    db.vm.provision "shell",
    path: "https://raw.githubusercontent.com/runnerdave/vagrant-init/master/scripts/centos-database.sh"
  end

  

  config.vm.synced_folder ".", "/vagrant", type: "rsync", rsync__exclude: [".git/", "Vagrantfile", "README.MD"], rsync__auto: "true"

end
