# -*- mode: ruby -*-
# vi: set ft=ruby  :

machines = {
  "office-new-york-router"   => {"memory" => "512", "cpu" => "2", "ip" => "240","image" => "debian/bullseye64"},
  "office-new-york-Switch"   => {"memory" => "512", "cpu" => "2", "ip" => "241","image" => "ubuntu/focal64"},
  "office-new-york-sr01"   => {"memory" => "512", "cpu" => "2", "ip" => "242","image" => "debian/bullseye64"},
  "office-new-york-sr02"   => {"memory" => "512", "cpu" => "2", "ip" => "243","image" => "debian/bullseye64"},

}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}.zabbix"
      machine.vm.network "public_network",ip: "192.168.3.#{conf["ip"]}", bridge: "wlp1s0"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        vb.customize ["modifyvm", :id, "--groups", "/zabbix"]
      end
      if "#{conf["image"]}" == "debian/bullseye64"
        machine.vm.provision "shell", path: "./scripts/debian.sh" 
      end
      if "#{conf["image"]}" == "ubuntu/focal64"
        machine.vm.provision "shell", path: "./scripts/debian.sh" 
      end

    end
  end
end
