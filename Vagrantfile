# Prioriy to running `vagrant up` you have to do:
# 1) Craete HDDs
# {
#   vboxmanage createmedium --filename $PWD/disk-1.vdi --size 1024 --format VDI
#   vboxmanage createmedium --filename $PWD/disk-2.vdi --size 1024 --format VDI
#   vboxmanage createmedium --filename $PWD/disk-3.vdi --size 1024 --format VDI
# }
# 2) Obtain avilable storage comtrollers names:
# - $ vboxmanage showvminfo sandbox

Vagrant.configure('2') do |config|

  # Enabling  X-Forwarding
  config.ssh.forward_x11 = true
  config.ssh.forward_agent = true

  # Config Files
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
      vm.cpus = 2
      vm.memory = 2048
      vm.name = 'sandbox'
    end
    node1.vm.hostname = 'sandbox'
    node1.vm.network 'private_network', ip: '192.168.100.100'
  end

end
