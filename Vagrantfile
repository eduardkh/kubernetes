BOX_IMAGE = "generic/ubuntu2004"
NODE_COUNT = 3

Vagrant.configure("2") do |config|
  config.vm.define "master" do |subconfig|

    subconfig.vm.provider :virtualbox do |v| 
      v.customize ["modifyvm", :id, "--memory", "2048"] 
     end
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "master"
    subconfig.vm.network :public_network, ip: "192.168.1.151", hostname: true, bridge: "Qualcomm Atheros AR8151 PCI-E Gigabit Ethernet Controller (NDIS 6.30)"
  end
  
(2..NODE_COUNT).each do |i|
  config.vm.define "node#{i}" do |subconfig|
    subconfig.vm.provider :virtualbox do |v| 
      v.customize ["modifyvm", :id, "--memory", "1024"] 
    end
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "node#{i}"
    subconfig.vm.network :public_network, ip: "192.168.1.#{i + 150}", hostname: true, bridge: "Qualcomm Atheros AR8151 PCI-E Gigabit Ethernet Controller (NDIS 6.30)"
  end
end

  # Install avahi on all machines  
  config.vm.provision "shell", inline: <<-SHELL
  sudo echo "192.168.1.151 master" | sudo tee -a /etc/hosts
  sudo echo "192.168.1.152 node2" | sudo tee -a /etc/hosts
  sudo echo "192.168.1.153 node3" | sudo tee -a /etc/hosts
  SHELL
end