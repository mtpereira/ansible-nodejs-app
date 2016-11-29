# -*- mode: ruby -*-
# vi: set ft=ruby ts=2 sw=2 tw=0 et :

boxes = {
  "ubuntu-trusty"  => {
                        :name => "ubuntu-trusty",
                        :box => "boxcutter/ubuntu1404",
                        :ip => '10.0.0.62',
                        :cpu => "100",
                        :ram => "256"
                      },
}

Vagrant.configure("2") do |config|
  boxes.each do |name, box|
    config.vm.define name do |machine|
      machine.vm.box = box[:box]
      machine.vm.box_url = box[:url]
      machine.vm.hostname = "%s" % box[:name]

      machine.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--cpuexecutioncap", box[:cpu]]
        v.customize ["modifyvm", :id, "--memory", box[:ram]]
      end

      machine.vm.network :private_network, ip: box[:ip]

      machine.vm.provision :shell do |shell|
        shell.inline = "sed -i -e 's/%sudo\tALL=NOPASSWD:ALL/%sudo\tALL=(ALL:ALL) ALL/' /etc/sudoers"
      end

       machine.vm.provision :ansible do |ansible|
         ansible.playbook = "tests/test.yml"
         ansible.tags = ENV['ANSIBLE_TAGS'] ||= "all"
         ansible.verbose = ENV['ANSIBLE_VERBOSE'] ||= "vv"
       end

#       machine.vm.provision :ansible_local do |ansible|
#         ansible.playbook          = "tests/test.yml"
#         ansible.galaxy_command    = "ansible-galaxy -vvv install --role-file=%{role_file} --roles-path=%{roles_path} --force"
#         ansible.galaxy_role_file  = "requirements.yml"
#         ansible.verbose           = "vvv"
#         ansible.install           = true
#         ansible.install_mode      = :pip
#         ansible.version           = "2.2.0.0"
#       end
    end
  end
end

