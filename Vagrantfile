# plugins:
# vagrant plugin install vagrant-bindfs

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.ssh.forward_agent = true

  # sync folders
  config.vm.synced_folder "/Users/allisson/Projects", "/home/vagrant/Projects", type: "nfs", mount_options: ['nolock', 'vers=3', 'udp', 'noatime', 'actimeo=1']
  config.bindfs.bind_folder "/home/vagrant/Projects", "/home/vagrant/Projects"

  # disable default sync folder
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "instance" do |instance|
    instance.vm.hostname = "devmachine"
    instance.vm.network "private_network", ip: "192.168.33.10"
    
    instance.vm.provider "virtualbox" do |vb|
      vb.name = "devmachine"
      vb.memory = "4096"
      vb.cpus = 6
    end

  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
  end

end
