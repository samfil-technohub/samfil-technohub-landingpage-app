Vagrant.configure("2") do |config|
  # vm operating system
  config.vm.box = "ubuntu-xenial64"

  # ssh settings
  config.ssh.username = "vagrant"
  config.ssh.private_key_path = ["~/.ssh/server_key", "~/.vagrant.d/insecure_private_key"]
  config.ssh.insert_key = false

  # upload public key into the machine
  config.vm.provision "file", source: "~/.ssh/server_key.pub", destination: "~/.ssh/authorized_keys"

  # vm provider
  config.vm.provider "virtualbox" do |vb|
    # serial port settings
    vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]

    # vm cpu cores
    vb.cpus = "1"

    # vm memory size in megabytes
    vb.memory = "1024"
  end

  # synchronize folders between host and guest machines
  config.vm.synced_folder '.', '/usr/share/nginx/html'

  # configure the vm
  config.vm.define "development" do |development|
    development.vm.hostname = "development"
    development.vm.network "private_network", ip: "192.168.255.9"
    development.vm.provision :ansible do |ansible|
      ansible.inventory_path = "configuration/hosts"
      ansible.verbose = "vvvv"
      ansible.raw_arguments  = ["--private-key=~/.ssh/server_key"]
      ansible.playbook = "configuration/server.yml"
    end
    development.vm.provision "shell", inline: <<-SHELL
      echo 'Running Serverspec Tests...'
      cd /usr/share/nginx/html/configuration/serverspec
      rake -v -t
    SHELL
  end 
end
