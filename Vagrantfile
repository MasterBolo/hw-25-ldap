# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
if Vagrant.has_plugin?("vagrant-vbguest")
      config.vbguest.auto_update = false
      config.vbguest.no_remote = true
    end  
    config.vm.box = "almalinux/9"
    config.vm.provider :virtualbox do |v|
      v.memory = 2048
      v.cpus = 1
    end
  
    boxes = [
      { :name => "ipa.otus.lan",
        :ip => "192.168.56.12",
        :playbook => "Ansible/ipa.yml"
      },
      { :name => "client1.otus.lan",
        :ip => "192.168.56.13",
        :playbook => "Ansible/client1.yml"
      },
      { :name => "client2.otus.lan",
        :ip => "192.168.56.14",
        :playbook => "Ansible/client2.yml"
      }
    ]

    boxes.each do |opts|
      config.vm.define opts[:name] do |config|
        config.vm.hostname = opts[:name]
        config.vm.network "private_network", ip: opts[:ip]
        config.vm.provision "ansible" do |ansible|
            ansible.playbook = opts[:playbook]
      end
    end
  end
end


