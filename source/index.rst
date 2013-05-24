.. videocache documentation master file, created by
   sphinx-quickstart on Thu May 23 19:33:39 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. toctree::
   :maxdepth: 2


.. _what-is-videocache:

===================
What is Videocache?
===================

Videocache_ is a Squid_ URL rewriter plugin written in Python_ for bandwidth optimization while
browsing famous video portals like Youtube_, Dailymotion_, Metacafe_ etc. It helps you save bandwidth
when a particular video is requested more than once from the same network/machine.

Squid can not cache the videos served dynamically. Videocache fits into squid to help it cache the
videos as well. The cached videos are stored on your proxy server's local storage or on a storage
server in your network. These cached videos can be served to your clients at a very fast speed saving
you significant upstream bandwidth.

**NOTE:** If you are new to Squid or you are willing to explore Squid in details, please check
my book `Squid Proxy Server 3.1 : Beginner's Guide`_.

.. _Videocache: http://cachevideos.com/
.. _Squid: http://www.squid-cache.org/
.. _Python: http://www.python.org/
.. _Youtube: http://www.youtube.com/
.. _Dailymotion: http://www.dailymotion.com/
.. _Metacafe: http://www.metacafe.com/
.. _`Squid Proxy Server 3.1 : Beginner's Guide`: http://tinyurl.com/squidbook


.. _supported-websites:

==================
Supported Websites
==================

Below is an exhaustive list of websites partially or wholly supported by Videocache.

These websites doesn’t normally contain any pornographic content.

#. YouTube - www.youtube.com
#. AOL - www.aol.com
#. Bing - www.bing.com/videos/
#. Blip - www.blip.tv
#. Break - www.break.com
#. CNN - www.cnn.com/video/
#. Dailymotion - www.dailymotion.com
#. Facebook - www.facebook.com [#f1]_
#. Metacafe - www.metacafe.com
#. MySpace - www.myspace.com/video/
#. Vimeo - www.vimeo.com
#. Weather - www.weather.com
#. Wrzuta - www.wrzuta.pl [#f2]_
#. Youku - www.youku.com

Videocache also supports caching of videos from pornographic websites mentioned in the list below.
Visit these sites only if you are above 18 years (or permitted age in your country).

#. ExtremeTube - www.extremetube.com
#. HardSexTube - www.hardsextube.com
#. KeezMovies - www.keezmovies.com
#. PornHub - www.pornhub.com
#. RedTube - www.redtube.com
#. SlutLoad - www.slutload.com
#. SpankWire - www.spankwire.com
#. Tube8 - www.tube8.com
#. Xhamster - www.xhamster.com
#. XTube - www.xtube.com
#. XVideos - www.xvideos.com
#. YouPorn - www.youporn.com


.. _software-dependencies:

=====================
Software Dependencies
=====================

Videocache requires following software to run on your system. Though most of these software are
already included in most of the standard Linux distributions, you need to make sure that these
are present. If anything is missing, Videocache installer will point it out during installation.
Also, some software are required during installation only and not during runtime. Below is a list.

#. Installation Dependencies

   * `bash shell`_
   * wget_
   * tar_
   * `gcc (c compiler)`_

#. Runtime Dependencies (Software)

   * `Python (2.5 or later) but not 3.x`_
   * `Squid Proxy Server (2.6.STABLE21 or later)`_
   * `MySQL (5.x)`_
   * `Apache Web Server`_

#. Runtime Dependencies (Python Modules) [#f3]_

   * setuptools
   * iniparse
   * netifaces
   * ctypes
   * multiprocessing

.. _bash shell: http://www.gnu.org/software/bash/
.. _wget: http://www.gnu.org/software/wget/
.. _tar: http://www.gnu.org/software/tar/
.. _gcc (c compiler): http://gcc.gnu.org/
.. _Python (2.5 or later) but not 3.x: http://www.python.org/
.. _Squid Proxy Server (2.6.STABLE21 or later): http://www.squid-cache.org/
.. _MySQL (5.x): http://dev.mysql.com/downloads/mysql/
.. _Apache Web Server: http://httpd.apache.org/


.. _supported-platforms-and-operating-systems:

========================================
Supported Platfoms and Operating Systems
========================================

