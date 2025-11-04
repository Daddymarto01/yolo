# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Base box
  config.vm.box = "ubuntu/focal64"

  # Forward ports for frontend, backend, and MongoDB
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 5000, host: 5000
  config.vm.network "forwarded_port", guest: 27017, host: 27017

  # Synced folder to share project files
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"

  # Provider-specific configuration
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"  # Adjust memory as needed
  end

  # Provisioning script to install Docker, Docker Compose, and run your app
  config.vm.provision "shell", inline: <<-SHELL
    # Update and install dependencies
    sudo apt-get update
    sudo apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release

    # Install Docker
    if ! command -v docker &> /dev/null; then
      curl -fsSL https://get.docker.com -o get-docker.sh
      sh get-docker.sh
      sudo usermod -aG docker $USER
    fi

    # Install Docker Compose
    if ! command -v docker-compose &> /dev/null; then
      sudo curl -L "https://github.com/docker/compose/releases/download/v2.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      sudo chmod +x /usr/local/bin/docker-compose
    fi

    # Navigate to synced folder and start Docker Compose
    cd /vagrant
    sudo docker-compose down
    sudo docker-compose up -d --build
  SHELL
end
