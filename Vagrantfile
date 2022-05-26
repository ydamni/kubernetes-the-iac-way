#Define number of Master and Worker nodes
NUM_MASTER_NODE = 2
NUM_WORKER_NODE = 2
NUM_LOADBALANCER_NODE = 1

#Define network
IP_NETWORK = "192.168.42."
MASTER_IP_START = 0
WORKER_IP_START = 10
LOADBALANCER_IP_START = 20

Vagrant.configure("2") do |config|
  #Create Master nodes
  (1..NUM_MASTER_NODE).each do |i|
    config.vm.define "master-#{i}" do |node|
      #Node config
      node.vm.box = "ubuntu/focal64"
      node.vm.hostname = "master-#{i}"
      node.vm.network "public_network", ip: IP_NETWORK + "#{MASTER_IP_START + i}", bridge: "eno1"
      #Provide Memory/CPU
      node.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
      end
      #Implement Ansible
      node.ssh.insert_key = false
      node.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "playbook.yml"
      end
    end
  end
end

Vagrant.configure("2") do |config|
  #Create Load Balancer nodes
  (1..NUM_LOADBALANCER_NODE).each do |i|
    config.vm.define "loadbalancer-#{i}" do |node|
      #Node config
      node.vm.box = "ubuntu/focal64"
      node.vm.hostname = "loadbalancer"
      node.vm.network "public_network", ip: IP_NETWORK + "#{LOADBALANCER_IP_START + i}", bridge: "eno1"
      #Provide Memory/CPU
      node.vm.provider "virtualbox" do |v|
        v.memory = 512
        v.cpus = 1
      end
      #Implement Ansible
      node.ssh.insert_key = false
      node.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "playbook.yml"
      end
    end
  end
end

Vagrant.configure("2") do |config|
  #Create Worker nodes
  (1..NUM_WORKER_NODE).each do |i|
    config.vm.define "worker-#{i}" do |node|
      #Node config
      node.vm.box = "ubuntu/focal64"
      node.vm.hostname = "worker-#{i}"
      node.vm.network "public_network", ip: IP_NETWORK + "#{WORKER_IP_START + i}", bridge: "eno1"
      #Provide Memory/CPU
      node.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
      end
      #Implement Ansible
      node.ssh.insert_key = false
      node.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "playbook.yml"
      end
    end
  end
end
