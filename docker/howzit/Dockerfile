FROM debian:11

RUN apt-get update
RUN apt-get install -y --no-install-recommends --no-install-suggests \
    ca-certificates cmake g++ git make autoconf coreutils libtool pkg-config \
    libevent-dev libssl-dev libsqlite3-dev libmicrohttpd-dev
RUN update-ca-certificates

RUN mkdir -p /coturn/logs
RUN mkdir -p /coturn/storage
RUN mkdir -p /coturn/howzit_coturn
WORKDIR /coturn
# Maybe make this repo private at some point
RUN git clone https://github.com/HazimMohamed/howzit_coturn.git
WORKDIR /coturn/howzit_coturn

RUN ./configure --turndbdir=/coturn/storage
RUN make

EXPOSE 3478 3478/udp

VOLUME ["/coturn/storage"]
VOLUME ["/coturn/logs"]
VOLUME ["/certificates"]

RUN chmod 755 /coturn/howzit_coturn/docker/howzit-start.sh

ENTRYPOINT ["/bin/sh", "/coturn/howzit_coturn/docker/howzit-start.sh"]