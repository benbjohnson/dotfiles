# -*- mode: ruby -*-
# vi: set ft=ruby :

################################################################################
#
# This Vagrant file is a basic configuration that sets up Go to run on
# Ubuntu 12.04 and syncs my GOPATH and projects folder.
#
################################################################################

VAGRANTFILE_API_VERSION = "2"

BOOTSTRAP = <<-eos
sudo apt-get install -y build-essential
sudo apt-get install -y python-software-properties
sudo add-apt-repository -y ppa:duh/golang
sudo apt-get -y update
sudo apt-get -y install golang

export GOPATH=/gocode
echo "export GOPATH=$GOPATH" | sudo tee /etc/profile.d/go.sh > /dev/null
echo "PATH=\$PATH:/usr/local/go/bin:$GOPATH/bin" | sudo tee -a /etc/profile.d/go.sh > /dev/null
source /etc/profile
eos

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network :forwarded_port, guest: 8585, host: 8585
  config.vm.network :forwarded_port, guest: 8589, host: 8589
  config.vm.provision "shell", inline: BOOTSTRAP
  config.vm.synced_folder ENV["GOPATH"], "/gocode"
  config.vm.synced_folder "/projects", "/projects"
end
