Vagrant.configure("2") do |config|
  config.vm.box = "vagrantbox-v1.1"
  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  config.vm.define "vagrantbox-dev" do |v|
    v.vm.host_name = "vagrantbox"
    v.vm.provision :shell, :path => 'script/provision-vm'
    v.vm.network "private_network", :ip => "172.16.10.10"
   	v.vm.provider :virtualbox do |vb|
        vb.customize ['modifyvm', :id, '--memory', ENV['VM_MEMORY'] || 3072]
        vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
        vb.customize ['modifyvm', :id, '--natdnsproxy1', 'on']
        vb.customize ["modifyvm", :id, "--cpus", ENV['VM_CPUS'] || 4]
  	end
  end

  vagrantfile_extra = "#{ENV['VAGRANT_CWD']}/Vagrantfile_extra.rb"
  eval File.open(vagrantfile_extra).read if File.exists?(vagrantfile_extra)
end
