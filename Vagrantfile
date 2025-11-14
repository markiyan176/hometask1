

Vagrant.configure("2") do |config|

  config.vm.box = "generic/centos9s"
  config.vm.hostname = "nginx-server" 


  config.vm.network "forwarded_port", guest: 80, host: 8888

  
  config.vm.synced_folder "./www-content", "/var/www/html"

  
  config.vm.provision "shell", inline: <<-SHELL
    echo "Starting Nginx setup..."
  
    sudo yum install -y epel-release
    
   
    sudo yum install -y nginx
    
   
    sudo sed -i 's/^SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
    sudo setenforce 0 

    sudo systemctl start nginx
    sudo systemctl enable nginx
    
    sudo systemctl disable firewalld
    sudo systemctl stop firewalld
    
    echo "Nginx setup complete."
    SHELL
end