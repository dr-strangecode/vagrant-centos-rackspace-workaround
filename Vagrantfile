# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "dummy"

  #####
  # DFW
  #####

  # use to create image needed for each dc - must fix sudoers file and create image from this machine
  config.vm.define 'temp-centos-6-dfw' do |c|
    c.vm.provider :rackspace do |rs|
      rs.username = ""
      rs.api_key = ""
      rs.flavor = /512MB/
      rs.image = /CentOS 6.3/
      rs.rackspace_region = :dfw
      rs.server_name = 'temp-centos-6-dfw'
    end
  end

  #####
  # ORD
  #####

  # use to create image needed for each dc - must fix sudoers file and create image from this machine
  config.vm.define 'temp-centos-6-ord' do |c|
    c.vm.provider :rackspace do |rs|
      rs.username = ""
      rs.api_key = ""
      rs.flavor = /512MB/
      rs.image = /CentOS 6.3/
      rs.rackspace_region = :ord
      rs.server_name = 'temp-centos-6-ord'
    end
  end


end
