# Suricata

[Suricata](https://suricata-ids.org/) is IDS / Alerting solution in RockNSM.


## Overview

Intrusion Detection Systems (IDS) are a great way to quickly alert on known bad.
Alerts are triggered when a packet matches a defined pattern or _**signature**_.


## Management

The Suricata service is configured and enabled on startup.

### Updating Rules

The newest versions of Suricata come with the `suricata-update` command to
manange and update rulesets. The official documentation is found
[here](https://suricata.readthedocs.io/en/suricata-4.1.2/rule-management/suricata-update.html).

### Service

Suricata is deployed as a systemd unit, called **suricata**. Normal systemd
procedures apply here:

```
sudo systemctl start suricata
sudo systemctl status suricata
sudo systemctl stop suricata
sudo systemctl restart suricata
```

It can also be managed using the `rockctl` command.


## Directories

`/etc/suricata/` - configuration path
