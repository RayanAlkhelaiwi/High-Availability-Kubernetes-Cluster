# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  if Vagrant.has_plugin? "vagrant-vbguest"
    config.vbguest.no_install  = true
    config.vbguest.auto_update = false
    config.vbguest.no_remote   = true
  end

  LoadBalancerCount = 2
  (1..LoadBalancerCount).each do |i|

    config.vm.define "loadbalancer0#{i}" do |lb|

      lb.vm.box               = "almalinux/8"
      lb.vm.box_check_update  = false
      lb.vm.hostname          = "loadbalancer0#{i}"

      lb.vm.network "private_network", ip: "172.16.16.5#{i}"

      lb.vm.provider :virtualbox do |v|
        v.name    = "loadbalancer0#{i}"
        v.memory  = 512
        v.cpus    = 1
      end
    end
  end

  MasterCount = 3
  (1..MasterCount).each do |i|
    config.vm.define "kmaster0#{i}" do |km|
      km.vm.box               = "almalinux/8"
      km.vm.box_check_update  = false
      km.vm.hostname          = "kmaster0#{i}"

      km.vm.network "private_network", ip: "172.16.16.10#{i}"

      km.vm.provider :virtualbox do |v|
        v.name    = "kmaster0#{i}"
        v.memory  = 2048
        v.cpus    = 2
      end
    end
  end

  WorkerCount = 2
  (1..WorkerCount).each do |i|
    config.vm.define "kworker0#{i}" do |kw|
      kw.vm.box               = "almalinux/8"
      kw.vm.box_check_update  = false
      kw.vm.hostname          = "kworker0#{i}"

      kw.vm.network "private_network", ip: "172.16.16.20#{i}"

      kw.vm.provider :virtualbox do |v|
        v.name    = "kworker0#{i}"
        v.memory  = 1024
        v.cpus    = 2
      end
    end
  end
end
