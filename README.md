# Vagrant Centos / Rackspace Workaround

Vagrant will not work properly with CentOS out of the box. 
This has to do with how vagrant handles ssh sessions and how 
the sudoers file is configured by default on CentOS.

This isssue is confirmed on CentOS and assumed to affect all
RHEL variants.

The "worst" part is that we must do this for every dc we wish 
to deploy to with vagrant.

**NOTE:** There is currently a problem with the vagrant-rackspace plugin. 
Please refer to [Pull Request 11](https://github.com/mitchellh/vagrant-rackspace/pull/11) for details. 
This fix is *required* to be able to deploy to ORD with vagrant.  If you are
only interested in DFW, then you can skip this step.

**NOTE:** There is also an issue with LON. A bit of a dirty
workaround can be seen in [Pull Request 4](https://github.com/mitchellh/vagrant-rackspace/pull/4)

## Usage

 - ensure vagrant is installed via package: [Vagrant Downloads](http://downloads.vagrantup.com/)
 - `vagrant plugin install vagrant-rackspace`
 - `git clone git@github.rackspace.com:lefty/vagrant-centos-rackspace-workaround.git`
 - `cd vagrant-centos-rackspace-workaround`
 - `vagrant box add dummy https://github.com/mitchellh/vagrant-rackspace/raw/master/dummy.box`
 - edit `Vagrantfile` adding in your username and api key
 - `vagrant up`
 - use vagrant to ssh in to each machine. e.g. `vagrant ssh temp-centos-6-dfw`
 - `visudo`
 - comment out `Defaults    requiretty`
 - comment out `Defaults   !visiblepw`
 - save file and logout of machine
 - from the control panel, create an image of that machine with a name like "vagrant-centos-6-dfw"

## Error Details

**Error:**

```
The following SSH command responded with a non-zero exit status.
Vagrant assumes that this means the command failed!

echo $(chef-solo --v | awk "{print \$2}" || "")
```

The only workaround at this time is to create a custom image with sudoers
configured to work with vagrant.

**Fix:**

 - create machine manually or with vagrant (suggest a small instance)
 - ssh into machine as root and edit `/etc/sudoers` with `visudo`
 - comment out `Defaults    requiretty`
 - comment out `Defaults   !visiblepw`
 - from the control panel, create an image of that machine
 - update `Vagrantfile` to use the new image instead of the "normal" one

**Note:** If you need to create CentOS / RHEL machines in multiple dc's, you
will need to do this for *every* dc.
