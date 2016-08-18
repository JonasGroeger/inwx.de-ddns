# inwx.de-ddns

This script updates your public IPv4 / IPv6 address at [inwx.de](https://inwx.de/) using their API.
It is intended to be run on a Synology NAS but you can run it on any other device.

## Features

* Only updates your IP if it changed
* Asks a pool of public IP address APIs
* Good error handling
* Timestamped logs
* Silent mode

## Requirements

* bash
* curl
* sed
* grep

## Installation

```
cd /root/
git clone git@github.com:JonasGroeger/inwx.de-ddns.git
cd inwx.de-ddns
```

## Configuration

Enter your username, password and both your record IDs in there. You can get the
record ids like this:

* Go to [https://www.inwx.de/domainlist](https://www.inwx.de/domainlist)
* Click the gear icon on the right and select "DNS records".
* Click `Add DNS entry`, create two records and click `Save`:

```
nas.domain.com A    127.0.0.1 3600
nas.domain.com AAAA ::1       3600
```

* Find the IDs in the source code of the website. You can also use the element picker of Chrome / Firefox / etc. Its usually something like `record_div_XXXXXXXX". Take only the XXXXXXXX part.

Then, enter the IDs as well as your credentials in the `dnsupdate` script:

```
cd /root/inwx.de-ddns/
vim dnsupdate
```

In the DSM you can create a scheduled task that runs this script every X minutes:

* Scheduled Tasks (calendar icon)
* Create -> Planned Task -> User defined task
* Name it somehow and make sure the user is `root`. Make sure its `activated`.
* Run it as often as you want and in the `Execute command` area enter the following:

```
cd /root/inwx.de-ddns/ && bash dnsupdate
```

There you go. If you have questions, please create an issue.
