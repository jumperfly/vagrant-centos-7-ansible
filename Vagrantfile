# -*- mode: ruby -*-
# vi: set ft=ruby :

$centos_version = "1804.02.01"
$ansible_version = "2.6.4"

Vagrant.configure("2") do |config|
  config.vm.box = "jumperfly/centos-7"
  config.vm.box_version = $centos_version
  config.vm.box_check_update = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |v|
    v.memory = 512
    v.cpus = 1
  end

  config.vm.provision "shell", inline: <<-SHELL
    # Install
    curl https://bootstrap.pypa.io/get-pip.py -o /tmp/get-pip.py
    python /tmp/get-pip.py
    pip install ansible==#{$ansible_version}

    # Cleanup
    rm -f /etc/ssh/*key*
    rm -f /tmp/get-pip.py
    yum clean all
    rm -rf /var/cache/yum
    dd if=/dev/zero of=/boot/ZERO bs=1M
    rm /boot/ZERO
    dd if=/dev/zero of=/ZERO bs=1M
    rm /ZERO
    swapoff /dev/mapper/VolGroup00-LogVol01
    dd if=/dev/zero of=/dev/mapper/VolGroup00-LogVol01 bs=1M
    mkswap /dev/mapper/VolGroup00-LogVol01
    sync
    echo "All done! Machine will now shutdown ready for a 'vagrant package'..."
    history -c && poweroff
  SHELL
end
