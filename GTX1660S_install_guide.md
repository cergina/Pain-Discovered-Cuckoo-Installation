# Cuckoo Sandbox - ON - GTX 1660 Super

##### I recommend reading all parts of this repository before intsallation attempt. Will save lots of time.

There is a reason why I'm not going instantly to Ubuntu 18, because it doesn't freeze, but there are some funky stripes all over the place and it doesn't let me even attempt installation.

Start with pure Ubuntu 16.04.7 LTS, LIVE USB installation
Wait for the popup to upgrade distribution to appear, or better. Use these commands.
    
    sudo apt install update-manager-core
    sudo do-release-upgrade
    # here, check for request to press ENTER, twice i think

Installation of 18.04.5 LTS should be done now

    $ sudo apt update & sudo apt upgrade
    # this was not possible in Ubuntu 16 as no additional drivers are there
    # software update center => additional drivers => choose (proprietary, tested) !
    # Restart
    # voila! 2560x1440 or similiar high res is set

### Create user named 'cuckoo' with password and login as him. 
##### Don't create user 'cuckoo' without password, it will cause issues, prevention of privilege elevation from VM is dealth with differently. Also never use sudo when running cuckoo rooter, but use the "--sudo --group cuckoo". 

### 1st. part

    
    $ sudo apt update & sudo apt upgrade

    # Python stuff
    $ sudo apt-get install python python-pip python-dev libffi-dev libssl-dev
    $ sudo apt-get install python-virtualenv python-setuptools
    $ sudo apt-get install libjpeg-dev zlib1g-dev swig

    $ sudo apt-get install mongodb
    $ sudo apt-get install postgresql libpq-dev

    # Virtualization SW
    $ sudo add-apt-repository multiverse
    $ sudo apt-get update
    $ sudo apt install virtualbox
    
    # LETS SAVE TIME
    # Watch out where you are, remember it
    $ wget https://cuckoo.sh/win7ultimate.iso
    
    # TCPDUMP
    $ sudo apt-get install tcpdump apparmor-utils
    $ sudo aa-disable /usr/sbin/tcpdump
    
    # Python Next Stuff
    $ sudo apt-get -y install python virtualenv python-pip python-dev build-essential
    $ sudo groupadd pcap
    $ sudo usermod -a -G pcap cuckoo
    
    $ sudo chgrp pcap /usr/sbin/tcpdump
    $ sudo setcap cap_net_raw,cap_net_admin=eip /usr/sbin/tcpdump

    $ sudo pip install m2crypto
    $ sudo usermod -a -G vboxusers cuckoo
    
    $ sudo mkdir /mnt/win7
    $ sudo chown -R cuckoo:cuckoo /mnt/win7/
    $ ls -alt /mnt/
    # I told you to remember where you put it :-)
    $ sudo mount -o ro,loop win7ultimate.iso /mnt/win7
    
    $ sudo apt-get -y install build-essential libssl-dev libffi-dev python-dev genisoimage
    
Download this file as RAW, save under the original name.
https://gist.github.com/jstrosch/de20131dda2aac5cd1116dd44b8f2474 

    $ chmod +x ./cuckoo-setup-virtualenv.sh
    $ sudo -u cuckoo ./cuckoo-setup-virtualenv.sh
    
    # you most likely need to enter also this
    $ source ~/.bashrc
    
    $ mkvirtualenv -p python2.7 cuckoo-test

### Important
Now when you see (cuckoo-test) you are in virtual environment, and every line that  will look like this
    
    (cuckoo-test) $ #example_command_to_execute_without_#_at_the_start
    
should be entered into this way

    $ workon cuckoo-test

### 2nd part

    (cuckoo-test) $ pip install -U pip setuptools
    (cuckoo-test) $ pip install -U cuckoo
    (cuckoo-test) $ pip install -U vmcloak

    (cuckoo-test) $ vmcloak-vboxnet0
    (cuckoo-test) $ vmcloak init --verbose --win7x64 win7x64base --cpus 2 --ramsize 2048
    (cuckoo-test) $ vmcloak clone win7x64base win7x64cuckoo
    (cuckoo-test) $ vmcloak install win7x64cuckoo winrar zer0m0n chrome flash python27 wallpaper
    (cuckoo-test) $ vmcloak snapshot --count 3 win7x64cuckoo 192.168.56.101
    (cuckoo-test) $ cuckoo init
    (cuckoo-test) $ cd ~/.cuckoo/conf
    (cuckoo-test) $ cuckoo community
    
    (cuckoo-test) $ while read -r vm ip; do cuckoo machine --add $vm $ip; done < <(vmcloak list vms)
    # Continue and open another config file
    (cuckoo-test) $ vim ~/.cuckoo/conf/virtualbox.conf 

* GIVE YOURSELF SOME REST

Changes in **virtualbox.conf**, each line is in **{old line} => {new line}**, 
**...** means lines of not interesting code
```
...
    { mode = headless } => { mode = gui }
...
```
**Remove also everything under [cuckoo1]**

    # go see results of this command, look for interface name that has broadcast
    ip a

**Mine is called enp24s0, so if you see it in some network configurations further, use yours**

    $ sudo sysctl -w net.ipv4.conf.vboxnet0.forwarding=1
    $ sudo sysctl -w net.ipv4.conf.enp24s0.forwarding=1

    # Continue and open another config file
    (cuckoo-test) $ vim ~/.cuckoo/conf/routing.conf

Changes in **routing.conf**, each line is in **{old line} => {new line}**, 
**...** means lines of not interesting code. Every conf file is in 
```
...
    { route = none} => { route = internet }
    { internet = none } => { internet = enp24s0 }
...
```

    # Continue and open another config file
    (cuckoo-test) $ vim ~/.cuckoo/conf/reporting.conf
    
Changes in **reporting.conf**, each line is in **{old line} => {new line}**, 
**...** means lines of not interesting code. Every conf file is in 
```
...
    # find  [mongodb] tag
    { enabled = no } => { enabled = yes }
...
```

### HOW TO START CUCKOO (EVEN AFTER REBOOT OF SYSTEM)
Give yourself a few more  terminals [Ctrl + Alt + T] (3 should be enough)

    (cuckoo-test) $ vmcloak-vboxnet0
    (cuckoo-test) $ cuckoo rooter --sudo --group cuckoo
    (cuckoo-test) $ cuckoo
    (cuckoo-test) $ cuckoo web --host 127.0.0.1 --port 8080

### virus samples websites (please dont run them in your real env...):
https://zeltser.com/malware-sample-sources/

**Open lets say firefox/chrome, type in the URL : "localhost:8080" and Enjoy, i guess.**

I'd like to thank the creator of https://dillinger.io/ for the ability to live edit markdown. :-)

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [cuckoo_od]: <https://cuckoo.readthedocs.io/en/latest/installation/>
   [git_readme]: <https://github.com/cergina/Pain-Discovered-Cuckoo-Installation/blob/main/README.md>
   