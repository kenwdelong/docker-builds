# ELK Image
A simple customization of sebp's elk image, but changing the input file to work with `net.logstash.logback.appender.LogstashTcpSocketAppender`.

An example logback.xml file might be

	<?xml version="1.0" encoding="UTF-8"?>
	<configuration>
	
		<appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
			<layout class="ch.qos.logback.classic.PatternLayout">
				<Pattern>%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n</Pattern>
			</layout>
		</appender>
		
		<appender name="stash" class="net.logstash.logback.appender.LogstashTcpSocketAppender">
			<remoteHost>192.168.59.103</remoteHost>
			<port>5000</port>
			<encoder class="net.logstash.logback.encoder.LogstashEncoder" />
		</appender>
		
		<logger name="demo" level="debug"/>
		
		<root level="debug">
			<appender-ref ref="STDOUT" />
			<appender-ref ref="stash"/>
		</root>
	
	</configuration>
