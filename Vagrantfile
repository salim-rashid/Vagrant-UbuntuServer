bootstrap = <<SCRIPT
  useradd -m -s /bin/bash -U dev -u 666 --groups sudo
  cp -pr /home/vagrant/.ssh /home/dev/
  chown -R dev:dev /home/dev
  echo "%dev ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/dev

  cp /etc/ssh/ssh_config /etc/ssh/ssh_config.bak
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "aspyatkin/ubuntu-18.04-server"
  config.vm.hostname = "ubuntu-server18.04"
  config.vm.disk :disk, size: "20GB", primary: true
  config.vm.boot_timeout = 600
  config.vm.network "public_network"
  config.ssh.username = 'dev'
  config.vm.provision "file", source: "./setup.sh",
    destination: "/tmp/"
  config.vm.provision "shell", inline: "#{bootstrap}", privileged: true
  config.vm.provision "file", source: "./setup.sh",
    destination: "/tmp/"
  config.vm.provision "file", source: "./ssh_config",
    destination: "/etc/ssh/ssh_config"
  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = 512
    vb.cpus = 1
  end
end