Videocache works on both 32 and 64bit platforms. It will run on most Linux/Unix based operating systems where
the required software packages mentioned above are available. Below is a list of officially supported operating systems.
It may also work on other Linux/Unix distributions provided the required software packages are present.

* Ubuntu
* Debian
* LinuxMint
* Fedora
* CentOS
* Red Hat Enterprise Linux
* OpenSuSE
* Mandriva
* Gentoo
* FreeBSD/NetBSD
* Slackware


.. _preparing-system-for-setup:

==========================
Preparing System for Setup
==========================

Before you can install Videocache on your server, you need to install and setup the required software mentioned in
:ref:`software-dependencies`.


.. _installing-required-packages:

Installing Required Packages
----------------------------

Videocache requires ``wget``, ``tar``, ``gcc``, Python development libraries during Videocache installation. We can install
these packages on Ubuntu, Debian, LinuxMint using ``apt-get`` as shown below::

     [user@white-magnet ~]# apt-get install python-dev wget tar gcc grep

For Fedora, CentOS, RHEL the packages can be installed using ``yum`` as::

     [root@white-magnet ~]# yum install python-devel wget tar gcc


.. _installing-python:

Installing Python
-----------------

There is a very high probability that you already have Python installed on your system. You can confirm the same
by using the following command::

    [root@white-magnet ~]# python
    Python 2.7.3 (default, Aug  1 2012, 05:16:07)
    [GCC 4.6.3] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

If Python is not present on your system, you can use Yum to install it on Fedora, CentOS, RHEL as shown below::

    [root@white-magnet ~]# yum install python

Or you can use apt-get to install it on Ubuntu, Debian, LinuxMint like::

    [root@white-magnet ~]# apt-get install python


.. _upgrading-python:

Upgrading Python
----------------

If you have Python installed but it's older than 2.5, then you will need to upgrade Python. Download latest version
(2.7.5) from `Python website`_ and extract. Then run the following commands in extracted archive::

    [user@white-magnet python-2.7.5]# ./compile
    [user@white-magnet python-2.7.5]# make
    [user@white-magnet python-2.7.5]# sudo make install

After that you will need to remove the `/usr/bin/python` symlink using the command::

    [user@white-magnet python-2.7.5]# sudo rm -f /usr/bin/python

And then add a symlink to the newly installed Python::

    [user@white-magnet python-2.7.5]# sudo ln -s /usr/local/bin/python2.7 /usr/bin/python

After adding the symlink, you can test your Python vesrion as shown below::

    [user@white-magnet ~]# python
    Python 2.7.5 (default, May 22 2013, 05:16:07)
    [GCC 4.6.3] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

.. _`Python website`: http://www.python.org/download/releases/


.. _mysql-setup:

MySQL Setup
----------------

Videocache requires MySQL to store information about cached videos, maintain a queue of videos to be cached in background
and other activity. We need to install and setup MySQL before we can proceed with Videocache installation.

If you are Ubuntu, Debian, LinuxMint or on a Debian derivative OS, you can run the following command to install MySQL::

    [user@white-magnet ~]# apt-get install mysql-server mysql-client libmysqlclient-dev

If you are on Fedora, RHEL, CentOS or any other distro which uses Yum as package manager, you can use the following command
to install MySQL::

    [root@white-magnet ~]# yum install mysql mysql-server mysql-devel

Once we are done with installing MySQL, we to setup a database for Videocache. We need to use database name, user name and
password for this. You can set them as per your convenience. Here are we using,

* Database Name : ``vcdb``
* Database Username : ``vc_dbuser``
* Database Password : ``password``

Now, we need to use the above details to setup database for Videocache as shown below::

    [root@white-magnet ~]# mysql -u root -p
    Enter password:

    mysql> create database vcdb;

    mysql> grant all on vcdb.* to 'vc_dbuser'@'localhost' identified by 'password';

    mysql> flush privileges;

Remeber the username, password and database name you used above as it'll be required when you run install script ``install.sh``.

.. _apache-web-server-setup:

Apache Web Server Setup
-----------------------

Videocache require Apache Web Server to serve cached videos. If Apache is not installed already on our server, we can install
apache on Ubuntu, Debian, LinuxMint using the command::

    [user@white-magnet ~]# apt-get install apache2

