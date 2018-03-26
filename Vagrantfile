Vagrant.configure("2") do |config|
  config.vm.box = "mvbcoding/awslinux"
  config.vm.box_version = "2017.03.0.20170401"
  config.vm.network "forwarded_port", guest: 3306, host: 3306


  # deploy codes
  config.vm.provision :shell, privileged: false, inline: <<-SHELL
    whoami      #=> vagrant
    echo $HOME  #=> /home/vagrant

    # install packages
    sudo yum -y update
    sudo yum -y install mysql mysql56-server

    # chkconfig
    sudo chkconfig mysqld on
    sudo service mysqld start
SHELL

  # Configure your environment variables
  $set_environment_variables = <<SCRIPT
tee "/etc/profile.d/myvars.sh" > "/dev/null" <<EOF
export MYSQL_ROOT_PASSWORD=""
export MYSQL_DATABASE=test # anything ok
export MYSQL_USER=youruser
export MYSQL_PASSWORD=yourpassword
export MYSQL_ALLOW_EMPTY_PASSWORD=yes
export IMPORT_SOURCES="your_db_host1,3306,username,password,database1|your_db_host2,3306,username,password,database2"
EOF
SCRIPT

  # Set environment variables & import DB
  config.vm.provision :shell, inline: $set_environment_variables, run: "always"
  config.vm.provision :shell, path: "import-data.sh"
end
