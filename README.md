#Servicemix Install Tutorial
Some notes on installing Servicemix with Fedora on linux (centos) 


#Step 1 : Setup directories if needed otherwise goto step 2
```
$ sudo mkdir /utility

$ sudo mkdir /utility/sidora

$ sudo ln -s /utility/sidora /opt/sidora

$ sudo chown -h fedora:fedora /opt/sidora
```

#Step 2 : Download and Install Servicemix
```
$ cd /opt/sidora/

$ sudo wget http://archive.apache.org/dist/servicemix/servicemix-5/5.4.0/apache-servicemix-5.4.0.zip

$ sudo unzip apache-servicemix-5.4.0.zip

$ sudo ln -s apache-servicemix-5.4.0 servicemix

$ sudo chown -h fedora:fedora servicemix
```

#Step 3 : Configure Servicemix as a system service

```
$ sudo /opt/sidora/servicemix/bin/servicemix
```
```
 ____                  _          __  __ _      
/ ___|  ___ _ ____   _(_) ___ ___|  \/  (_)_  __
\___ \ / _ \ '__\ \ / / |/ __/ _ \ |\/| | \ \/ /
 ___) |  __/ |   \ V /| | (_|  __/ |  | | |>  < 
|____/ \___|_|    \_/ |_|\___\___|_|  |_|_/_/\_\

  Apache ServiceMix (5.4.0)

Hit '<tab>' for a list of available commands
and '[cmd] --help' for help on a specific command.
Hit '<ctrl-d>' or 'osgi:shutdown' to shutdown ServiceMix.

karaf@root> features:install wrapper

karaf@root> wrapper:install -s AUTO_START -n karaf -d Karaf -D "Karaf Service"

karaf@root> shutdown

karaf@root> yes
```
```
$ sudo chown -R fedora:fedora /opt/sidora/apache-servicemix-5.4.0

$ sudo vim /opt/sidora/servicemix/bin/karaf-service
```
```
:%s/\/utility\/sidora\/apache-servicemix-5.4.0/\/opt\/sidora\/servicemix/g

:%s/#RUN_AS_USER=/#RUN_AS_USER=\rRUN_AS_USER=fedora/g

:x
```
```
$ sudo vim /opt/sidora/servicemix/etc/karaf-wrapper.conf
```
```
:%s/\/utility\/sidora\/apache-servicemix-5.4.0/\/opt\/sidora\/servicemix/g

:%s/set.default.JAVA_HOME=null/set.default.JAVA_HOME=\/opt\/java

:x
```
```
$ sudo ln -s /opt/sidora/servicemix/bin/karaf-service /etc/init.d/

$ sudo chkconfig karaf-service --add

$ sudo chkconfig karaf-service on

$ sudo service karaf-service start
```

#Check that Servicemix is running:
```
$ sudo service karaf-service status
Karaf is running (5212).
```
