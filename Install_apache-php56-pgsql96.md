# TUTORIAL

## Instalação de Servidor Zanthus para Ambiente Cloud

# SETUP

1. usuários
    ```sh
    useradd -r zanthus; useradd postgres
    ```
1. diretórios
    ```sh
    cd /; mkdir backup infra web data; cd /infra; mkdir _env libs logs pacotes tmpz utils primeshare; mkdir -p /Zanthus/Zeus/Manager
    ```
    1. permissões de diretórios
    ```
    chown -fR zanthus.zanthus /Zanthus
    chown -fR postgres.postgres /data
    ```
1. repositórios
    ```sh
    cd /home/'seu-usuario'/
    curl -O http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
    curl -O http://rpms.remirepo.net/enterprise/remi-release-7.rpm
    curl -O https://repo.zabbix.com/zabbix/5.0/rhel/7/x86_64/zabbix-release-5.0-1.el7.noarch.rpm
    curl -O https://packages.erlang-solutions.com/erlang-solutions-2.0-1.noarch.rpm
    curl -sL https://rpm.nodesource.com/setup_14.x | sudo bash -
    curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
    rpm --import https://packages.erlang-solutions.com/rpm/erlang_solutions.asc
    rpm --import http://www.webmin.com/jcameron-key.asc
    yum -y install *.rpm
    ```
1. yum
    ```sh
    yum -y install wget gcc gcc-c++ zlib-devel libxml2-devel openssl-devel \
                   curl-devel freetype-devel gd-devel libjpeg-devel \
                   libpng-devel python-devel openldap-devel libmcrypt-devel \
                   bzip2-devel kernel-devel kernel-headers bzip2 memcached \
                   telnet links nfs-utils autoconf ftp curl vim-enhanced \
                   zip unzip htop iotop rsync ntsysv nss curl socat dkms \
                   make perl net-tools perl-Digest-MD5 lvm2 git nvme-cli \
                   syslog-ng cifs-utils openssl098e zabbix-agent nodejs \
                   yarn ncurses ncurses-devel geoip-devel libmaxminddb-devel \
                   openssl-devel tokyocabinet-devel goaccess tcpdump erlang \
                   traceroute net-snmp; yum -y upgrade
    ```
1. pacotes compilados
    - `zlib`
        ```sh
        cd /pacotes && curl -O https://www.zlib.net/zlib-1.2.11.tar.gz && cp -farp zlib-1.2.11.tar.gz /usr/src/ && cd /usr/src/ && tar -xzf zlib-1.2.11.tar.gz && cd zlib-1.2.11 && ./configure --prefix=/usr/local/lib64 && make && make install
        ```
    - libxml2
        ```sh
        cd /pacotes && curl -O ftp://xmlsoft.org/libxml2/libxml2-2.9.9.tar.gz && cp -farp libxml2-2.9.9.tar.gz /usr/src/ && cd /usr/src/ && tar -xzf libxml2-2.9.9.tar.gz && cd libxml2-2.9.9 && ./configure --prefix=/usr/local/lib64 && make && make install
       ```
    - postgres
        ```sh
        cd /pacotes && curl -O https://ftp.postgresql.org/pub/source/v9.6.21/postgresql-9.6.21.tar.gz && cp -arp postgresql-9.6.21.tar.gz /usr/src && cd /usr/src/ && tar -xzf postgresql-9.6.21.tar.gz && cd postgresql-9.6.21 && ./configure --prefix=/usr/local/pgsql --without-readline && make && make install
        ```
        1. links simbólicos
            ```sh
            ln -sf /usr/local/pgsql/bin/psql /usr/bin/psql; ln -sf /usr/local/pgsql /var/lib/pgsql
            ```
