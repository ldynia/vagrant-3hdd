Vagrant.configure('2') do |config|

  config.vm.box = 'centos/7'

  config.vm.provider 'virtualbox' do |vb|
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
    vb.customize ['storageattach', :id,
      '--storagectl', 'IDE',
      '--port', 0,
      '--device', 1,
      '--type', 'hdd',
      '--medium', File.absolute_path('disk-1.vdi'),
    ]
    vb.customize ['storageattach', :id,
      '--storagectl', 'IDE',
      '--port', 1,
      '--device', 0,
      '--type', 'hdd',
      '--medium', File.absolute_path('disk-2.vdi'),
    ]
    vb.customize ['storageattach', :id,
      '--storagectl', 'IDE',
      '--port', 1,
      '--device', 1,
      '--type', 'hdd',
      '--medium', File.absolute_path('disk-3.vdi'),
    ]
  end

  config.vm.define 'sandbox' do |node1|
    node1.vm.provider 'virtualbox' do |vm|
      vm.cpus = 1
      vm.memory = 512
      vm.name = 'sandbox'
    end
  end


  # Provision machine
  config.vm.provision :shell, :inline  => '
   sudo yum install -y lvm2*
  '

end
