# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
apt-get update

# Install Ansible
apt-get install -y software-properties-common
apt-add-repository -y ppa:ansible/ansible
apt-get update
apt-get install -y ansible

# Install Git
apt-get install -y git

# Checkout the repo
sudo -i -u vagrant git clone https://github.com/ScorpionResponse/statistics-etl.git statistics-etl

# Run the ansible playbook
cd statistics-etl
ansible-playbook ansible/site.yml -i ansible/hosts --connection=local
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url = "https://vagrantcloud.com/ubuntu/boxes/trusty64/versions/1/providers/virtualbox.box"
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'" # avoids 'stdin: is not a tty' error.
  config.vm.provision :shell, inline: $script

end
