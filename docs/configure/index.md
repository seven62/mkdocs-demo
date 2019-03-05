# Configuration

After installation your sensor configuration will need to be customized.  This can be done by local login, or remotely via ssh.


## Config File
The primary configuration file for ROCK is [/etc/rocknsm/config.yml](https://github.com/rocknsm/rock/blob/master/playbooks/templates/rock_config.yml.j2).  This file contains key variables like network interface setup, cpu cores assignment, and much more.  There are a lot of options to tune here, so take time to familiarize.  Let's break down this file into it's major sections:  


### Network Interface
As mentioned previously, ROCK takes the interface with an ip address / gateway and will use that as the _management_ NIC.  Beginning at line 8, `config.yml` displays the remaining interfaces that will be used to **MONITOR** traffic.

Let's run through a basic example:  
```
[admin@rock ~]$ ip a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether ...
    inet 192.168.1.207/24 brd 192.168.1.255 scope global noprefixroute dynamic enp0s3
    ...
3: enp0s4: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether ...
```

The demo box above has 2 NICs:  
1. `enp0s3` - is plugged in for install and deployment with an ip address from local dhcp. This will be used to **manage** the sensor  
2. `enp0s4` - will be unused (not connected) during install and deployment and be listed as a `rock_monif` in the config file

Lines 7 - 9 of `/etc/rocknsm/config.yml` show that the other interface (`enp0s3`) is listed as MONITOR interface.
```yml
# interfaces that should be configured for sensor applications
rock_monifs:
    - enp0s3
```


### Sensor Resource

```yml
# Set the hostname of the sensor:
rock_hostname:

# Set the Fully Qualified Domain Name:
rock_fqdn:

# Set the number of CPUs assigned to Bro:
bro_cpu:

# Set the Elasticsearch cluster name:
es_cluster_name:

# Set the Elasticsearch cluster node name:
es_node_name:

# Set the value of Elasticsearch memory:
es_mem:
```


### Installation Source
We've taken into consideration that your sensor won't always have internet access.  The ISO's default value is set to offline:  

```yml
53  # The primary installation variable defines the ROCK installation method:
54  # ONLINE:   used if the system may reach out to the internet
55  # OFFLINE:  used if the system may *NOT* reach out to the internet
56  # The default value "False" will deploy using OFFLINE (local) repos.
57  # A value of "True" will perform an install using ONLINE mirrors.
58
59  rock_online_install: True
```

If your sensor has access to online repos just set `rock_online_install: True`, Ansible will configure your system for the yum repositories listed and pull packages and git repos directly from the URLs shown. You can easily point this to local mirrors if needed.  

If this value is set to `False`, Ansible will look at the cached files in `/srv/rocknsm`.


### Data Retention
This section controls how long NSM data stay on the sensor:  
```yml
# Set the interval in which Elasticsearch indexes are closed:
elastic_close_interval:

# Set the interval in which Elasticsearch indexes are deleted:
elastic_delete_interval:

# Set value for Kafka retention (in hours):
kafka_retention:

# Set value for Bro log retention (in days):
bro_log_retention:

# Set value for Bro statistics log retention (in days):
bro_stats_retention:

# Set how often logrotate will roll Suricata log (in days):
suricata_retention:

# Set value for FSF log retention (in days):
fsf_retention:
```


### ROCK Component Options
This is a critical section that provides boolean options to choose what components of ROCK are **_installed_** and **_enabled_** during deployment.  

```yml
# The following "with_" statements define what components of RockNSM are
# installed when running the deploy script:

with_stenographer: True
with_docket: True
with_bro: True
with_suricata: True
with_snort: True
with_suricata_update: True
with_logstash: True
with_elasticsearch: True
with_kibana: True
with_zookeeper: True
with_kafka: True
with_lighttpd: True
with_fsf: True

# The following "enable_" statements define what RockNSM component services
# are enabled (start automatically on system boot):

enable_stenographer: True
enable_docket: True
enable_bro: True
enable_suricata: True
enable_snort: True
enable_suricata_update: True
enable_logstash: True
enable_elasticsearch: True
enable_kibana: True
enable_zookeeper: True
enable_kafka: True
enable_lighttpd: True
enable_fsf: True
```

A good example for changing this section would involve [Stenographer](../services/stenographer.md). Collecting raw PCAP is resource and _**storage intensive**_.  You're machine may not be able to handle that and if you just wanted to focus on network logs, then you would set both options in the config file to **disable** installing and enabling Stenographer:  

```yml
67 with_stenographer: False
  ...
  ...
  ...
83 enable_stenographer: False
```
