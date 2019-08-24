MyVesta Control Panel
==================================================

* MyVesta is a fork of VestaCP
* Focused on security and stability
* Therefore, only Debian is supported - keeping focus on ONE eco-system - not wasting energy on compatibility with other Linux distributions
* It will always be synchronized with official VestaCP commits
* VestaCP commercial plugins will be only available for purchase on official vestacp.com website - we will NOT take their earnings, since we are not making this fork for monetary reasons. Instead, we are doing this with open source in mind - to enhance security and to build new features, without being interlocked with official VestaCP release cycles, and without affecting or heavily diverting from the VestaCP's planned development milestones
* With previous in mind, all features that are added in this fork, will be offered to official VestaCP through pull-request mechanisms

Features
==================================================

+ Support for Debian 10 (previous releases are also supported)

+ You can totally "lock" VestaCP so it can be accessed only via https://serverhost:8083/?MY-SECRET-URL
    + During installation you will be asked to choose secret URL for your hosting panel
    + Literally no PHP scripts will be alive (won't be able to get executed), unless you access the URL with that parameter. Thus, when it happens that, let's say, some zero-day exploit pops up - hacker will not be able to access it without knowing your secret URL. PHP scripts from VestaCP will be simply dead - no one will be able to interact with your panel unless he has the secret URL.
    + You can see for yourself how mechanism was built by looking at:
      + https://github.com/myvesta/vesta/blob/master/src/deb/for-download/php/php.ini#L496
      + https://github.com/myvesta/vesta/blob/master/web/inc/secure_login.php
    + If you didn't set secret URL during installation, you can do it anytime, just execute in SSH:
    + `echo "<?php \$login_url='MY-SECRET-URL';" > /usr/local/vesta/web/inc/login_url.php`

+ We disabled dangerous PHP functions in php.ini, so even if, for example, customer's CMS gets compromised, hacker will not be able to execute "shell" from PHP.

+ Apache is fully switched to mpm_event mode, while PHP is running in PHP-FPM, which is the most stable PHP-stack solution
    + OPCache is turned on by default

+ Support for multi-PHP versions - https://forum.vestacp.com/viewtopic.php?t=17129

+ Auto-generating LetsEncrypt SSL for server hostname (signed SSL for Vesta 8083 port, for dovecot (IMAP & POP3) and for Exim (SMTP))

+ You can change Vesta port during installation or later using one command line: **v-change-vesta-port [number]**

+ You can compile Vesta binaries by yourself - https://github.com/myvesta/vesta/blob/master/src/deb/vesta_compile.sh
    + You can even create your own APT repositorium in a minute
    + We are using latest nginx version for vesta-nginx package
    + With your own APT infrastructure you can take security of Vesta-installer infrastructure in your own hands. You will have full control of your Vesta code (this way you can rest assured that there's 0% chance that you'll install malicious packages from repositories that may get hacked)

How to install
----------------------------
Download the installation script:
```bash
curl -O http://c.vesta.hostingpanel.dev/vst-install-debian.sh
```
Then run it:
```bash
bash vst-install-debian.sh
```

About VestaCP
==================================================

* Vesta is an open source hosting control panel.
* Vesta has a clean and focused interface without the clutter.
* Vesta has the latest of very innovative technologies.

Special thanks to vestacp.com and Serghey Rodin for open-source VestaCP project

License
----------------------------
Vesta is licensed under  [GPL v3 ](https://github.com/serghey-rodin/vesta/blob/master/LICENSE) license

