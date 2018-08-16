
# PostGIS-uberspace7

This is a step-by-step guid to install postgresql + postgis on CentOS 7 without root access

Anleitung Postgres and Postgis


## Get readline. The following helps me alot https://unix.stackexchange.com/questions/61283/yum-install-in-user-home-for-non-admins

`curl -o readline-devel-6.2-10.el7.x86_64.rpm http://mirror.centos.org/centos/7/os/x86_64/Packages/readline-devel-6.2-10.el7.x86_64.rpm`

`curl -o readline-6.2-10.el7.x86_64.rpm http://mirror.centos.org/centos/7/os/x86_64/Packages/readline-6.2-10.el7.x86_64.rpm`

`rpm2cpio readline-devel-6.2-10.el7.x86_64.rpm > readline-devel.cpio`

`rpm2cpio readline-6.2-10.el7.x86_64.rpm > readline.cpio`

`cpio -idv < readline-devel.cpio`

`cpio -idv < readline.cpio`

## Get Postgres

`curl -o postgresql-9.6.10.tar.gz https://ftp.postgresql.org/pub/source/v9.6.10/postgresql-9.6.10.tar.gz`

`tar -zxvf postgresql-9.6.10.tar.gz`

`cd postgresql-9.6.10`

`./configure --prefix=$HOME --with-includes=$HOME/usr/include --with-libraries=$HOME/usr/lib64`

`make`

`make install`


### Edit postgresql config

`nano $HOME/share/postgresql/postgresql.conf.sample`

Uncomment PORT and set one

### Set Datadir and add bin to path

`export PGDATA=$HOME/pgdata`

`export PATH=$HOME/bin:$PATH`

### Add pathes to bash profile 

`nano ~/.bashrc`

Add `export PGDATA=$HOME/pgdata`

Add `export PATH=$HOME/bin:$PATH`


## Get geos

`curl -o geos-3.6.3.tar.bz2 http://download.osgeo.org/geos/geos-3.6.3.tar.bz2`

`tar -jxvf geos-3.6.3.tar.bz2`

`cd geos-3.6.3`

`./configure --prefix=$HOME`

`make install`



## Get proj4

`curl -o proj-4.9.3RC3.tar.gz http://download.osgeo.org/proj/proj-4.9.3RC3.tar.gz`

`tar -zxvf proj-4.9.3RC3.tar.gz`

`cd proj-4.9.3`

`./configure --prefix=$HOME/proj`

`make install`



## Get gdal

`curl -o gdal-2.3.1.tar.gz http://download.osgeo.org/gdal/CURRENT/gdal-2.3.1.tar.gz`

`tar -zxvf gdal-2.3.1.tar.gz`

`cd gdal-2.3.1`

`./configure --prefix=$HOME`

`make`

`make install`



## Get Postgis

`curl -o postgis-2.4.4.tar.gz http://download.osgeo.org/postgis/source/postgis-2.4.4.tar.gz`

`tar -zxvf postgis-2.4.4.tar.gz`

`cd postgis-2.4.4`

`./configure --prefix=$HOME --with-geosconfig=$HOME/bin/geos-config --with-projdir=$HOME/ --with-pgconfig=$HOME/bin/pg_config --with-gdalconfig=$HOME/bin/gdal-config`

`make && make install DESTDIR=$HOME/postgis REGRESS=1`



## Setup

`nano $HOME/share/postgresql/postgresql.conf`

Hier wird der Port geändert

pg_ctl start | stop | status

psql -p <PORTNUMMER>

//Im SSH Client kann ein Tunnel gesetzt werden
