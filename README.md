# kvm commands
Quick Command List For KVM 

**Create VM**

sudo virt-install --name Ubuntu-18.04 --ram=2048 --vcpus=1 --cpu host --hvm --disk path=/var/lib/libvirt/images/ubuntu-18.04-vm1,size=10 --cdrom /home/ostechnix/ubuntu18.iso --network bridge=br0 --graphics vnc


**Check the port that vnc is running on to install the os via vnc viewer**

sudo virsh dumpxml Ubuntu-18.04 | grep vnc

Example output:

<graphics type='vnc' port='5900' autoport='yes' listen='127.0.0.1'>


**Create ssh port forward to connect vnc over**

ssh andrew@192.168.0.2 -L 5900:127.0.0.1:5900

**List running vm’s**

sudo virsh list


**Start vm’s**

sudo virsh start Ubuntu-18.04

**Reboot vm’s**

sudo virsh reboot Ubuntu-18.04


**Pause vm’s**

sudo suspend Ubuntu-18.04


**Resume vm’s**

sudo virsh resume Ubuntu-18.04


**Shutdown vm’s**

sudo virsh shutdown Ubuntu-18.04


**Delete vm’s**

sudo virsh undefine Ubuntu-18.04

sudo virsh destroy Ubuntu-18.04

**Add cpu or memory to a vm that’s already built**

virsh shutdown Ubuntu-18.04

**Edit vm**

Virsh edit Ubuntu-18.04

**Edit line <memory unit='KiB'>4194304</memory>**

**And cpu line**

**Save and exit**

**Add disk to a vm**

cd /var/lib/libvirt/images/

 qemu-img create -f raw myRHELVM1-disk2.img 7G
Formatting 'Ubuntu-18.04-disk2.img', fmt=raw size=7516192768

**Attach newly created disk **

virsh attach-disk Ubuntu-18.04 --source /var/lib/libvirt/images/Ubuntu-18.04-disk2.img --target vdb --persistent
Disk attached successfully

**Save Virtual Machine Configuration**

virsh dumpxml Ubuntu-18.04 > Ubuntu-18.04.xml

Once you have the configuration file in the XML format, you can always recreate your guest VM from this XML file, using virsh create command as shown below:
virsh create myrhelvm1.xml


**Remove disk image after deleting vm**

rm /var/lib/libvirt/images/Ubuntu-18.04-disk1.img
