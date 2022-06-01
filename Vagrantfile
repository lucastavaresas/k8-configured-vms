Vagrant.configure("2") do |config|
  (1..3).each do |i|
      config.vm.define "k8-#{i}" do |kube|
          kube.vm.box = "ubuntu/bionic64"
          kube.vm.hostname = "node-#{i}"
          kube.vm.network "private_network", ip: "192.168.56.1#{i}"

          kube.ssh.insert_key = false
          kube.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa']
          kube.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"

          config.vm.provision "shell", inline: <<-SHELL
          apt-get update && sudo apt-get install -y apt-transport-https curl
          curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
          cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
            deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-get install docker.io -y
sudo apt-mark hold kubelet kubeadm kubectl
          SHELL
      end
  end

  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 2
end
end