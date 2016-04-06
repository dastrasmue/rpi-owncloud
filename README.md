# rpi-owncloud

This is a docker image for ownCloud 9.0.0 (March 8 2016) on the Raspberry Pi.

It was forked from https://bitbucket.org/schoeffm/rpi-docker/
Changes made:

    update to Version 9.0.0
    data and config directory are mounted to local directories

To get owncloud running, you have to do a few simple steps:

    checkout the docker-compose.yml and folder structure from https://github.com/dastrasmue/rpi-owncloud.git
    git clone https://github.com/dastrasmue/rpi-owncloud.git && cd rpi-owncloud

    set the OWNCLOUD_SERVERNAME in docker-compose.yml to the public ip address that points to your raspberry
    e.g. vim docker-compose.yml

    ...
    OWNCLOUD_SERVERNAME: user123.no-ip.org
    ...
    start the database and owncloud server with docker-compose
    docker-compose up

You can stop the server with
docker-compose stop
and restart it with
docker-compose up
or
docker-compose start

Your data and config is stored in
rpi-owncloud/data
rpi-owncloud/config

To backup the database you can use:
docker exec rpiowncloud_db1 mysqldump --lock-tables -u owncloud -pmycloud owncloud > owncloud-sqlbkpdate +"%Y%m%d".bak

Don't be scared if you get a integrity check error. This is due to the trusteddomainhelper.php that whe mount to have a temporary fix for the bug introduced in 9.0.0 (https://forum.owncloud.org/viewtopic.php?f=38&t=34229).
Also be aware, that the ownership of the data and config directories is changed to www-data.

