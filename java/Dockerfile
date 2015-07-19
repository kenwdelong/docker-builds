FROM centos:centos7
MAINTAINER kenwdelong
# Based on cooniur/java

ENV JAVA_VERSION="8u51" \
    JAVA_LONG_VERSION="8u51-b16" \
    JAVA_HOME="/usr/local/java" \
    PATH="$JAVA_HOME/bin:$PATH" \
    TMP_FILE="/tmp/java/tar.gz"

RUN yum -y install wget tar && yum clean all


RUN yum -y install wget tar && \
    yum clean all && \
    mkdir -p $JAVA_HOME && \
	wget --quiet --output-document="$TMP_FILE" \
		--no-cookies --no-check-certificate \
		--header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
		"http://download.oracle.com/otn-pub/java/jdk/$JAVA_LONG_VERSION/server-jre-$JAVA_VERSION-linux-x64.tar.gz" && \
	tar -xf "/tmp/java.tar.gz" --directory="$JAVA_HOME" --strip-components 1 && \
	rm "$TMP_FILE"
