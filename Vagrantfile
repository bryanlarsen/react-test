# -*- mode: ruby -*-
# vi: set ft=ruby :

_script = <<SCRIPT
set -o errexit
set -o pipefail
set -o nounset
set -o xtrace
shopt -s failglob

sudo apt-get update
sudo apt-get install -y python-software-properties make curl git build-essential g++

export DEBIAN_FRONTEND=noninteractive
curl -sL https://deb.nodesource.com/setup_dev | sudo bash -
apt-get install -y nodejs
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"

#  config.vm.provider "virtualbox" do |v|
#    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
#  end

  config.vm.synced_folder ".", "/vagrant", type: "rsync", rsync__exclude: [".git/", "node_modules/", "share/"]
  config.vm.synced_folder "share", "/share"

  config.vm.provision "shell", inline: _script
  config.vm.network "forwarded_port", guest: 3000, host: 3000
end
