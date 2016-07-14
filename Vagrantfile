# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "terrywang/archlinux"
  config.ssh.forward_x11 = true

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
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"


  # simple copy to destination
  # config.vm.provision "file", source: "~/.gitconfig", destination: ".gitconfig"
  config.vm.provision "file", source: "environment/linux/.xinitrc", destination: ".xinitrc"
  config.vm.provision "file", source: "environment/linux/.bashrc", destination: ".bashrc"
  config.vm.provision "file", source: "environment/linux/awesome/rc.lua", destination: ".config/awesome/rc.lua"
  
  #sync
  config.vm.synced_folder "environment/workspace", "/home/vagrant/workspace"
  config.vm.synced_folder "C:/Users/Riewe/Downloads", "/mnt/archive"


  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
     vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "2048"
     #video memory
     vb.customize ["modifyvm", :id, "--vram", "32"]
     vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
     vb.cpus = 4
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

# language
     echo "de_DE.UTF-8 UTF-8" >> /etc/locale.gen
     echo LANG=de_DE.UTF-8 > /etc/locale.conf
     echo KEYMAP=de-latin1-nodeadkeys > /etc/vconsole.conf
     ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime
     locale-gen

     cp /vagrant/environment/linux/20-keyboard.conf /etc/X11/xorg.conf.d/
     chmod 755 /etc/X11/xorg.conf.d/ -R

     usermod -aG video vagrant
     usermod -aG audio vagrant


#mirror liste
     echo 'Searching for fast package mirrors...'
     cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup
     sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.backup
     rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist
     echo 'done.'

# updating system
     echo 'Upgrading to the latest System...'
     pacman -Syu --noconfirm
     echo 'Installing additional Software'
     pacman -S eclipse-java jdk8-openjdk xorg-xinit awesome chromium xterm xfce4-terminal apache-ant junit visualvm java-jdepend maven gradle --noconfirm --noscriptlet 

     # pacman -S docker npm 

     archlinux-java set java-8-openjdk

# prepare system for autostart
     mkdir -p /etc/systemd/system/getty@tty1.service.d/
     mkdir /home/vagrant/.config/awesome/ -p
     mkdir /home/vagrant/workspace -p
     mkdir /mnt/archive -p
     mkdir /srv/ecommerce -p
     cp -R /vagrant/environment/.eclipse/ /home/vagrant/
     chown vagrant:vagrant /home/vagrant/ -R
     chown vagrant:vagrant /mnt/archive -R
     chown vagrant:vagrant /srv/ecommerce -R

echo "[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin vagrant --noclear %I $TERM
" > /etc/systemd/system/getty@tty1.service.d/override.conf 

sed -i -- 's/timeout=5/timeout=1/' /boot/grub/grub.cfg

   SHELL
end
