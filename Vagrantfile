Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.box_version = "14.04"
  config.vm.hostname = "listener-documentation"

  # Forwarding for web application
  config.vm.network :forwarded_port, guest: 4000, host: 4000
  # Forwarding for livereload
  config.vm.network :forwarded_port, guest: 35729, host: 35729

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
  end

  config.vm.provision "shell", inline: <<-SHELL
    echo "--------------------------"
    echo "Installing system packages"
    echo "--------------------------"
    # Add NodeJS PPA
    curl -sL https://deb.nodesource.com/setup_4.x | sudo bash -

    sudo apt-get update
    sudo apt-get install -y --force-yes build-essential nodejs git

    echo "-----------------------"
    echo "Installing Node Modules"
    echo "-----------------------"
    sudo npm install --global gitbook-cli
    cd /vagrant
    npm install
    echo "cd /vagrant" >> /home/vagrant/.bashrc
  SHELL
end
