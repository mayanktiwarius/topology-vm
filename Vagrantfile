Vagrant.configure("2") do |config|
  # Define the base box
  config.vm.box = "ubuntu/focal64"

  # Set up the VM
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  # Set up the VM hostname
  config.vm.hostname = "topology-vm"

  # Network configuration
  config.vm.network "private_network", type: "dhcp"

  # Sync the topology folder
  # config.vm.synced_folder "./topology", "/home/vagrant/topology", type: "nfs"

  # Mount
  #config.vm.synced_folder "./topology", "/home/vagrant/topology"
  config.vm.synced_folder "./topology", "/home/vagrant/topology", type: "rsync", rsync__auto: true

  # Provision the VM with Docker and Docker Compose
  config.vm.provision "shell", inline: <<-SHELL
    # Update and install necessary packages
    sudo apt-get update
    sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common

    # Install Docker
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    sudo apt-get update
    sudo apt-get install -y docker-ce

    # Install Docker Compose
    sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose

    # Add vagrant user to the docker group
    sudo usermod -aG docker vagrant
  SHELL
end
