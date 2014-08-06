$script = <<SCRIPT
  # Update software repository on Ubuntu
  sudo apt-get -y update

  # Install git
  sudo apt-get install -y git

  # Download the Git repository that contains analysis scripts/code
  git clone https://github.com/srp33/Makedown_code.git

  # Move the analysis files to the home directory
  mv Makedown_code/* .
  mv Makedown_code/.git* .
  rm -rf Makedown_code

  # Update permissions on .git directory so it can be updated
  sudo chmod 777 .git -R

  # Install software and dependencies
  ./install

  # Create directory that will be shared between host and guest operating systems
  mkdir -pv Notebooks
SCRIPT

# https://docs.vagrantup.com for details about the settings below
Vagrant.configure("2") do |config|
  config.vm.box = "trusty64"
  # From https://vagrantcloud.com/ubuntu/trusty64/version/1
  config.vm.box_url = "https://vagrantcloud.com/ubuntu/trusty64/version/1/provider/virtualbox.box"
  config.vm.provision :shell, :inline => $script

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]
  end

  config.vm.synced_folder "Notebooks", "/home/vagrant/Notebooks", :create => "true"
end
