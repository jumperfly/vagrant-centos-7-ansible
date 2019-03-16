# Vagrant CentOS 7 Ansible
Adds Virtual Box guest additions and Ansible to the official centos/7 Vagrant box.
To build simply run:
```
vagrant up
# Wait for build to complete and VM to shutdown
vagrant package
```

To test the build image run:
```
cd tests
vagrant up
vagrant destroy
vagrant box remove test
cd ..
```

The generated box file can then be used or deployed to a box repository.
