# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
apt-get update

# Install Ansible
if [ ! -x "$(which ansible)" ]; then
  apt-get install -y software-properties-common
  apt-add-repository -y ppa:ansible/ansible
  apt-get update
  apt-get install -y ansible
fi

# Install Git
if [ ! -x "$(which git)" ]; then
  apt-get install -y git
fi

# Checkout or update the repo
if [ ! -d statistics-etl ]; then
  sudo -i -u vagrant git clone https://github.com/ScorpionResponse/statistics-etl.git statistics-etl
else
  sudo -i -u vagrant sh -c "cd statistics-etl && git pull"
fi

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
