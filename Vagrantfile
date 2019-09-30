# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  routes = `ip route`.lines.grep(/default via/)
  if routes.first.start_with?("default")
    iface = routes.first.split(" ")[4]  # first line always has default: default via 192.168.1.1 dev eth0  metric 1024
    puts "Detected " + iface + " as default interface"

  end

  config.vm.box = "centos/7"
  config.vm.provider :libvirt do |vb|
    vb.memory = 4096
    vb.cpus = "4"
  end

  config.vm.network "public_network", bridge: iface, dev: iface

  config.vm.define "nessus" do |node|
    config.vm.hostname = "nessus.local"
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.compatibility_mode = "2.0"
  end

end
