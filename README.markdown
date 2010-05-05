# A Recipe for a Redis RPM on CentOS

Perform the following on a build box as root.

## Create an RPM Build Environment

    yum install rpmdevtools
    rpmdev-setuptree

## Install Prerequisites for RPM Creation

    yum groupinstall 'Development Tools'

## Download Redis

    cd /tmp
    wget http://github.com/antirez/redis/tarball/v1.3.9
    tar -xzf antirez-redis-v1.3.9-0-gd4dd655.tar.gz
    mv antirez-redis-d495a77 redis-1.3.9
    tar -czf redis-1.3.9.tar.gz redis-1.3.9
    cp redis-1.3.9.tar.gz ~/rpmbuild/SOURCES/

## Get Necessary System-specific Configs

    git clone git://github.com/causes/redis-centos.git
    cp redis-centos/conf/redis.conf ~/rpmbuild/SOURCES/
    cp redis-centos/spec/redis.spec ~/rpmbuild/SPECS/

## Build the RPM

    cd ~/rpmbuild/
    rpmbuild -ba SPECS/redis.spec

The resulting RPM will be:

    ~/rpmbuild/RPMS/x86_64/redis-1.3.9-1.x86_64.rpm

## Credits

Based on the `redis.spec` file from Jason Priebe, found on [Google Code][gc].

 [gc]: http://groups.google.com/group/redis-db/files
