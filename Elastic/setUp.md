# Set-Up
I will be running Elastic 7.17 on Ubuntu 20.04 for this home lab set-up. Once I am able to acquire more resources and better hardware, I will catch up to the latest version of Elastic stack.

### Set-up
- Download Ubuntu Server 20.04
- Install .iso as a virtual machine
- Configure network settings
    - I am using a static IP address so that the SIEM IP always stays the same.
- Complete set-up of virtual machine basics
- Update & Upgrade
    - `sudo apt update -y && sudo apt upgrade -y`

### Install Java
- `sudo apt install default-jre`

### Install elasticsearch
- Go to elastic website and download Elasticsearch
- scp elasticsearch to the vm
- Install elasticsearch
    - extract the tar.gz
        - `tar xvf elasticsearch-<version>.tar.gz`
        - `mv elasticsearch-<version> /usr/local`
        