# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.hostname = 'matomo.local'

  config.vm.provider "virtualbox" do |v, override|
    v.memory = 1024
    v.cpus = 2
    override.vm.network 'private_network', ip: '10.55.55.56'
  end

  # Workarounds for:
  # https://github.com/hashicorp/vagrant/issues/10914
  # https://github.com/hashicorp/vagrant/issues/10950
  $script = <<-SCRIPT
  if [[ (( `which ansible` )) ]]; then
    exit 0
  fi
  echo Implementing work-around for Ansible install hanging.
  sudo apt-get update -y -qq
  sudo DEBIAN_FRONTEND=noninteractive apt-get install -y -qq --option \"Dpkg::Options::=--force-confold\" libssl1.1 python-pip
  SCRIPT

  config.vm.provision "shell", inline: $script

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "tests/test.yml"
  end

end
