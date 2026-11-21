# -*- mode: ruby -*-
# Создаёт отдельный сервер FreeIPA и два клиента VirtualBox.
machines = {
  "ipa" => ["ipa.otus.lan", "192.168.57.10", 4096, 4],
  "client1" => ["client1.otus.lan", "192.168.57.11", 1024, 4],
  "client2" => ["client2.otus.lan", "192.168.57.12", 1024, 1]
}

Vagrant.configure("2") do |config|
  config.vm.box = "otus/centos-stream9"
  config.vm.box_url = "https://cloud.centos.org/centos/9-stream/x86_64/images/CentOS-Stream-Vagrant-VirtualBox-9-latest.x86_64.vagrant-virtualbox.box"
  config.vm.boot_timeout = 1800
  config.vm.box_check_update = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  machines.each do |name, (fqdn, ip, memory, cpus)|
    config.vm.define name do |vm|
      vm.vm.hostname = fqdn
      vm.vm.network "private_network", ip: ip, netmask: "255.255.255.0",
                    virtualbox__intnet: "otus-freeipa-centos"

      vm.vm.provider "virtualbox" do |vb|
        vb.name = "otus-ldap-centos-#{name}"
        vb.memory = memory
        vb.cpus = cpus
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      end

      vm.vm.provision "ansible" do |ansible|
        ansible.playbook = name == "ipa" ? "ansible/server.yml" : "ansible/client.yml"
        ansible.extra_vars = {
          ipa_node_fqdn: fqdn,
          ipa_node_ip: ip,
          ansible_timeout: 1800
        }
      end
    end
  end
end

# Версия 2 | 2026-11-21 | CentOS Stream 9, ресурсы и тайм-ауты.
