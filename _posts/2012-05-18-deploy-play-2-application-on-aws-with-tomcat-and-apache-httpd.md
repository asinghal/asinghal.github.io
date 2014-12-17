---
author: Aishwarya Singhal
comments: true
date: 2012-05-18 08:02:31+00:00
layout: post
slug: deploy-play-2-application-on-aws-with-tomcat-and-apache-httpd
title: Deploy Play 2 application on AWS with Tomcat and Apache HTTPD
wordpress_id: 124
tags:
- Play Framework
- Scala
- Set up
---

I have created a web application on Play 2.0 framework, in Scala. To deploy it, I looked at various cloud options - [Amazon](http://aws.amazon.com/ec2/) looks the best because, well its free :-)  Once the instance was created, it already had Java 6, I installed Apache HTTPD and Tomcat 7.

Lets first add some swap space

	sudo -i
	dd if=/dev/zero of=/swapfile bs=1024 count=524288
	mkswap /swapfile
	swapon /swapfile

Now edit /etc/fstab and append the following line to it:

	/swapfile swap swap defaults 0 0

Ok, lets install tomcat and httpd now.

	yum -y install httpd
	mkdir -p /var/www/html/assets
	mkdir -p /usr/share/tomcat7
	cd /usr/share/tomcat7
	wget http://apache.mirrors.timporter.net/tomcat/tomcat-7/v7.0.27/bin/apache-tomcat-7.0.27.tar.gz
	gzip -d apache-tomcat-7.0.27.tar.gz tar xvf apache-tomcat-7.0.27.tar
	mkdir -p /var/log/tomcat7 /var/cache/tomcat7/temp /var/lib/tomcat7/webapps /var/cache/tomcat7/work
	rm -rf logs temp webapps work
	ln -s logs /var/log/tomcat7
	ln -s webapps /var/lib/tomcat7/webapps
	ln -s work /var/cache/tomcat7/work
	ln -s temp /var/cache/tomcat7/temp
	useradd -d /usr/share/tomcat7 tomcatusr
	chown -R tomcatusr /var/log/tomcat7
	chown -R tomcatusr /var/cache/tomcat7/
	chown -R tomcatusr /var/lib/tomcat7
	chown -R tomcatusr /usr/share/tomcat7

Now open the server.xml (inside /usr/share/tomcat7/conf) and comment out the connector for port 8080

```xml
	 <!-- Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" / --> 
```

Look for 8009 (AJP connector) and modify it to:

```xml
	<Connector port="8009" enableLookups="false" redirectPort="8443" protocol="AJP/1.3" URIEncoding="UTF-8" />
```

Now create a start up script under /etc/init.d and call it tomcat7:

```bash
	#!/bin/bash

	# Tomcat7: Start/Stop Tomcat 7
	#
	# chkconfig: - 90 10
	# description: Tomcat is a Java application Server.

	. /etc/init.d/functions
	. /etc/sysconfig/network

	CATALINA_HOME=/usr/share/tomcat7
	TOMCAT_USER=tomcatusr
	LOCKFILE=/var/lock/subsys/tomcat

	RETVAL=0
	start(){
	 echo "Starting Tomcat7: "
	 su - $TOMCAT_USER -c "$CATALINA_HOME/bin/startup.sh"
	 RETVAL=$?
	 echo
	 [ $RETVAL -eq 0 ] && touch $LOCKFILE
	 return $RETVAL
	}

	stop(){
	 echo "Shutting down Tomcat7: "
	 $CATALINA_HOME/bin/shutdown.sh
	 RETVAL=$?
	 echo
	 [ $RETVAL -eq 0 ] && rm -f $LOCKFILE
	 return $RETVAL
	}

	case "$1" in
	 start)
	 start
	 ;;
	 stop)
	 stop
	 ;;
	 restart)
	 stop
	 start
	 ;;
	 status)
	 status tomcat
	 ;;
	 *)
	 echo $"Usage: $0 {start|stop|restart|status}"
	 exit 1
	 ;;
	esac
	exit $?
```

All set. Now let us connect the HTTPD to talk to Tomcat.

1. Open `/etc/httpd/conf/httpd.conf` for editting

2. Go to the end of the file and uncomment the VirtualHost (port 80). The whole block, of course.

3. Add the following inside the VirtualHost

```
	ErrorLog logs/error_log

	CustomLog logs/ajp.log combined

	SetOutputFilter DEFLATE

	BrowserMatch ^Mozilla/4 gzip-only-text/html

	BrowserMatch ^Mozilla/4\.0[678] no-gzip

	BrowserMatch \bMSIE !no-gzip !gzip-only-text/html

	# Don't compress images

	SetEnvIfNoCase Request_URI \

	\.(?:gif|jpe?g|png)$ no-gzip dont-vary

	# Make sure proxies don't deliver the wrong content

	#Header append Vary User-Agent env=!dont-vary

	ExpiresByType image/gif A604800

	ExpiresByType image/png A604800

	ExpiresByType image/jpg A604800

	<Proxy *>

	AddDefaultCharset Off

	Order deny,allow

	Allow from all

	</Proxy>

	ProxyPass /assets !

	ProxyPass / ajp://localhost:8009/

	ProxyPassReverse / ajp://localhost:8009/
```

The above will enable gzip compression on your pages (for performance), cache images on the client for a week and enable you to serve static assets from the webserver itself.

Set docroot and error pages:

	DocumentRoot "/var/www/html"

	ErrorDocument 404 /assets/html/missing.html

	ErrorDocument 503 /assets/html/missing.html


All done. Now use the [Play WAR plugin](https://github.com/dlecan/play2-war-plugin) to generate the WAR file. Copy the generated WAR file into `/var/lib/tomcat7/webapps` as ROOT.war (otherwise you don't get the "/" root URL).

Package the static files from inside `APP_HOME/public` separately into a TAR and extract into the `/var/www/html/assets` directory.
