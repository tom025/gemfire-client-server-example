# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.landrush.enabled = true
  config.landrush.tld = 'gemfire-example.dev'

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y python
  SHELL

  config.vm.define('gemfire-locator') do |locator|
    locator.vm.hostname = 'gemfire-locator.gemfire-example.dev'
  end
end
