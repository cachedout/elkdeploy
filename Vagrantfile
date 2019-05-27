Vagrant.configure("2") do |config|

#  config.vm.synced_folder "salt/roots/", "/srv/salt/"
#  config.vm.box = "archlinux/archlinux"
#  config.vm.box_version = "2019.04.05"
#  config.vm.box = "centos/7"
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end
  config.vm.define "es1.prod" do |es1_prod|
    es1_prod.vm.network :private_network, ip: "10.0.0.10"
    es1_prod.vm.network :forwarded_port, guest: 9200, host: 9200
    es1_prod.vm.network :forwarded_port, guest: 9300, host: 9300
    es1_prod.vm.network :forwarded_port, guest: 22, host: 1234
    es1_prod.vm.provision "ansible_local" do |ansible|
      ansible.become = true
      ansible.playbook = "deploy.yml"
    end
  end

  config.vm.define "kb1.prod" do |kb1_prod|
    kb1_prod.vm.network :private_network, ip: "10.0.0.11"
    kb1_prod.vm.network :forwarded_port, guest: 5601, host: 5601
    kb1_prod.vm.network :forwarded_port, guest: 22, host: 1235
    kb1_prod.vm.provision "ansible_local" do |ansible|
      ansible.become = true
      ansible.playbook = "deploy.yml"
    end
  end

  config.vm.define "ls1.prod" do |ls1_prod|
    ls1_prod.vm.network :private_network, ip: "10.0.0.12"
    ls1_prod.vm.network :forwarded_port, guest: 5044, host: 5044
    ls1_prod.vm.network :forwarded_port, guest: 9600, host: 9600
    ls1_prod.vm.network :forwarded_port, guest: 22, host: 1236
    ls1_prod.vm.provision "ansible_local" do |ansible|
      ansible.become = true
      ansible.playbook = "deploy.yml"
    end
  end

  config.vm.define "bs1.prod" do |bs1_prod|
    bs1_prod.vm.network :private_network, ip: "10.0.0.13"
    bs1_prod.vm.provision "ansible_local" do |ansible|
      ansible.become = true
      ansible.playbook = "deploy.yml"
    end
  end

  config.vm.define "es1.mon" do |es1_mon|
    es1_mon.vm.network :private_network, ip: "10.0.0.20"
    es1_mon.vm.network :forwarded_port, guest: 10200, host: 10200
    es1_mon.vm.network :forwarded_port, guest: 10300, host: 10300
    es1_mon.vm.network :forwarded_port, guest: 22, host: 2234
    es1_mon.vm.provision "ansible_local" do |ansible|
      ansible.extra_vars = {elasticsearch_http_port: "10200", elasticsearch_network_host: "10.0.0.20"}
      ansible.become = true
      ansible.playbook = "deploy.yml"
    end
  end

  config.vm.define "kb1.mon" do |kb1_mon|
    kb1_mon.vm.network :private_network, ip: "10.0.0.11"
    kb1_mon.vm.network :forwarded_port, guest: 5601, host: 6601
    kb1_mon.vm.network :forwarded_port, guest: 22, host: 2235
    kb1_mon.vm.provision "ansible_local" do |ansible|
      ansible.extra_vars = {kibana_elasticsearch_url: "http://10.0.0.20:10200"}
      ansible.become = true
      ansible.playbook = "deploy.yml"
    end
  end

end
