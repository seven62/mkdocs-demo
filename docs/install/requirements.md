# Requirements

Installation of ROCK can be broken down into three main steps:  

1. install
1. configure
1. deploy

Before that, let's cover what you're going to need before starting.  


## Sensor Hardware

The analysis of live network data is a resource intensive task.  The bottom line
is this: **if you throw hardware at ROCK it will use it, and use it well**. The
higher the IOPS the better.  Here's a starting point to get you moving:  

|   RESOURCE  |     RECOMMENDATION |
| ----------- | ------------------ |
| CPU         | 4 or more physical cores |
| Memory      | 16GB ( 8GB to start, more the better ) |
| Storage     | 256GB, with 200+ of that dedicated to `/data`, SSD preferred |
| Network     | 2 gigabit interfaces, one for management and one for collection |


## Install Media

- ROCK install image - download `.iso` **[here](https://download.rocknsm.io/isos/stable/)**
- 8GB+ capacity USB drive - to apply install image
- BIOS settings to allow booting from mounted USB drive


## Network Connection

ROCK is first and foremost a _**passive**_ network sensor and is designed with
the assumption that there may not be a network connection available during
install. There's some built in flexibility on how


This will be clarified more in then next sections.  
<br>
<br>

> NOTE: Check out the [ROCK@home Video Series](https://www.youtube.com/channel/UCUD0VHMKqPkdnJshsngZq9Q) that goes into detail on many things about deploying ROCK to include hardware choices for both sensor and network equipment.