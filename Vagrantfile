IMAGE_NAME = "ubuntu/focal64"
N = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 2
    end

#    config.vm.provision "shell", inline: <<-SHELL
#             pacman -Syu --noconfirm
#             pacman -S python --noconfirm
# SHELL

    
    config.vm.define "domain-controller" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.hostname = "dc"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible-setup/master-playbook.yml"
            ansible.extra_vars = {
              node_ip: "192.168.50.10",
              ansible_python_interpreter: "/usr/bin/python3",
            }
        end
    end

    # (1..N).each do |i|
    #     config.vm.define "node-#{i}" do |node|
    #         node.vm.box = IMAGE_NAME
    #         node.vm.network "private_network", ip: "192.168.50.#{i + 10}"
    #         node.vm.hostname = "node-#{i}"
    #         node.vm.provision "ansible" do |ansible|
    #             ansible.playbook = "ansible-setup/node-playbook.yml"
    #             ansible.extra_vars = {
    #               node_ip: "192.168.50.#{i + 10}",
    #               ansible_python_interpreter: "/usr/bin/python3",
    #             }
    #         end
    #     end
    # end
end
