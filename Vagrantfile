# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provision "file",
    source: "elastic.repo", destination: "/tmp/elastic.repo"
  config.vm.provision "shell", 
    inline: "sudo yum install -y vim java-1.8.0-openjdk
              sudo mv /tmp/elastic.repo /etc/yum.repos.d/"
  config.vm.box = "centos/7"
  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
    v.memory = 2048
  end

  config.vm.define "elasticsearch" do |els|
    els.vm.hostname = "elastic-search"
    els.vm.network "private_network", ip: "10.10.10.10"
    els.vm.provision "shell", inline: "sudo yum install -y elasticsearch metricbeat filebeat"
  end

  config.vm.define "logstash" do |logs|
    logs.vm.hostname = "log-stash"
    logs.vm.network "private_network", ip: "10.10.10.20"
    logs.vm.provision "shell", inline: "sudo yum install -y logstash metricbeat filebeat"
  end

  config.vm.define "kibana" do |kib|
    kib.vm.hostname = "kibana"
    kib.vm.network "private_network", ip: "10.10.10.30"
    kib.vm.provision "shell", inline: "sudo yum install -y kibana metricbeat filebeat"
  end

end
