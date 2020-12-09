IMAGE_NAME = "centos/7"
IP = "192.168.219.133"

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

  # master node
  config.vm.define "rancher" do |cfg|
    cfg.vm.box = IMAGE_NAME
    cfg.vm.network "public_network", ip: IP
    cfg.vm.hostname = "rancher"
    
    cfg.vm.provider "virtualbox" do |v|
      v.memory = 16384
      v.cpus = 4
      v.name = "rancher"
    end

    cfg.vm.provision "shell", inline: <<-SCRIPT
      yum install epel-release -y
      yum install vim git tree wget -y
    SCRIPT

    # install docker
    cfg.vm.provision "shell", inline: <<-SCRIPT
      yum install -y yum-utils
      yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
      yum install docker-ce docker-ce-cli containerd.io docker-compose -y
      systemctl enable docker
      systemctl start docker
    SCRIPT
  end
end