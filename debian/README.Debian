arma2oa-server for Debian
=========================

## Installation
You will, of course, need all the non-redistributable content of ArmA2:OA to be
able to use this package.

I've replaced BIS's tolower.c with a simple one-line bash script that will be run
against the assets directory (i.e., where normally copy all the game directory
contents to) as part of the post-installation steps. Either upload all the asset
files there before installing this package, or, more likely, directory, so put
all the game assets in there before installing this package, run
"dpkg-reconfigure arma2oa-server" after installation. Repeat the latter upon
addition of new addons, etc. whose names need to be downcased.

## Configuration

### Server Config Files
/etc/arma2oa-server.d/2302.cfg will be used by the watchdog to manage the
server with default settings. If you need to run multiple servers, make altered
copies of that file in that directory, ending in ".cfg". Each of these files
should be named with respect to what port the server instance using them will
be running on. If you feel the need to name them more descriptively, I suggest
using symlinks or comments at the top of each to document their contents.

Edit /etc/default/arma2oa-server if you want to add args to every server
instance or change where the assets directory is located.

### Monit
I've elected to take advantage of Monit to act as a watchdog for the server
processes. It has a lot of nice features that, with some reading of the
manpage, should allow administrators a good amount of control over the server
instances, including when and how to restart each process.

Unfortunately, out of the box, monit as distributed in the debian package needs
a few tweaks before it's really usable. That said, if you install this package
and get the monit daemon running, your default server instance running on port
2302 should work without problem. You can edit the 2302.cfg file and manually
restart the server using "cat /var/run/arma2oa-server/2302.pid | xargs kill".

That said, I suggest making the following changes after installation:
* Edit /etc/monit/monitrc
    * Change the line containing "set daemon 120" to something shorter, like 10.
      This will cut down on the time it takes for your crashed server to come
      back up.
    * Uncomment the lines containing:
        set httpd port 2812 and
           use address localhost  # only accept connection from localhost
           allow localhost        # allow localhost to connect to the server and
    * sudo invoke-rc.d monit restart
Now, you'll be able to use the monit command to control the server processes. A brief list of examples (run as root):
* monit status
* monit start arma2oa-server.2302
* monit stop arma2oa-server.2302

Caveat: Watch out for /etc/monit/conf.d/*.dpkg-old or -new files. Merge and
delete them, or else monit complains about duplicate definitions

"man monit" for further help.

### Adding Instances
If you want to add more server instances, do the following:
* copy /etc/arma2oa-server/2302.cfg to the new port number + .cfg; edit it appropriately.
* edit /etc/monit/conf.d/arma2oa-server and add a new stanza with all instances of 2302 changed appropriately.
* run "monit reload"
You'll then be able to start/stop the new instance under its new name. You may also add args particular to specific instances in each "start" line, if adding them in /etc/default/arma2oa-server's DAEMON_OPTS isn't suitable.

---

 -- Eric Litak <elitak@gmail.com>  Fri, 27 Jul 2012 09:00:00 +0200
