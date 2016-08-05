# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/trusty64"
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.hostname = "influxdb.dev"
    config.vm.synced_folder ".", "/var/www",
        :mount_options => ["dmode=777", "fmode=777"]

    # Optional NFS. Make sure to remove other synced_folder line too
    #config.vm.synced_folder ".", "/var/www", :nfs => true
    #{ :mount_options => ["dmode=777","fmode=666"] }

    config.vm.provision "shell", inline: <<-SHELL
        curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -
        source /etc/lsb-release
        echo "deb https://repos.influxdata.com/${DISTRIB_ID,,} \
        ${DISTRIB_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
        sudo apt-get -y update && sudo apt-get -y install influxdb
        sudo service influxdb start
    SHELL
end
