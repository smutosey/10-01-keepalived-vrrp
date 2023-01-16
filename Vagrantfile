# -*- mode: ruby -*-
# vi: set ft=ruby :

# Массив виртмашин
virt_machines=[
  {
    :hostname => "node-1",
    :ip_public => "192.168.0.201",
    :ip_private => "192.168.1.1",
  },
  {
    :hostname => "node-2",
    :ip_public => "192.168.0.202",
    :ip_private => "192.168.1.2",
  }
]

# Show VM GUI
# Показывать гуй виртмашины
HOST_SHOW_GUI = false 

# VM RAM
# Оперативная память ВМ
HOST_MEMMORY = "1024" 

# VM vCPU
# Количество ядер ВМ
HOST_CPUS = 1

# Network adapter to bridge
# В какой сетевой адаптер делать бридж
#HOST_BRIDGE = "Intel(R) Ethernet Connection (2) I219-V" 
HOST_BRIDGE = "Ethernet Ethernet"

# Which box to use
# Из какого бокса выкатываемся
HOST_VM_BOX = "generic/ubuntu2004" 

################################################
# Parameters passed to provision script
# Параметры передаваемые в скрипт инициализации
################################################

# Script to use while provisioning
# Скрипт который будет запущен в процессе настройки
HOST_CONFIG_SCRIPT = "config.sh" 

# Additional user
# Дополнительный пользователь
HOST_USER = 'test'

# Additional user pass. Root pass will be same
# Пароль дополнительного пользователя. Пароль рута будет таким же
HOST_USER_PASS = '1' 

# Run apt dist-upgrade
# Выполнить apt dist-upgrade
HOST_UPGRADE = 'true' 

Vagrant.configure("2") do |config|
	virt_machines.each do |machine|
		config.vm.box = HOST_VM_BOX
		config.vm.define machine[:hostname] do |node|
			node.vm.hostname = machine[:hostname]
			node.vm.network :public_network, bridge: HOST_BRIDGE, ip: machine[:ip_public]
      node.vm.network :private_network, ip: machine[:ip_private]
			node.vm.provider "virtualbox" do |current_vm, override|
				current_vm.name = machine[:hostname]
				current_vm.gui = HOST_SHOW_GUI
				current_vm.memory = HOST_MEMMORY
				current_vm.cpus = HOST_CPUS
				override.vm.provision "shell", path: HOST_CONFIG_SCRIPT, args: [ 'test', HOST_USER_PASS, HOST_UPGRADE, machine[:hostname], machine[:ip_public], machine[:ip_private]], run: "once"
			end
		end
	end
end