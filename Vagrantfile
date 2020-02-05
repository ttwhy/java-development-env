Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/disco64"
	config.vm.boot_timeout = 500
	config.vm.provision "ansible_local" do |ansible|
		ansible.playbook = "playbook.yml"
	end
end
