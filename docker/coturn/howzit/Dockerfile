FROM debian:11

RUN apt-get update
RUN apt-get install -y --no-install-recommends --no-install-suggests \
    ca-certificates cmake g++ git make autoconf coreutils libtool pkg-config \
    libevent-dev libssl-dev libsqlite3-dev libmicrohttpd-dev
RUN update-ca-certificates

RUN mkdir -p /coturn/storage
WORKDIR /coturn
RUN git clone https://github.com/HazimMohamed/howzit_coturn.git
WORKDIR /coturn/howzit_coturn

RUN ./configure --turndbdir=/coturn/storage
RUN make

EXPOSE 3478 3478/udp

VOLUME ["/coturn/storage"]

ENTRYPOINT ["/coturn/docker/howzit-start.sh"]