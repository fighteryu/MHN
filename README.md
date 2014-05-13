Modern Honey Network
==========================

Multi-snort and honeypot sensor management, uses a network of VMs, small footprint SNORT installations, stealthy dionaeas, and a centralized server for management.

### HONEYPOT

Deployed sensors with intrusion detection software installed: SNORT, Conpot, and Dionaea. 

### MANAGEMENT SERVER

Flask application that exposes an HTTP API that honeypots can use to:
- Download a deploy script
- Connect and register
- Download snort rules
- Send intrusion detection logs

It also allows systems administrators to:
- View a list of new attacks
- Manage snort rules: enable, disable, download


### INSTALLING SERVER (tested Ubuntu 12.0.4.3 x86_64)
    
    $ cd /opt/
    $ git clone https://github.com/threatstream/MHN.git
    $ cd MHN/scripts/
    $ sudo ./install_hpfeeds.sh
    $ sudo ./install_mnemosyne.sh


Run the following script to complete the installation.  While this script runs, you will
be prompted for some configuration options.  See below for how this looks.

    $ sudo ./install_mhnserver.sh


### Configuration:
    
    ===========================================================
    MHN Configuration
    ===========================================================
    Do you wish to run in Debug mode?: y/n n
    Superuser email: YOUR_EMAIL@YOURSITE.COM
    Superuser password: 
    Server base url ["http://1.2.3.4:8080"]: 
    Mail server address ["localhost"]: 
    Mail server port [25]: 
    Use TLS for email?: y/n n
    Use SSL for email?: y/n n
    Mail server username [""]: 
    Mail server password [""]: 
    Mail default sender [""]: 
    Path for log file ["mhn.log"]: 


MHN Can be run with an optional component called honeymap.  This allows realtime visualization of the 
honeypot data as it flows back to the MHN server.

    $ sudo ./install_honeymap.sh  #optional

### Running

If the installation scripts ran successfully you should have a number of services running on your
MHN server.  See below for checking these.  Note: if you did not install honeymap, you will not see
honeymap or geoloc in the list below.


    user@precise64:/opt/MHN/scripts$ sudo /etc/init.d/nginx status
     * nginx is running
    user@precise64:/opt/MHN/scripts$ sudo /etc/init.d/supervisor status
     is running
    user@precise64:/opt/MHN/scripts$ sudo supervisorctl status
    geoloc                           RUNNING    pid 31443, uptime 0:00:12
    honeymap                         RUNNING    pid 30826, uptime 0:08:54
    hpfeeds-broker                   RUNNING    pid 10089, uptime 0:36:42
    mhn-celery-beat                  RUNNING    pid 29909, uptime 0:18:41
    mhn-celery-worker                RUNNING    pid 29910, uptime 0:18:41
    mhn-uwsgi                        RUNNING    pid 29911, uptime 0:18:41
    mnemosyne                        RUNNING    pid 28173, uptime 0:30:08



## LICENSE

Modern Honeypot Network

Copyright (C) 2014 - ThreatStream

This program free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public
License along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA
