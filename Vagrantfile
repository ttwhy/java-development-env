Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/disco64"
	config.vm.boot_timeout = 500
	

	config.vm.provider :virtualbox do |vb|
		vb.gui = true
		vb.customize ["modifyvm", :id, "--memory", 4096]
		vb.customize ["modifyvm", :id, "--cpus", 2] 
		#`awk "/^processor/ {++n} END {print n}" /proc/cpuinfo 2> /dev/null || sh -c 'sysctl hw.logicalcpu 2> /dev/null || echo ": 2"' | awk \'{print \$2}\' `.chomp ]
	end

	config.vm.provision "ansible_local" do |ansible|
		ansible.playbook = "playbook.yml"
	end
end
