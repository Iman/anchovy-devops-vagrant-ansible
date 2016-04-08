VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|

    config.vm.provider :virtualbox do |v|
        v.name = "anchovy"
        v.customize [
            "modifyvm", :id,
            "--name", "anchovy_vagrant",
            "--memory", 2048,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end
    config.vm.box = "vektra/trusty64-min" #"ubuntu/trusty64" #
    config.vm.network :private_network, ip: "192.168.56.105"
    config.ssh.forward_agent = true
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.inventory_path = "ansible/inventories/dev"
        ansible.limit = 'all'
        ansible.sudo = true
        ansible.raw_arguments  = "--user=vagrant"
    end
    config.vm.synced_folder "/workspace", "/workspace"

end
