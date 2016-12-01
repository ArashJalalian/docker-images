FROM phusion/baseimage
CMD ["/sbin/my_init"]

# install java
ENV JAVA_VERSION_MAJOR 8
ENV JAVA_VERSION_MINOR 111
ENV JAVA_VERSION_BUILD 14
ENV JAVA_PACKAGE       jdk
RUN curl -jksSLH "Cookie: oraclelicense=accept-securebackup-cookie"\
  http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz \
    | tar -xzf - -C /opt &&\
    ln -s /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/jdk &&\
    rm -rf /opt/jdk/*src.zip \
           /opt/jdk/lib/missioncontrol \
           /opt/jdk/lib/visualvm \
           /opt/jdk/lib/*javafx* \
           /opt/jdk/jre/lib/plugin.jar \
           /opt/jdk/jre/lib/ext/jfxrt.jar \
           /opt/jdk/jre/bin/javaws \
           /opt/jdk/jre/lib/javaws.jar \
           /opt/jdk/jre/lib/desktop \
           /opt/jdk/jre/plugin \
           /opt/jdk/jre/lib/deploy* \
           /opt/jdk/jre/lib/*javafx* \
           /opt/jdk/jre/lib/*jfx* \
           /opt/jdk/jre/lib/amd64/libdecora_sse.so \
           /opt/jdk/jre/lib/amd64/libprism_*.so \
           /opt/jdk/jre/lib/amd64/libfxplugins.so \
           /opt/jdk/jre/lib/amd64/libglass.so \
           /opt/jdk/jre/lib/amd64/libgstreamer-lite.so \
           /opt/jdk/jre/lib/amd64/libjavafx*.so \
           /opt/jdk/jre/lib/amd64/libjfx*.so
ENV JAVA_HOME /opt/jdk
ENV PATH ${PATH}:${JAVA_HOME}/bin

#  install and run bamboo
ENV BAMBOO_VERSION 5.14.1
ENV BAMBOO_HOME /home/bamboo
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -yq python-software-properties && apt-get update
RUN apt-get update && apt-get install -y wget && rm -rf /var/lib/apt/lists/*
RUN wget --progress=dot:mega http://downloads.atlassian.com/software/bamboo/downloads/atlassian-bamboo-${BAMBOO_VERSION}.tar.gz -O /tmp/atlassian-bamboo.tar.gz &&\
  tar xzf /tmp/atlassian-bamboo.tar.gz -C /opt &&\
  rm -f /tmp/atlassian-bamboo.tar.gz
RUN mkdir -p ${BAMBOO_HOME}
EXPOSE 8085
EXPOSE 54663
ENTRYPOINT [ "sh", "-c", "/opt/atlassian-bamboo-${BAMBOO_VERSION}/bin/catalina.sh run" ]

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
