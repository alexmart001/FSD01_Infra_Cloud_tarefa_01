$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server-5.7 && \
  mysql -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';"
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 512
    vb.cpus = 1
  end
  
  config.vm.define "mysqlserver" do |mysqlserver|
    mysqlserver.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)", ip: "192.168.0.70"
    mysqlserver.vm.network "forwarded_port", guest: 3306, host: 3306

    mysqlserver.vm.provider "virtualbox" do |vb|
      vb.name = "mysqlserver"
    end

    mysqlserver.vm.provision "shell", inline: $script_mysql
    mysqlserver.vm.provision "shell", inline: "service mysql restart"

  end  

end