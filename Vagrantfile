# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "dreamscapes/archlinux"

  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provision "shell", inline: <<-SHELL
    pacman -S --noconfirm lighttpd php-fpm
    cp /vagrant/provision/lighttpd.conf /etc/lighttpd/
    sed -i 's/ = http/ = vagrant/' /etc/php/php-fpm.d/www.conf    
   SHELL

   config.vm.provision "bootstrap", type: "shell", run: "always", inline: <<-SHELL
    systemctl start lighttpd.service
    systemctl enable lighttpd.service
    systemctl start php-fpm
    systemctl enable php-fpm
   SHELL
end
