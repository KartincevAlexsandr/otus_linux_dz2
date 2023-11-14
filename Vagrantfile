Vagrant.configure("2") do |config|
	config.vm.define "server1" do |web|
		web.vm.box = "generic/debian10"
		web.vm.network "forwarded_port", id: "ssh", host: 2122 , guest: 22
		web.vm.network "forwarded_port", id: "http", host: 8080 , guest: 8080
		web.vm.network "private_network", ip: "10.11.10.10", virtualbox__intnet: true
		web.vm.hostname = "server1"

		web.vm.provision "shell" do |s|
			ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
			s.inline = <<-SHELL
			echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
			echo  'StrictHostKeyChecking no' >> /etc/ssh/ssh_config
			SHELL
		end

		web.vm.provider "virtualbox" do |v|
			v.name = "server1"
			v.memory = 2048
			v.cpus = 2
		end
	end
end 
