$script = <<SCRIPT
  # See http://craig-russell.co.uk/2012/05/08/install-r-on-ubuntu.html#.UyHZEuddXks
  sudo gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9
  sudo gpg -a --export E084DAB9 | sudo apt-key add -

  echo "deb http://cran.fhcrc.org/bin/linux/ubuntu precise/" | sudo tee -a /etc/apt/sources.list
  sudo apt-get -y update

  # Install pandoc, texlive, and git
  sudo apt-get install -y pandoc texlive git

  # Download the Git repository that contains analysis scripts/code
  git clone https://github.com/srp33/Makedown_code.git

  # Move the analysis files to the home directory
  mv Makedown_code/* .
  mv Makedown_code/.git* .
  rm -rf Makedown_code

  # Update permissions on .git directory so it can be updated
  sudo chmod 777 .git -R

  # Create directory that will be shared between host and guest operating systems
  mkdir -pv Notebooks
SCRIPT

# https://docs.vagrantup.com for details about the settings below
Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.provision :shell, :inline => $script

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]
  end

  config.vm.synced_folder "Notebooks", "/home/vagrant/Notebooks", :create => "true"
end