On Fedora, CentOS, RHEL we can use yum to install Apache (``httpd``) as below::

    [root@white-magnet ~]# yum install httpd

If we are planning to run Squid in ``transparent`` or ``tproxy`` mode, we must configure Apache to listen on port other than ``80``.
We can use any other free port like ``81`` or ``8181``. Now, we need to locate Apache configuration file to make the appropriate changes.
The Apache config file on Ubuntu, Debian, LinuxMint is located at ``/etc/apache2/ports.conf`` while on Fedora, CentOS, RHEL it's located
at ``/etc/httpd/conf/httpd.conf``.

Once we have the config file open, look for the lines shown below and change the port to ``81``::

    NameVirtualHost *:81
    Listen 81

Now save the file.


.. _installing-squid:

Installing Squid
----------------

First you need to decide whether you want to go for Squid 2.x or Squid 3.x. We always recommend using Squid 3.x for
best performance. Once you have decided, you can use your distro's package manager to install the required version.
You can also refer to the following manuals for installing and running Squid.

* `Installing Squid from Binary Packages Using Package Manger`_
* `How to Configure Squid Proxy Server`_
* `How to Configure Hierarchy of Squid Proxy Servers`_
* `Squid Proxy Server 3.1 : Beginner's Guide`_

.. _`Installing Squid from Binary Packages Using Package Manger`: http://wiki.squid-cache.org/SquidFaq/BinaryPackages
.. _`How to Configure Squid Proxy Server`: http://gofedora.com/how-to-configure-squid-proxy-server/
.. _`How to Configure Hierarchy of Squid Proxy Servers`: http://gofedora.com/how-to-configure-hierarchicy-proxy-servers-squid/
.. _`Squid Proxy Server 3.1 : Beginner's Guide`: http://tinyurl.com/squidbook


.. _installing-upgrading-videocache:

==================================
Installing or Upgrading Videocache
==================================

Once we are done with the steps in :ref:`preparing-system-for-setup`, we are all set to install or upgrade Videocache.
Installation and upgrade process for Videocache are same. You need to run the same installer script to install or upgrade.

**NOTE:** If you are upgrading your Videocache, please don't forget to take a backup of your existing configuration file
located at */etc/videocache.conf*.

Below are the steps required to install or upgrade Videocache. **You must be logged in as root or super user to perform this action**.

#. Untar the Videocache software bundle you received in your email::

    [root@white-magnet ~]$ tar -xvzf videocache-2.3.tar.gz

#. Navigate to the directory videocache-2.3::

    [root@white-magnet ~]$ cd videocache-2.3

