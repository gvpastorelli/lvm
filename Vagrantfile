# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "lvmtest"
  config.vm.box = "centos/7"
  config.vm.hostname = "test01.local"
  config.vm.network :private_network, ip: "192.168.33.150"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"

	file_to_disk = 'tmp_disk.vdi'
	unless File.exists?(file_to_disk)
	  # 10GB
      vb.customize ['createhd', '--filename', file_to_disk, '--size', 10 * 1024]
      vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', file_to_disk]
    end

  end

  config.vm.provision :ansible do |ansible|
    ansible.limit = "all"
  ansible.become = true
  ansible.playbook = "tests/test.yml"
  #ansible.extra_vars = {
  #  users: ['greg', 'shannon'],
  #}
  end

end
