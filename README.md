Nextcloud VM
============

Server installation. Simplified. :cloud:
--------------------------------

#### Interactive Guidance
> **The Nextcloud VM** — _(aka **N**ext**c**loud **V**irtual **M**achine_ or _**NcVM**)_ — helps you create a personal or corporate [Nextcloud Server] _faster_ and _easier._ Fundamentally, NcVM is a carefully crafted _family_ of [\*nix] scripts which interactively guide you through a quality-controlled installation to obtain an [A+ security-rated] Nextcloud instance.

#### Curated Extras
> The Nextcloud [app store] extends core features by allowing you to enable a multitude of free one-click apps. However, _integration apps_ there like [Collabora Online] and [ONLYOFFICE] are solely _bridges_ to Nextcloud. You’re still required to install those services _separately_, which can be complex. NcVM provides optional _**full installation of select curated apps**_, including those and others. Monitor and manage your cloud using any web browser with NcVM’s hand-picked collection of power utilities featuring stunning, modern UIs.

#### All Systems Go
> NcVM can check for and install _stable_ updates to keep things current, smooth, and secure.

--------------------

## Build your own Nextcloud VM
How to build your own Nextcloud VM from scratch
25th April 2019, 20:21 — revised 24th September 2019, 18:57

1. Digitalocean example
  
DigitalOcean example: https://youtu.be/LlqY5Y6P9Oc
The script will mount and format the drive. Please select Manually Format & Mount when adding the second volume.

2. Minimum System Requirements
  
A clean Ubuntu Server 18.04.X using the alternative installer
OpenSSH (preferred)
20 GB HDD for OS
XX GB HDD for DATA (/mnt/ncdata)
Absolute minimum is 1 vCPU and 2 GB RAM (4 GB minimum if you are running OnlyOffice)
A working internet connection (the script needs it to download files and variables)
VMware Player (fully tested with Hyper-V and KVM as well). It would also work on a bare-metal server/computer/laptop of course.
2.1  Recomended
  
DHCP available
40 GB HDD for OS
4 vCPU
4 GB RAM
Ports 80 and 443 open to the server. Here’s why port 80 is recomended. Yes: the VM handles redirection to 443.

3. Installation overview
  
Two scripts run consecutively to create your Nextcloud instance, seperated by a reboot. The first script (nextcloud_install_production.sh) is used to to the main installation, e.g. when installing it on a new server. It helps you choose and install features, create your user account, and then reboots. After the VM reboots and you login with the new user name you created, the second script (nextcloud-startup-script.sh) completes setup.

4. Installation: Step-by-step
  
STEP 1 — Download and execute the latest Nextcloud VM installer script using super user do (sudo):

sudo bash -c "$(wget -q -O - https://raw.githubusercontent.com/tgd1973/Nexcloud-vm/master/nextcloud_install_production.sh)"

After the first script completes …

STEP 2 — The VM automatically reboots.

STEP 3 — Login with your new user name locally or remotely (via CLI: ssh <user>@IP-ADDRESS). The second script executes and completes installation.
  
AN IMPORTANT NOTE:
*If the VM automatically runs as root after rebooting, press CTRL+C to abort nextcloud-startup-script.sh. Then manually run the startup script as your newly-created user:* sudo su (user) then: sudo bash /var/scripts/nextcloud-startup-script.sh — Setup is not finished after running the first script. Both must execute consecutively.

--------------------

## Support the development
* [Create a PR](https://help.github.com/articles/creating-a-pull-request/) and improve the code
* Report [your issue](https://github.com/nextcloud/vm/issues/new)
* Help us with [existing issues](https://github.com/nextcloud/vm/issues)

  
## Full documentation
* [VM](https://docs.hanssonit.se/s/W6fMouPiqQz3_Mog/virtual-machines-vm/d/W6fMquPiqQz3_Moi/nextcloud-vm) (the easiest option)
* [Install with scripts](https://docs.hanssonit.se/s/bj0vl1ihv0jgrmfm08j0/build-your-own/d/bj0vl4ahv0jgrmfm0950/nextcloud-vm) (if you feel brave)
* [FAQ](https://docs.hanssonit.se/s/bj101nihv0jgrmfm09f0/faq/d/bj101pihv0jgrmfm0a10/nextcloud-vm?currentPageId=bj101sqhv0jgrmfm0a1g) (Frequently Asked Questions)
* [Machine configuration](https://docs.hanssonit.se/s/W6fMouPiqQz3_Mog/virtual-machines-vm/d/W7Du9uPiqQz3_Mr1/machine-setup-nextcloud-vm) (of the released version)

## If You want to test a Release Candidate (RC), or Beta!
No problem, brave explorer! We made it simple. 

In some cases we do pre-releases of the VM as well. Those can be found in the [TESTING](https://cloud.hanssonit.se/s/zjsqkrSpzqJGE9N?path=%2FTESTING) folder on the download server. If you want to try the latest version yourself, just follow the steps below:
1. Download the latest [nextcloud_update.sh](https://raw.githubusercontent.com/nextcloud/vm/master/nextcloud_update.sh) to your server.
2. Put the below variables right above line 256 **(# Major versions unsupported)**
3. Run nextcloud_update.sh

To test a specific RC version:

```
NCREPO="https://download.nextcloud.com/server/prereleases"
NCVERSION=16.0.0RC1
STABLEVERSION="nextcloud-$NCVERSION"
```

Or the latest Beta:
```
NCREPO="https://download.nextcloud.com/server/prereleases"
NCVERSION=$(curl -s -m 900 $NCREPO/ | sed --silent 's/.*href="nextcloud-\([^"]\+\).zip.asc".*/\1/p' | sort --version-sort | tail -1)
STABLEVERSION="nextcloud-$NCVERSION"
```

## First look
![alt tag](https://github.com/nextcloud/nextcloud.com/blob/master/assets/img/features/VMwelcome.png)

## The usual tags
**Downloads from Github (not the main downloads location):**
<br>
![Downloads](https://img.shields.io/github/downloads/nextcloud/vm/total.svg)
<br>
**Downloads from main server:**
<br>
~100 per day since 2016
<br>
**Build Status:**
<br>
[![Build Status](https://travis-ci.org/nextcloud/vm.svg?branch=master)](https://travis-ci.org/nextcloud/vm)
<br>
**Stability Status:**
<br>
![Stability Status](https://img.shields.io/badge/stability-stable-brightgreen.svg)

## Current [maintainers](https://github.com/nextcloud/vm/graphs/contributors)
* [Daniel Hanson](https://github.com/enoch85) @ [T&M Hansson IT AB](https://www.hanssonit.se)
* You? :)

## Special thanks to
* [Ezra Holm](https://github.com/ezraholm50) @ [Tech and Me](https://www.techandme.se)
* [Luis Guzman](https://github.com/Ark74) @ [SwITNet](https://switnet.net)
* [Stefan Heitmüller](https://github.com/morph027) @ [morph027's Blog](https://morph027.gitlab.io/)
* [Lorenzo Faleschini](https://github.com/penzoiders)
* [Georg Großmann](https://github.com/ggeorgg)

[Nextcloud Server]: https://bit.ly/2CHIUkA
[app store]: https://bit.ly/2HUy4v9
[\*nix]: https://bit.ly/2UaCC7b
[A+ security-rated]: https://bit.ly/2mvlyJ3
[Collabora Online]: https://bit.ly/2WjVVZ8
[ONLYOFFICE]: https://bit.ly/2FA0TKj
