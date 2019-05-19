FROM ubuntu:16.04

RUN apt-get update -q && apt-get upgrade -y \
	&& apt-get install -qy wget bison cmake flex g++ gdb make libmagic-dev libpcap-dev libgeoip-dev python-dev swig gawk libncurses5-dev zlib1g-dev libssl-dev git --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/* \
	&& mkdir -p /root/bro/ \
	&& cd /root/bro/ \
	&& wget https://www.zeek.org/downloads/bro-2.6.1.tar.gz --no-check-certificate \
	&& tar -xzf bro-2.6.1.tar.gz

RUN cd bro-2.6.1 \
	&& ./configure \
	&& make \
	&& make install

COPY local.bro /usr/local/bro/share/bro/site/

RUN export PATH=$PATH:/usr/local/bro/bin \
	&& /usr/local/bro/bin/broctl deploy \
	&& /usr/local/bro/bin/broctl status \
	&& /usr/local/bro/bin/broctl stop \
	&& find / -perm /6000 -type f -exec chmod a-s {} \; || true

WORKDIR /usr/local/bro/logs/current
VOLUME /usr/local/bro/logs/current

ENTRYPOINT ["/usr/local/bro/bin/bro", "-C", "-r"]
