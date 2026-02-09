# Build
For this example, I will be putting KVM onto an Ubuntu Server 24.04 image on bare metal.

#### Install required packages
`sudo apt update`\
`sudo apt install -y qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager`


#### Verify Installation
- List VMs
`sudo virsh list --all`

- Check KVM status
`sudo systemctl status libvirtd`
  - If it is active then you are good to go.

- Add User to KVM and Libvirt groups
`sudo usermod -aG kvm,libvirt $USER`

#### Install Cockpit
- Install package
`sudo apt install cockpit`

- Go to webpage
`https[:]//x.x.x.x:9090`
