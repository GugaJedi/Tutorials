# HOW TO HTTP + PHP 7.4 + POSTGRESQL + MARIADB10.5

This is a collection of information that worked for me and therefore became a tutorial on how to install through yum a ecomm web server...

```
cd /home/centos
curl -O http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
curl -O http://rpms.remirepo.net/enterprise/remi-release-7.rpm
curl -O https://repo.zabbix.com/zabbix/5.0/rhel/7/x86_64/zabbix-release-5.0-1.el7.noarch.rpm
curl -O https://packages.erlang-solutions.com/erlang-solutions-2.0-1.noarch.rpm
curl -O https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
curl -O https://packages.erlang-solutions.com/rpm/erlang_solutions.asc
curl -O http://www.webmin.com/jcameron-key.asc
curl -sL https://rpm.nodesource.com/setup_14.x | sudo -E bash -
curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
rpm --import https://packages.erlang-solutions.com/rpm/erlang_solutions.asc
rpm --import http://www.webmin.com/jcameron-key.asc
yum -y install *.rpm && yum -y install yum-utils && yum-config-manager --enable remi && yum-config-manager --enable epel && yum-config-manager --enable zabbix && yum-config-manager --enable remi-php74 && yum install -y yarn && yum -y install wget vim-enhanced zip unzip htop iotop tcpdump telnet links nfs-utils erlang zabbix-agent
```

```sh
echo "# MariaDB 10.5 CentOS repository list - created 2020-09-16 19:42 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.5/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1" > /etc/yum.repos.d/MariaDB.repo
```

```sh
vim /etc/yum.repos.d/CentOS-Base.repo
```

add:

exclude=postgresql* to [base] and [updates]

```sh
yum -y upgrade; yum -y install postgresql96 postgresql96-devel postgresql96-libs postgresql96-server
```

rm -fR /var/lib/pgsql/9.6/data

ln -sf /data /var/lib/pgsql/9.6/data

chown -fR postgres.postgres /data; chown -fR postgres.postgres /var/lib/pgsql/9.6/data

su - postgres

/usr/pgsql-9.6/bin/initdb -E LATIN1 --locale=pt_BR --lc-messages=pt_BR --lc-monetary=pt_BR --lc-numeric=pt_BR --lc-time=pt_BR /data

			Success. You can now start the database server using:
			
				/usr/pgsql-9.6/bin/pg_ctl -D /data -l logfile start
				#not necessary to run this command... return to root

systemctl enable postgresql-9.6
systemctl start postgresql-9.6

yum -y install MariaDB-client

	#only if you are going to run mysql as server

	yum -y install MariaDB-server
	systemctl enable mariadb
	systemctl start mariadb
	#MariaDB-server wasn't installed at BC-ECOMM-01

yum -y install httpd httpd-tools php php-mysql php-pdo php-gd php-mbstring php-pgsql

echo "<?php phpinfo(); ?>" > /var/www/html/info.php

systemctl enable httpd
systemctl restart httpd

sed -i 's/^SELINUX=.*/SELINUX=disabled/g' /etc/selinux/config

reboot

yum -y install geoip-devel libmaxminddb-devel tokyocabinet-devel goaccess

chcon -R -t httpd_sys_content_t /var/www/html

