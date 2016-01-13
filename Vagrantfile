# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  # Amount of nodes to start
  nodes = 1

  (1..nodes).each do |i|
    config.vm.define "ansible-rexray-#{i}" do |node|
      node.vm.box = "geerlingguy/centos7"

      # Add a SATA controller with 30 ports to the VM, so REX-Ray can add disks on the fly
      node.vm.provider :virtualbox do |vb|
       vb.customize ["storagectl", :id, "--add", "sata", "--controller", "IntelAhci", "--name", "SATA", "--portcount", 30, "--hostiocache", "on"]
       vb.customize ["modifyvm", :id, "--macaddress1", "auto"]
      end

      # Set the current $PWD as the place where you will
      # store the VMDKs that are attached to the VM.
      dir = "#{ENV['PWD']}/Volumes"

      node.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "ansible_rexray.yml"
        ansible.galaxy_role_file = "galaxy_roles.txt"
        #ansible.extra_vars = {
        #  rexray_vbox_volume_path: "#{dir}"
        #}
      end

      node.vm.provision "shell",
        inline: "sed -i '/.*volumePath.*/c\\\x20\x20volumePath: \"#{dir}\"' /etc/rexray/config.yml"
    end
  end
end
