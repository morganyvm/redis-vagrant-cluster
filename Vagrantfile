require 'rubygems'

def setup_vm(shard_name, shard, port)
    shard.vm.host_name = shard_name
    shard.vm.box = "precise32"
    shard.vm.box_url = 'http://files.vagrantup.com/precise32.box'
    shard.vm.forward_port(6379, port)

    shard.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = ['cookbooks']
        chef.json.merge! :tz => 'America/Sao_Paulo'

        chef.add_recipe 'redis::source'

        chef.json = {
            'redis' => {
                'source' => {
                    'version' => '2.8.17',
                },
                'password' => 'foobared',
                'bind' => "0.0.0.0"
            }
        }
    end
end


Vagrant::Config.run do |config|

    config.vm.define :shard do |shard|
        setup_vm("shardA", shard, 6379)
    end

    config.vm.define :shard2 do |shard|
        setup_vm("shardB", shard, 6380)
    end

end
