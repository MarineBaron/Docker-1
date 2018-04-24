FROM  debian:latest

ENV   TS_VERSION=3.0.13.8 \
      TS_FILENAME=teamspeak3-server_linux_amd64 \
      TS_USER=teamspeak \
      TS_HOME=/teamspeak \
	  TS3SERVER_LICENSE=accept

RUN   apt-get update && apt-get install wget bzip2 -y \
      && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN   groupadd -r $TS_USER \
      && useradd -r -m \
        -g $TS_USER \
        -d $TS_HOME \
        $TS_USER

WORKDIR ${TS_HOME}

RUN  wget "http://dl.4players.de/ts/releases/${TS_VERSION}/${TS_FILENAME}-${TS_VERSION}.tar.bz2" -O ${TS_FILENAME}-${TS_VERSION}.tar.bz2 \
       && tar -xjf "${TS_FILENAME}-${TS_VERSION}.tar.bz2" \
       && rm ${TS_FILENAME}-${TS_VERSION}.tar.bz2 \
       && mv ${TS_FILENAME}/* ${TS_HOME} \
       && rm -r ${TS_HOME}/tsdns \
       && rm -r ${TS_FILENAME}

RUN chown -R ${TS_USER}:${TS_USER} ${TS_HOME}

USER  ${TS_USER}

EXPOSE 9987/udp
EXPOSE 10011
EXPOSE 30033

CMD ["sh", "ts3server_minimal_runscript.sh"]
