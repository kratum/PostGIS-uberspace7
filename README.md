# PostGIS-uberspace7
This is a step-by-step guid to install postgresql + postgis on CentOS 7 without root access

Anleitung Postgres and Postgis

`cd bin`

`git clone https://github.com/postgres/postgres`

Get readline. The following helps me alot https://unix.stackexchange.com/questions/61283/yum-install-in-user-home-for-non-admins
`curl -o readline-devel-6.2-10.el7.x86_64.rpm http://mirror.centos.org/centos/7/os/x86_64/Packages/readline-devel-6.2-10.el7.x86_64.rpm`

`curl -o readline-6.2-10.el7.x86_64.rpm http://mirror.centos.org/centos/7/os/x86_64/Packages/readline-6.2-10.el7.x86_64.rpm`

`rpm2cpio readline-devel-6.2-10.el7.x86_64.rpm > readline-devel.cpio`

`rpm2cpio readline-6.2-10.el7.x86_64.rpm > readline.cpio`

`cpio -idv < readline-devel.cpio`

`cpio -idv < readline.cpio`

`cd postgres`

`./configure --prefix=$HOME/postgresql --with-includes=$HOME/bin/usr/include --with-libraries=$HOME/bin/usr/lib64`

`make`

`make install`

`nano $HOME/postgresql/share/postgresql.conf`
Hier wird der Port geändert

pg_ctl start | stop | status

psql -p <PORTNUMMER>

//Im SSH Client kann ein Tunnel gesetzt werden



Get geos

`curl -o geos-3.6.3.tar.bz2 http://download.osgeo.org/geos/geos-3.6.3.tar.bz2`

`tar -jxvf geos-3.6.3.tar.bz2`

`cd geos-3.6.3`

`./configure --prefix=$HOME/geos`

`make install`



Get proj4
`curl -o proj-4.9.3RC3.tar.gz http://download.osgeo.org/proj/proj-4.9.3RC3.tar.gz`

`tar -zxvf proj-4.9.3RC3.tar.gz`

`cd proj-4.9.3`

`./configure --prefix=$HOME/proj`

`make install`


Get Postgis

`curl -o postgis-2.4.4.tar.gz http://download.osgeo.org/postgis/source/postgis-2.4.4.tar.gz`

`tar -zxvf postgis-2.4.4.tar.gz`

`cd postgis-2.4.4`

`./configure --with-geosconfig=$HOME/geos/bin/geos-config --with-projdir=$HOME/proj/`


Get gdal

`curl -o gdal-2.3.1.tar.gz http://download.osgeo.org/gdal/CURRENT/gdal-2.3.1.tar.gz`

`tar -zxvf gdal-2.3.1.tar.gz`

`cd gdal-2.3.1`

`./configure`
