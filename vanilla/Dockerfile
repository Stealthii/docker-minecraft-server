FROM java:8

MAINTAINER stealthii

# Install server admin dependencies

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
      libmozjs-24-bin \
      imagemagick \
      lsof \
      nano \
      sudo \
      vim && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    update-alternatives --install /usr/bin/js js /usr/bin/js24 100

RUN wget -O /usr/bin/jsawk https://github.com/micha/jsawk/raw/master/jsawk && \
    chmod +x /usr/bin/jsawk

RUN useradd -M -s /bin/false --uid 1000 minecraft && \
    mkdir /data && \
    mkdir /config && \
    mkdir /mods && \
    mkdir /plugins && \
    chown minecraft:minecraft /data /config /mods /plugins

EXPOSE 25565

COPY start.sh /start
COPY start-minecraft.sh /start-minecraft

VOLUME ["/data"]
VOLUME ["/mods"]
VOLUME ["/config"]
VOLUME ["/plugins"]
COPY server.properties /tmp/server.properties
WORKDIR /data

CMD [ "/start" ]

# Special marker ENV used by MCCY management tool
ENV MC_IMAGE=YES

ENV UID=1000 GID=1000
ENV MOTD A Minecraft Server Powered by Docker
ENV JVM_OPTS -Xmx1024M -Xms1024M
ENV TYPE=VANILLA VERSION=LATEST FORGEVERSION=RECOMMENDED LEVEL=world PVP=true DIFFICULTY=easy \
  LEVEL_TYPE=DEFAULT GENERATOR_SETTINGS= WORLD= MODPACK=
