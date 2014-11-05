require 'rubygems'

def setup_vm(node_name, node, port, master)
    node.vm.host_name = node_name
    node.vm.box = "precise32"
    node.vm.box_url = 'http://files.vagrantup.com/precise32.box'
    node.vm.forward_port(6379, port)

    node.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = ['cookbooks']
        chef.json.merge! :tz => 'America/Sao_Paulo'

        chef.add_recipe 'redisio'
        chef.add_recipe 'redisio::enable'


        if master
            chef.json = {
                'redisio' => {
                    'version' => '3.0.0-rc',
                    'requirepass' => 'foobared',
                    'servers' => [
                        {'address' => '0.0.0.0', 'port' => '6379' }
                    ]
                }
            }
        else
            chef.json = {
                'redisio' => {
                    'version' => '3.0.0-rc',
                    'requirepass' => 'foobared',
                    'servers' => [
                        {'address' => '0.0.0.0', 'port' => '6379', 'slaveof' => { 'address' => '127.0.0.1', 'port' => '6379' }}
                    ]
                }
            }
        end
    end
end


Vagrant::Config.run do |config|

    (1..2).each do |i|

        config.vm.define :master#{i} do |node|
            setup_vm("master#{i}", node, 6379, nil)
        end
        
        (1..2).each do |j|

            config.vm.define :node-#{i}-#{j} do |node|
                setup_vm("node-#{j}", node, 6379, "master#{i}")
            end
        end
    end
end
