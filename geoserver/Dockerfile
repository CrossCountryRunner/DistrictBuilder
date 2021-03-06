# A GeoServer installation
FROM openjdk:8-jre-alpine

ENV GEOSERVER_VERSION 2.11.2
ENV GEOSERVER_ZIP_URL http://sourceforge.net/projects/geoserver/files/GeoServer/${GEOSERVER_VERSION}/geoserver-${GEOSERVER_VERSION}-bin.zip

ENV GEOSERVER_DIR /usr/share
ENV GEOSERVER_EXT_DIR $GEOSERVER_DIR/geoserver-$GEOSERVER_VERSION/webapps/geoserver/WEB-INF/lib
ENV PATH /usr/share/geoserver-$GEOSERVER_VERSION/bin:$PATH
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV GEOSERVER_HOME $GEOSERVER_DIR/geoserver-$GEOSERVER_VERSION/

RUN apk add --update ca-certificates openssl && update-ca-certificates && \
  wget -O $GEOSERVER_DIR/geoserver.zip $GEOSERVER_ZIP_URL && \
  unzip -qq $GEOSERVER_DIR/geoserver.zip -d $GEOSERVER_DIR && \
  rm $GEOSERVER_DIR/geoserver.zip

ENV GEOSERVER_DATA_DIR /data

VOLUME $GEOSERVER_DATA_DIR

COPY ./jetty.xml $GEOSERVER_DIR/etc/jetty.xml
COPY ./geoserver-startup.sh $GEOSERVER_HOME/bin/geoserver-startup.sh

WORKDIR $GEOSERVER_HOME

CMD ["sh", "bin/geoserver-startup.sh"]
