Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"
#  config.vm.define "consul-server" do |machine|
#	machine.vm.network "private_network", ip: "192.168.99.100"
#	machine.vm.provision "shell", inline: "echo ubuntu:ubuntu | chpasswd"
#	machine.vm.provision "shell", inline: "sudo echo ubuntu:ubuntu | chpasswd"
#	machine.vm.provision "shell", inline: "apt-get update && apt-get install -y python3-minimal"
#  end


##################################################################
# VIRTUALBOX config
##################################################################
config.vm.provider "virtualbox" do |vb|
  # Don't boot with headless mode
#   vb.gui = false
   vb.name = "srv1"
   vb.memory = "4096"
   vb.cpus = "2"
#   vb.customize ["modifyvm", :id, "--vram", "128"]
#   vb.customize ["modifyvm", :id, "--memory", "2048"]
#   vb.customize ["modifyvm", :id, "--cpus", "2"]
#   vb.customize ["modifyvm", :id, "--cpuexecutioncap", "75"]
#   vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
#   vb.customize ["modifyvm", :id, "--ioapic", "on"]
#   vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    #unless File.exist?(disk)
     #vb.customize ['createhd', '--filename', disk, '--variant', 'Fixed', '--size', 1 * 1024]
      ##vb.customize ['createhd', '--filename', disk, '--size', 500 * 1024]
     #end
    #vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk]
  end



  ### network setting
  config.vm.define "srv1"
  config.vm.network "public_network", bridge: "enp0s31f6", ip: "192.168.100.100"
#  config.vm.network "forwarded_port", guest: 8080, host: 8081

#  config.vm.network "private_network", bridge: "enp0s31f6", auto_config: false, ip: "192.168.99.101"
#  config.vm.provision "shell", run: "always", inline: "ip addr add 192.168.100.200 dev eth1"

  ### SSH access 
  # 1
  config.ssh.insert_key = false 
  # 2
  config.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa'] 
  # 3
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
  # 4
  config.vm.provision "shell", inline: <<-EOC
    sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
    sudo systemctl restart sshd.service
    echo "finished"
  EOC
  ### 

  ### install python for ansible
  config.vm.provision "shell", inline: "apt-get update && apt-get install -y python3-minimal"


end
