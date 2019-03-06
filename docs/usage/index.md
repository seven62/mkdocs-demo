# Basic Usage

## Key Interfaces

### Kibana - `https://localhost`

The generated credentials are in the home directory of the user created at install:  
<br>
`~/KIBANA_CREDS.README`  

### Docket - `https://localhost/app/docket/`

Docket - web interface for pulling PCAP from the sensor (must be enabled in config)  
<br>
> localhost **or** IP of the management interface of the box  


## Functions Checks

Check to see that the ES cluster says it's green:
```
curl -s localhost:9200/_cluster/health?pretty  
```
See how many documents are in the indexes. The count should be non-zero:
```
curl -s localhost:9200/_all/_count?pretty  
```
You can fire some traffic across the sensor at this point to see if it's collecting.

> NOTE: This requires that you upload your own test PCAP to the box.
```
sudo tcpreplay -i [your monitor interface] /path/to/a/test.pcap  
```
After a few moments of live traffic (or replaying a PCAP file), the document count should go
up. This can again be validated with `curl -s localhost:9200/_all/_count?pretty`

You should have plain text bro logs showing up in /data/bro/logs/current/:  
```
ls -ltr /data/bro/logs/current/  
```

## Rockctl

The basic service management functions are accomplished with:  

`sudo rockctl status` - get the status of ROCK services

<!-- <p align="center">
<a href="https://asciinema.org/a/z9qgFqFTr9HoeSMpX2gKWXqng" target="\_blank"><img src="https://asciinema.org/a/z9qgFqFTr9HoeSMpX2gKWXqng.png" width="469"/></a>
</p> -->

`sudo rockctl start` - start ROCK services

<!-- <p align="center">
<a href="https://asciinema.org/a/QAxK2iiWEw2bFRKUc5JFri3n9" target="\_blank"><img src="https://asciinema.org/a/QAxK2iiWEw2bFRKUc5JFri3n9.png" width="469"/></a>
</p> -->

`sudo rockctl stop` - stop ROCK services

<!-- <p align="center">
<a href="https://asciinema.org/a/ME56ahRQrj3qmrynGzCc47GyM" target="\_blank"><img src="https://asciinema.org/a/ME56ahRQrj3qmrynGzCc47GyM.png" width="469"/></a>
</p> -->

`sudo rockctl reset-failed` - clear the failed states of services
