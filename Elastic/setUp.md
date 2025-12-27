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

### Install Kibana
- `sudo apt install kibana=7.17.29`

### Configure Kibana
- Open kibana config file
    - Adjust network settings and elasticsearch settings
    - Ensure to set `network.host` to `0.0.0.0`
    - Ensure to put the actual IP or hostname of your elasticsearch server.

### Enable and Start Kibana
- `sudo systemctl daemon-reload`
- `sudo systemctl enable kibana`
- `sudo systemctl start kibana`

### Verify Your Install
- Go to the webpage
    - http://localhost:5601
- ***It may take a minute for it to register***


### Install Logstash
- `sudo apt install logstash`

### Configure Logstash

### Set-up rsyslogd to ingest firewall logs
- Edit rsyslog configuration
    - `sudo vim /etc/rsyslog.conf`
    - Uncomment UDP/TCP configs
- Restart rsyslog
    - `sudo systemctl restart rsyslog`
- Add rule to catch firewall traffic
    - `if $fromhost-ip == '< ip address >' then /var/log/pfsense.log`
    - `if $fromhost-ip == '192.168.1.1' then { action(type="omfile" file="/var/log/pfsense.log") stop }`

### Install Filebeat
- `sudo apt install filebeat`

### Set-up Modules.d config
- `vim pfsense.yml`
- `- module: system`
- `syslog:`
-   `enabled: true`
-   `var.paths: ["/var/log/pfsense.log"]`


### Check the magic in the SIEM
