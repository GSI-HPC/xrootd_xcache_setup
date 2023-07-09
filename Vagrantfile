boxes={
  "client":{networks:['172.17.0.9'], forwarded:[]},
  "server":{networks:['172.17.0.10'], forwarded:[[9090,9099]]},
  "proxy":{networks:['172.17.0.11'], forwarded:[]},
  "memoryproxy":{networks:['172.17.0.11'], forwarded:[]},
  "diskproxy":{networks:['172.17.0.11'], forwarded:[]},
}

provider= "libvirt"

Vagrant.configure("2") do |config|
  boxes.each do |name,box|
    config.vm.synced_folder ".", "/vagrant", type: "rsync",
      rsync__exclude: ".git/"
    config.vm.define "#{name}" do |vm|
      vm.vm.hostname="#{name}"
      vm.vm.graceful_halt_timeout = 300
      vm.vm.provider provider do |v|
        if provider=="libvirt" then
          v.cpu_mode = "host-model"
        end
        v.memory = 2048
        v.cpus = 2
      end
      vm.vm.box = "generic/rocky8"
      box[:networks].each do |ipi|
        #generate all networks
        vm.vm.network "private_network", ip: ipi
        box[:forwarded].each do| guest,host|
          vm.vm.network "forwarded_port", guest: guest , host: host
        end
      end
      if box[:ib]
        #install ib if needed
        end
      vm.vm.provision "ansible" do |ansible|
#        ansible.verbose='v'
        ansible.playbook="playbook.yml"
      end

      vm.vm.provision :hosts, :sync_hosts => true

      

      vm.vm.provision "shell", inline: "mkdir /etc/apparmor.d/disable -p"


    end
  end
end
