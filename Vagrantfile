### Define number of Master and Worker nodes
NUM_MASTER_NODE = 2
NUM_WORKER_NODE = 2
NUM_LOADBALANCER_NODE = 1

### Define network
IP_NETWORK = "192.168.42."
MASTER_IP_START = 0
WORKER_IP_START = 10
LOADBALANCER_IP_START = 20

### Ansible playbooks
ARRAY_PLAYBOOK = ["prerequisites.yml", "provision-ca-tls-certs.yml", "generate-kube-conf-auth.yml", "generate-data-encryption-conf-key.yml", "bootstrap-etcd-cluster.yml", "bootstrap-control-plane.yml", "tls-bootstrap-kube-worker-nodes.yml", "configure-kubectl-remote-access.yml", "pod-networking-solution.yml", "kube-api-server-to-kubelet-conf.yml", "deploy-dns-cluster-addon.yml"]
NUM_PLAYBOOK = ARRAY_PLAYBOOK.length()

### Create Master nodes
Vagrant.configure("2") do |config|
  (1..NUM_MASTER_NODE).each do |i|
    config.vm.define "master-#{i}" do |node|
      ### Node config
      node.vm.box = "ubuntu/focal64"
      node.vm.hostname = "master-#{i}"
      node.vm.network "public_network", ip: IP_NETWORK + "#{MASTER_IP_START + i}", bridge: "eno1"
      ### Provide Memory/CPU
      node.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
      end
    end
  end
end

### Create Load Balancer nodes
Vagrant.configure("2") do |config|
  (1..NUM_LOADBALANCER_NODE).each do |i|
    config.vm.define "loadbalancer-#{i}" do |node|
      ### Node config
      node.vm.box = "ubuntu/focal64"
      node.vm.hostname = "loadbalancer"
      node.vm.network "public_network", ip: IP_NETWORK + "#{LOADBALANCER_IP_START + i}", bridge: "eno1"
      ### Provide Memory/CPU
      node.vm.provider "virtualbox" do |v|
        v.memory = 512
        v.cpus = 1
      end
    end
  end
end

### Create Worker nodes
Vagrant.configure("2") do |config|
  (1..NUM_WORKER_NODE).each do |i|
    config.vm.define "worker-#{i}" do |node|
      ### Node config
      node.vm.box = "ubuntu/focal64"
      node.vm.hostname = "worker-#{i}"
      node.vm.network "public_network", ip: IP_NETWORK + "#{WORKER_IP_START + i}", bridge: "eno1"
      ### Provide Memory/CPU
      node.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 2
      end
      ### Execute Ansible playbook
      if i == NUM_WORKER_NODE
        (1..NUM_PLAYBOOK).each do |j|
          node.vm.provision "ansible" do |ansible|
            ### Apply Parallel Execution
            ansible.limit = "all"
            ansible.verbose = "v"
            ansible.playbook = "./playbooks/" + ARRAY_PLAYBOOK[j-1]
          end
        end
      end
    end
  end
end
