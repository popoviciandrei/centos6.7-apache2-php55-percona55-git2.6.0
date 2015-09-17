# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "centos6.4"
  config.vm.box_url ="http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-x86_64-v20131103.box"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
     vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "4096"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL
  		sudo yum  update -y
      # Developer tools
		sudo yum groupinstall -y "Development Tools"
		sudo yum install -y zlib-devel perl-ExtUtils-MakeMaker asciidoc xmlto openssl-devel curl-devel openssl expat expat-devel 
      # Install apache
		sudo yum install -y apache
      
      # php55 install
      	sudo rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm
      	sudo yum install -y php55w php55w-gd php55w-dom php55w-mcrypt php55w-intl php55w-xsl php55w-mbstring 
	
      # percona install
		sudo rpm -Uvh http://www.percona.com/downloads/percona-release/redhat/0.1-3/percona-release-0.1-3.noarch.rpm
		sudo yum install -y Percona-Server-server-55
 
      # Open http port 80
		sudo iptables -I INPUT 5  -p tcp --dport 80 -m state --state NEW,ESTABLISHED -j ACCEPT
		sudo service iptables save
		sudo service iptables restart
	

       # git install
      	cd ~
      	wget -O git.zip https://github.com/git/git/archive/master.zip
      	unzip git.zip
      	cd git-master
      	make configure
      	./configure --prefix=/usr/local --with-expat --with-openssl
      	make all doc
        sudo make install install-doc install-html
     	cd ~ && rm git.zip && rm -rf git-master

		cd ~ && mkdir bin

      # install composer
		cd ~/bin && curl -sS https://getcomposer.org/installer | php
		mv composer.phar composer
      # install n98-magerun
		cd ~/bin && wget http://files.magerun.net/n98-magerun-latest.phar -O n98-magerun.phar
		mv n98-magerun.phar n98-magerun
	  # start apache
		sudo service httpd start
		sudo service mysql start
     # install gnome & start it with: $ startx from command line
     # sudo yum -y groupinstall "X Window System" "Desktop" "General Purpose Desktop"
   SHELL
end
