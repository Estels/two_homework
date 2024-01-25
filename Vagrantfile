
Vagrant.configure("2") do |config|

  config.vm.define "nginx" do |nginx|
    nginx.vm.box = "ubuntu/focal64"
    nginx.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.boot_timeout = 1200
    nginx.vm.provider "virtualbox" do |v|
      v.cpus = 2
      v.memory = 4096
    end
    nginx.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "two_homework.yml"
    end

end
end
