---
published: true
title: Using monit to restart processes
layout: post
---
Monit is an invaluable tool for configuring an automated production environment, it offers streamlined and simple monitoring, takes actions based on defined conditions and it's syntax is incredibly easy to read.

The following example is used in the Bseller.com.br production environment to restart misbehaving tomcat processes, monitoring for cpu, process memory, port binding and lastly system memory.

	check process tomcat with pidfile /var/run/tomcat5.5.pid
		start program = "/etc/init.d/tomcat5.5 start"
		stop program = "/etc/init.d/tomcat5.5 stop"
		if cpu > 80% for 5 cycles then alert
			if cpu > 90% for 10 cycles then restart
			if totalmem > 1500.0 MB for 5 cycles then restart
		if failed host 127.0.0.1 port 8080 then alert
		if 5 restarts within 5 cycles then timeout
	check system localhost
		if memory usage > 95% for 5 cycles then exec "/sbin/shutdown -r now"


For a basic introduction to monit, check the official docs at http://mmonit.com/monit/
