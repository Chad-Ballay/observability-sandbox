Vagrant.require_version ">= 1.7.0"

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/xenial64"
  
  
  config.ssh.insert_key = false

        
  config.vm.define :DB do |cfg|
        cfg.vm.network "forwarded_port", guest: 9090, host: 9100
        cfg.vm.network :private_network, ip: "10.0.0.10"
        cfg.vm.provider :virtualbox do |v|
            v.name = "DB"
            v.memory = "2048"
            v.cpus = 1
        end
    end
    
  config.vm.define :App do |cfg|
        cfg.vm.network :private_network, ip: "10.0.0.11"
        cfg.vm.provider :virtualbox do |v|
            v.name = "App"
            v.memory = "2048"
            v.cpus = 1
        end
    end

  config.vm.define :Web do |cfg|
        cfg.vm.network "forwarded_port", guest: 80, host: 8080
        cfg.vm.network :private_network, ip: "10.0.0.12"
        cfg.vm.provider :virtualbox do |v|
            v.name = "Web"
            v.memory = "2048"
            v.cpus = 1
        end
    end
  config.vm.define :Prometheus do |cfg|
        cfg.vm.network "forwarded_port", guest: 9090, host: 9090
        cfg.vm.network "forwarded_port", guest: 3000, host: 3000
        cfg.vm.network :private_network, ip: "10.0.0.13"
        cfg.vm.provider :virtualbox do |v|
            v.name = "Prometheus"
            v.memory = "2048"
            v.cpus = 1
        end
    end

  config.vm.provision "shell" do |s|
        s.inline = "apt-get install -y python"
  end

  config.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "playbook.yaml"
  end 
end
