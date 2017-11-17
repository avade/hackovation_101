# Getting Started with Cloud Foundry

All of your interactions with Cloud Foundry will be through the command line.

Have a look at the official _Getting Started Guide_ if you are not familiar with it yet: https://docs.cloudfoundry.org/cf-cli/getting-started.html

### Debian and Ubuntu-based Linux distributions Installation::

1. Add the Cloud Foundry Foundation public key and package repository to your system:
```
$ wget -q -O - https://packages.cloudfoundry.org/debian/cli.cloudfoundry.org.key | sudo apt-key add -
$ echo "deb http://packages.cloudfoundry.org/debian stable main" | sudo tee /etc/apt/sources.list.d/cloudfoundry-cli.list
```
2. Update your local package index:
```
$ sudo apt-get update
```
3. Install the cf CLI:
```
$ sudo apt-get install cf-cli
```

### Enterprise Linux and Fedora systems (RHEL6/CentOS6 and up) Installation::

1. Configure the Cloud Foundry Foundation package repository:
```
$ sudo wget -O /etc/yum.repos.d/cloudfoundry-cli.repo https://packages.cloudfoundry.org/fedora/cloudfoundry-cli.repo
```
2. Install the cf CLI, which also downloads and adds the public key to your system:
```
$ sudo yum install cf-cli
```

### Mac OS Installation::

1. Download the OS X installer from:
```
https://cli.run.pivotal.io/stable?release=macosx64&source=github
```
2. Open the .pkg file.
3. In the installer wizard, click Continue.
4. Select an install destination and click Continue.
5. When prompted, click Install.


### Windows Installation::

1. Download the Windows installer from:
```
https://cli.run.pivotal.io/stable?release=windows64&source=github
```
2. Unpack the zip file.
3. Double click the cf CLI executable.
4. When prompted, click Install, then Close.


To verify your installation, open a terminal window and type:
```
$ cf -v
```
If your installation was successful, the cf CLI help listing appears.


## Login to Cloud Foundry
```
$ cf login -a https://api.us-west-2.apps.msi.audi.com
```

You will be redirected to the organisation "hackovation" and your team space. Only organisations and spaces that you have permission for will be displayed. If you come up with an idea to interact with more than one space ask TECH-TEAM to grant you access to more than one space.


## Deploy a "Simple" application

1. Clone the following repository:
```
$ git clone https://github.com/abi-open/cf-sample-app-spring
```
2. Push your application:
```
$ cf push
```
3. Check if you application is running:
```
$ cf apps
```
4. By default on application will be mapped automatically to the standard DNS entry (cf.hackovation.io), you can copy the domain name and open it on a web-browser.

5. Delete your app after you are finished with it
```
$ cf delete cf-hackovation
```

## Services in Cloud Foundry Marketplace
The following services are available in our Cloud Foundry Marketplace, use them as you see fit:
* Neo4J 3.0.2
* PostgreSQL 9.4
* MySQL 5.6
* Redis 3.2.0
* MongoDB 3.0.7
* RabbitMQ 3.6.2
* Zookeeper 3.4.6
* Cassandra
* Apache Jackrabbit
