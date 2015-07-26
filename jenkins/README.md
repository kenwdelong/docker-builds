# Jenkins

## Volumes
Link out from:
* /var/jenkins_home - this is where Jenkins puts all it's stuff
* /usr/local/maven/conf - this will allow you to set up your own settings.xml file, and control where you want the local maven repository to go (hint, not inside your docker container).

## Ports
* Jenkins is on 8080