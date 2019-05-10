FROM krallin/centos-tini:centos7
MAINTAINER kenwdelong
# Based on cooniur/java

ENV JAVA_VERSION=8.0.212 \
	ZULU_VERSION=8.38.0.13-ca \
    JAVA_HOME=/usr/local/java \
    TMP_DIR=/tmp/java \
    TMP_FILE=$TMP_DIR/java.tar.gz

RUN yum -y install wget tar sudo && \
    yum clean all && \
    mkdir -p $JAVA_HOME && \
	mkdir -p $TMP_DIR && \
    wget --quiet --output-document="$TMP_FILE" \
        --no-cookies --no-check-certificate \
        "https://cdn.azul.com/zulu/bin/zulu${ZULU_VERSION}-jdk${JAVA_VERSION}-linux_x64.tar.gz" && \
    tar -xf "$TMP_FILE" --directory="$JAVA_HOME" --strip-components 1 && \
    rm "$TMP_FILE"
# If I set the path up above with the other ENV vars, it doesn't work.
ENV PATH $JAVA_HOME/bin:$PATH
