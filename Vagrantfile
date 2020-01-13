servers=[
  {
    :hostname => "server",
    :ip => "192.168.11.100",
    :box => "centos/7",
    :playbook => "./provision/playbook.yml",
    :ram => 1024,
    :cpu => 2
  }
]

Vagrant.configure(2) do |config|
    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network "private_network", ip: machine[:ip]
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = machine[:playbook]
            end
            node.vm.provider "virtualbox" do |vb|
                vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
            end
        end
    end
end

