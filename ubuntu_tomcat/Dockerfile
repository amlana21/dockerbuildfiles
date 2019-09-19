FROM ubuntu:16.04
RUN mkdir /servers
RUN mkdir /servers/tomcat8 && apt-get -y update && apt-get -y install default-jdk
ENV CATALINA_HOME /servers/tomcat8
ENV PATH $PATH:$CATALINA_HOME/bin
ADD apache-tomcat-8.5.31 /servers/tomcat8
COPY server.xml /servers/tomcat8/conf
COPY tomcat-users.xml /servers/tomcat8/conf
COPY context.xml /servers/tomcat8/webapps/manager/META-INF

RUN chmod +x $CATALINA_HOME/bin/startup.sh && chmod +x $CATALINA_HOME/bin/startup.bat && chmod +x $CATALINA_HOME/bin/shutdown.bat && chmod +x $CATALINA_HOME/bin/shutdown.sh  && chmod +x $CATALINA_HOME/bin/catalina.sh

EXPOSE 8094


CMD ["catalina.sh","run"]