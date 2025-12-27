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

### Install Necessary Packages
- `sudo apt install apt-transport-https gnupg2 wget`

### Install elasticsearch
- Import the Elasticsearch GPG Key
    - `wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -`
- Add the elastic APT repository
    - `sudo echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" > /etc/apt/sources.list.d/elastic-7.x.list`
- If you are running multiple servers (e.g Elasticsearch vm#1 and logstash,kibana,etc vm#2) you need to complete everything above this line for every server.
- Update and install Elasticsearch
    - `sudo apt update && sudo apt install elasticsearch=7.17.29 -y`

### Configure Elasticsearch
- Open elasticsearch config file
    - `sudo vim /etc/elasticsearch/elasticsearch.yml`
    - Make any network or memory setting adjustments that you need to
- Open jvm config file
    - `sudo vim /etc/elasticsearch/jvm.options`
    - Adjust heap size as needed

### Start and Enable Elasticsearch
- `sudo systemctl daemon-reload`
- `sudo systemctl enable elasticsearch`
- `sudo systemctl start elasticsearch`

### Verify Your Install
- `curl -X GET http://localhost:9200`

