FROM ubuntu

ENV VERSION 2.44.0

EXPOSE 4444

RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections
RUN apt-get install oracle-java7-installer -y
RUN wget http://selenium-release.storage.googleapis.com/${VERSION%.*}/selenium-server-standalone-${VERSION}.jar
ADD run.sh /var/run.sh
RUN chmod 755 /var/run.sh

CMD ["/bin/bash", "/var/run.sh"]