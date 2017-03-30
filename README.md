# brightspot-server
This is an [Ant](http://ant.apache.org) build script that automates the steps of the [Advanced Installation](http://docs.brightspot.com/cms/developers-guide/installation/advanced.html) of Brightspot.

## Features
* Interactive - zero configuration. The script asks you what to name your database and server directory.
* Creates a project-specific database (if MySQL is running).
* Creates a Brightspot-specific version of Tomcat.
* Configures proper permissions and ownership of the server directory.
* Makes the Tomcat shell scripts executable.

## Limitations
* It does not install MySQL (yet). See Prerequisites below.

## Prerequisites
* Java 8 - Download and install the latest release of [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Ant - Download and install [Ant 1.9.7 or higher](http://ant.apache.org/bindownload.cgi). Make sure ```ant``` is on your PATH.
* MySQL - Download and install [MySQL 5.6.31 or higher](https://dev.mysql.com/downloads/mysql/5.6.html#downloads).

## Installation
[Download](https://github.com/OttoHagg/brightspot-server/archive/master.zip) the latest version and extract contents to some directory where you want to host your server. For example, ```~/dev/servers```. Once you do that you want to ensure the ```_template``` directory and ```build.xml``` file are at the root of this directory.

You may delete the ```LICENSE``` and ```README.md``` files.

```
~/dev/servers/_template
~/dev/servers/build.xml
```
## Usage

To run this script simply type ```ant``` at the root of your ```~/dev/servers``` directory.

```
$ cd ~/dev/servers
$ ant
$ ...
```

This script will create new server directories here. So, for example, if you name your server "myapp" you'll have a new directory sibling to _template named myapp.

```
~/dev/servers/_template
~/dev/servers/build.xml
~/dev/servers/myapp
```

## Great! Now What?
Start your new server as you would with any Tomcat.

```
cd ~/dev/server/myapp/bin
$ ./startup.sh
```

Stopping your server is just as familiar.

```
cd ~/dev/server/myapp/bin
$ ./shutdown.sh
```

And, lastly, if you're here, you're probably doing some Brightspot development.

### Build your Brightspot Project
The artifact of building your project is a war file, typically at ```target/myapp-1.0.0-SNAPSHOT.war```. You can copy this file to your server's ```webapps``` directory and rename the file to ```ROOT.war```. Tomcat will hot-deploy this as the default application.

### Link your War File
Better yet, link your target's artifact to ROOT.war in your server's ```webapps``` directory. For example:

```
$ cd ~/dev/server/myapp/webapps
$ ln -sf ~/dev/workspace/myapp/target/myapp-1.0.0-SNAPSHOT.war ./ROOT.war
```


## Version Details
* Tomcat 8.0.26
* MySQL Connector 5.0.8
* Solr 4.8.1