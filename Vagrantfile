Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"

##################################################################
# VIRTUALBOX config
##################################################################
config.vm.provider "virtualbox" do |vb|
   vb.name = "srv1"
   vb.memory = "4096"
   vb.cpus = "2"
end

### network setting
  config.vm.define "srv1"
  config.vm.network "public_network", bridge: "enp0s31f6", ip: "192.168.100.100"
  #config.vm.network "forwarded_port", guest: 8080, host: 8081

  ### SSH access 
  config.ssh.insert_key = false 
  config.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa'] 
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
  config.vm.provision "shell", inline: <<-EOC
    sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
    sudo systemctl restart sshd.service
    echo "finished"
  EOC
  ### 

  ### install python for ansible
  config.vm.provision "shell", inline: "apt-get update && apt-get install -y python3-minimal"

end
