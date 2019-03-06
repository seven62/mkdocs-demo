# Deployment

## Deploy
Once `/etc/rocknsm/config.yml` has been tuned to suit your environment, it's
finally time to **deploy this thing**.  This is done by running the deployment
script, which is in the install user's path (`/usr/sbin/`).

<!-- ```
/usr/sbin/
├── ...
├── deploy_rock.sh.sh
├── ...
``` -->

To kick off the deployment script run:  `sudo deploy_rock.sh`  

Once the deployment is completed with the components you chose, you'll be
congratulated with a success banner.  

<p align="center">
<img src="../img/install_banner.png">
</p>
<!-- <p align="center">
<a href="https://asciinema.org/a/2rS2u1fJzhaNVtkuKWgqd5BQl" target="\_blank"><img src="https://asciinema.org/a/2rS2u1fJzhaNVtkuKWgqd5BQl.png" width="469"/></a>
</p>   -->


## Generate Defaults
> What do I do when I've completely messed things up and need to start over?

Great question.  There's a simple solution for when the base config file needs
to be reset back to default settings. There's a generate_defaults script also
located in your `$PATH`. Simply execute this to regenerate a fresh default
config file ( `/etc/rocknsm/config.yml` ) for you and get you out of jail:  

`sudo generate_defaults.sh`  

This effectively reverts things to factory defaults, and you can then revisit
your config file.  


## Initial Kibana Access
We strive to do the little things right, so rather than having Kibana available
to everyone in the free world, it's sitting behind a reverse proxy and secured
by a [passphrase](https://xkcd.com/936/).  The credentials are generated and
then stored in the home directory of the user you created during the initial
installation e.g. `/home/admin`.

To get into Kibana:  

1. `cat` and copy the contents of `~/KIBANA_CREDS.README`
1. browse to `https://<sensor-management-IP>`
1. enter this user / password combo
1. profit!
