Vagrant.configure("2") do |config|
  # config.vm.box = "mvbcoding/awslinux"

  config.vm.network "forwarded_port", guest: 80, host: 80
  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vireo4.yml"
#    ansible.playbook = "migration.yml"
  end

  # Application server
  config.vm.define :vireo4 do |vireo4|
    # dspace.vm.hostname = "vireo4"

    vireo4.vm.provider :virtualbox do |vb, override|
      # Launch with AWS AMI
      override.vm.box = "gbailey/amzn2"
      #override.vm.box = "ubuntu/xenial64" #16.04
      #override.vm.box = "ubuntu/bionic64"  #18.04

      #vb.memory = 4096
      vb.memory = 8192
      #vb.cpus = 2

      # Forward ports
      override.vm.network "forwarded_port", guest: 80, host: 80
      override.vm.network "forwarded_port", guest: 8080, host: 8080

    end
  end

end



#      override.vm.network "forwarded_port", guest: 9000, host: 9000
#      override.vm.network "forwarded_port", guest: 443, host: 443
#  config.vm.network "forwarded_port", guest: 9000, host: 9000
#  config.vm.network "forwarded_port", guest: 443, host: 443
#  config.vm.network "private_network", ip: "127.0.0.0"
