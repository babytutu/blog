---
title: Install MongoDB on CentOS
date: 2018-11-18 21:58:32
tags:
  - MongoDB
categories:
  - CentOS
---

# Install MongoDB Community Edition

> This installation guide only supports 64-bit systems.

## Using .rpm Packages (Recommended)

<!--more-->

### Configure the package management system (yum).

> Create a /etc/yum.repos.d/mongodb-org-4.2.repo file so that you can install MongoDB directly using yum:

```
[mongodb-org-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.1/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.1.asc
```

### Install the MongoDB packages.

> To install the latest stable version of MongoDB, issue the following command:

```bash
sudo yum install -y mongodb-org
```

> To install a specific release of MongoDB, specify each component package individually and append the version number to the package name, as in the following example:

```bash
sudo yum install -y mongodb-org-4.1.5 mongodb-org-server-4.1.5 mongodb-org-shell-4.1.5 mongodb-org-mongos-4.1.5 mongodb-org-tools-4.1.5
```


# Run MongoDB Community Edition

## Start MongoDB.

> You can start the mongod process by issuing the following command:

```bash
sudo service mongod start
```

## Verify that MongoDB has started successfully

> You can verify that the mongod process has started successfully by checking the contents of the log file at /var/log/mongodb/mongod.log for a line reading

```bash
[initandlisten] waiting for connections on port <port>
```
> where <port> is the port configured in /etc/mongod.conf, 27017 by default.

> You can optionally ensure that MongoDB will start following a system reboot by issuing the following command:

```bash
sudo chkconfig mongod on
```

## Stop MongoDB

> As needed, you can stop the mongod process by issuing the following command:

```bash
sudo service mongod stop
```

## Restart MongoDB.

> You can restart the mongod process by issuing the following command:

```bash
sudo service mongod restart
```
> You can follow the state of the process for errors or important messages by watching the output in the /var/log/mongodb/mongod.log file.

## Begin using MongoDB.

> Start a mongo shell on the same host machine as the mongod. You can run the mongo shell without any command-line options to connect to a mongod that is running on your localhost with default port 27017:

```bash
mongo
```

# Uninstall MongoDB Community Edition

> To completely remove MongoDB from a system, you must remove the MongoDB applications themselves, the configuration files, and any directories containing data and logs. The following section guides you through the necessary steps.

## Stop MongoDB.

> Stop the mongod process by issuing the following command:

```bash
sudo service mongod stop
```
## Remove Packages

> Remove any MongoDB packages that you had previously installed.

```bash
sudo yum erase $(rpm -qa | grep mongodb-org)
```

## Remove Data Directories.

> Remove MongoDB databases and log files.

```bash
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongo
```


# 参考文档
[Install MongoDB Community Edition on Red Hat Enterprise or CentOS Linux](https://docs.mongodb.com/master/tutorial/install-mongodb-on-red-hat/)