#. Run the installer script (install.sh) to install or upgrade Videocache::

    [root@white-magnet videocache-2.3]$ bash install.sh
    Checking root access..................................................Granted


    ---------------------------Dependency Check---------------------------
    Checking which........................................................Installed
    Checking python.......................................................Installed
    Checking wget.........................................................Installed
    Checking tar..........................................................Installed
    Checking gcc..........................................................Installed


    -----------------Python Modules And Development Files-----------------
    Checking setuptools...................................................Installed
    Checking iniparse.....................................................Installed
    Checking Python.h.....................................................Installed
    Checking netifaces....................................................Installed
    Checking ctypes.......................................................Installed
    Checking multiprocessing..............................................Installed


    ------------------------Database Configuration------------------------
    MySQL database is used for hashing cached files for efficient cleanup


    ------------------------MySQL Dependency Check------------------------
    Checking mysql........................................................Installed
    Checking mysql_config.................................................Installed
    Checking MySQLdb......................................................Installed

    Enter hostname ( default: localhost ):
    Selected hostname for database........................................localhost
    Enter username ( default: vc_dbuser ):
    Selected username for database........................................vc_dbuser
    Enter password ( default: password ):
    Selected password for database........................................password
    Enter database name ( default: vcdb ):
    Selected database name................................................vcdb
    Checking MySQL access.................................................Working


    --------------------------------Squid---------------------------------
    Checking squid........................................................Installed

    Full path to Squid access.log file (default: /var/log/squid3/access.log):
    Selected Squid access.log file......................................../var/log/squid3/access.log

    User who run Squid Proxy Server daemon (default: proxy):
    Selected user who runs Squid daemon...................................proxy


    -------------------------Apache Configuration-------------------------
    Do you want to skip Apache configuration? (y/n): n
    Checking Apache.......................................................Installed

    Full path to Apache conf.d or extra directory (default: /etc/apache2/conf.d/):
    Selected Apache conf.d or extra directory............................./etc/apache2/conf.d/


    -----------------------------Client Email-----------------------------
    Enter the email address using which you purchased Videocache: a@b.me
    Selected email address................................................a@b.me


    -----------------------Cache Host (Web Server)------------------------
    IP address with optional port. It will be used as a web server to serve
    cached videos. Examples: 192.168.1.14 or 192.168.1.14:81

    Enter IP_Address[:port] for cache_host option (available: 192.168.0.100 ): 192.168.0.100
    Selected cache_host...................................................192.168.0.100


    --------------------------Squid Proxy Server--------------------------
    IP_Address:Port combination for Squid proxy running on this machine.
    Examples: 127.0.0.1:3128 or 192.168.1.1:8080

    Enter IP_Address:Port for Squid on this machine (example: 127.0.0.1:3128): 127.0.0.1:3128
    Selected proxy server.................................................127.0.0.1:3128


    ------------------------Collected Information-------------------------
    We will be using the following information to install videocache.
    Squid access.log....................................................../var/log/squid3/access.log
    Squid user............................................................proxy
    Apache conf.d........................................................./etc/apache2/conf.d/
    Email address.........................................................a@b.me
    Cache Host............................................................192.168.0.100
    Squid proxy...........................................................127.0.0.1:3128


    --------------------------Install Videocache--------------------------
    Installing Videocache.................................................Installed

    Command used: python setup.py --squid-user proxy --client-email a@b.me --cache-host 192.168.0.100 --this-proxy 127.0.0.1:3128 --squid-access-log /var/log/squid3/access.log --apache-conf-dir /etc/apache2/conf.d/ --db-hostname localhost --db-username videocache --db-password videocache --db-database videocache install 2>&1


    ------------------------Install init.d Script-------------------------
    Trying to set default run levels for vc-scheduler.....................Done

    --------------------Post Installation Instructions--------------------
    Setup has completed successfully. A file instructions.txt has been created
    in the bundle which you should follow to complete the installation process.

    FOLLOW EACH STEP CAREFULLY.

    ----------------------------------Step 1-----------------------------------------
    Open the Videocache configuration file located at /etc/videocache.conf and modify
    any options you want. Once you are done, save the file.

    ----------------------------------Step 2-----------------------------------------
    Run vc-update command to update your installation in accordance with new options.
    [root@white-magnet ~]# vc-update

    ----------------------------------Step 3-----------------------------------------
    Restart Apache web server on your machine by using the following command
    [root@white-magnet ~]# apachectl -k restart

    ----------------------------------Step 4-----------------------------------------
    Depending on the version of your Squid, open vc_squid_2.conf or vc_squid_3.conf
    in your Videocache bundle. Copy all the lines and paste them at the top of your
    Squid configuration file squid.conf.

    Also add the following lines at the top of your Squid config file squid.conf.
    #-----------------CUT FROM HERE-------------------
    access_log /var/log/squid3/access.log
    acl this_machine src 127.0.0.1 192.168.0.100
    http_access allow this_machine
    #-----------------CUT TILL HERE-------------------

    ----------------------------------Step 5-----------------------------------------
    Restart videocache scheduler vc-scheduler using the following command.
    [root@white-magnet ~]# vc-scheduler -s restart

    ----------------------------------Step 6-----------------------------------------
    Restart Squid proxy server daemon using the following command.
    [root@white-magnet ~]# /etc/init.d/squid restart

    ----------------------------------Step 7-----------------------------------------
    Go the videocache log directory /var/log/videocache/ and check various log files
    to have a look at videocache activity.

    Check Manual.pdf file for detailed configurations of squid, apache and videocache.
    In case of any bugs or problems, visit http://cachevideos.com/ and contact us.
    [root@white-magnet videocache-2.3]$


.. rubric:: Footnotes

.. [#f1] Does not support caching of Videos served via HTTPS.
.. [#f2] Supports caching of Audio and Video both.
.. [#f3] These python modules will be installed automatically by installer if not present.

