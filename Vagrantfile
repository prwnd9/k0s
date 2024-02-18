# https://app.vagrantup.com/boxes

Vagrant.configure("2") do |config|
  config.vm.define "k0s" do |config|
    # https://app.vagrantup.com/boxes/search
    # ubuntu 22.04
    config.vm.box = "ubuntu/jammy64"

    config.vm.hostname = "k0s"
    config.vm.box_check_update = false
    config.vm.network "private_network", ip: "192.168.56.10"
    config.vm.synced_folder '.', '/vagrant', disabled: false

    # increase primary disk
    # https://www.vagrantup.com/docs/disks/usage
    # export VAGRANT_EXPERIMENTAL="disks"
    # config.vm.disk :disk, size: "200GB", primary: true

    config.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.cpus = 1
      vb.memory = "1024" # mb
      vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ] # disable logging

      # FIX
      # https://github.com/hashicorp/vagrant/issues/9524
      vb.customize [ "modifyvm", :id, "--audio", "none"]
    end

$ROOT_SCRIPT = <<SCRIPT
# https://docs.k0sproject.io/stable/
# https://docs.k0sproject.io/stable/install/
# https://github.com/k0sproject/k0s/releases

# Download
curl -sSLf https://get.k0s.sh | K0S_VERSION=v1.29.1+k0s.1 sh

# Install
k0s install controller --single

# Start
k0s start
SCRIPT
    config.vm.provision "shell", :inline => $ROOT_SCRIPT

$USER_SCRIPT = <<SCRIPT
# go to /vagrant
echo "cd /vagrant" >> /home/vagrant/.bashrc
SCRIPT
    config.vm.provision "shell", :inline => $USER_SCRIPT, privileged: false

  end
end

