# Basic Usage

## Key Interfaces

### Kibana - `https://localhost`

The generated credentials are in the home directory of the user created at install:  
<br>
`~/KIBANA_CREDS.README`  

### Docket - `https://localhost:8443`

Docket - web interface for pulling PCAP from the sensor (must be enabled in config)  

<br>
> localhost **or** IP of the management interface of the box  


## Functions Checks
After the initial build, the ES cluster will be yellow because the marvel index
will think it's missing a replica. Run this to fix this issue. This job will
run from cron just after midnight every day:  

    `/usr/local/bin/es_cleanup.sh 2>&1 > /dev/null`  

Check to see that the ES cluster says it's green:

    `curl -s localhost:9200/_cluster/health | jq '.'`  

See how many documents are in the indexes. The count should be non-zero:

    `curl -s localhost:9200/_all/_count | jq '.'`  

You can fire some traffic across the sensor at this point to see if it's collecting. NOTE: This requires that you upload your own test PCAP to the box.

    `sudo tcpreplay -i [your monitor interface] /path/to/a/test.pcap`  

After replaying some traffic, or just waiting a bit, the count should be going
up. You should have plain text bro logs showing up in /data/bro/logs/current/:  

    `ls -ltr /data/bro/logs/current/`  


## Rockctl

These functions are accomplished with:  

`sudo rock_status` - get the status of ROCK services

<!-- <p align="center">
<a href="https://asciinema.org/a/z9qgFqFTr9HoeSMpX2gKWXqng" target="\_blank"><img src="https://asciinema.org/a/z9qgFqFTr9HoeSMpX2gKWXqng.png" width="469"/></a>
</p> -->

`sudo rock_start` - start ROCK services

<!-- <p align="center">
<a href="https://asciinema.org/a/QAxK2iiWEw2bFRKUc5JFri3n9" target="\_blank"><img src="https://asciinema.org/a/QAxK2iiWEw2bFRKUc5JFri3n9.png" width="469"/></a>
</p> -->

`sudo rock_stop` - stop ROCK services

<!-- <p align="center">
<a href="https://asciinema.org/a/ME56ahRQrj3qmrynGzCc47GyM" target="\_blank"><img src="https://asciinema.org/a/ME56ahRQrj3qmrynGzCc47GyM.png" width="469"/></a>
</p> -->
