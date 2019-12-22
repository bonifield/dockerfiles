FROM ubuntu:16.04
LABEL build_date="2019-01-17"
LABEL name="Laika BOSS Object Scanning System"
LABEL description="Laika BOSS dissects files and provides results in JSON format."

#=============
# Laika BOSS
# docker run --rm -v ~:/lb laikaboss [your-file-to-analyze] | jq -C . | less -r
# - derived from LMCO's install notes and Dockerfile located at https://github.com/lmco/laikaboss
#=============

ENV WORKY=/home/workerbee

RUN apt-get update -q && apt-get install -qy git yara python-yara python-progressbar python-pip \
	&& mkdir -p $WORKY/workdir

RUN pip install --upgrade pip

RUN pip install --upgrade setuptools \
	&& pip install interruptingcow

RUN echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.conf \
	&& echo "net.ipv6.conf.default.disable_ipv6 = 1" >> /etc/sysctl.conf \
	&& echo "net.ipv6.conf.lo.disable_ipv6 = 1" >> /etc/sysctl.conf

RUN apt-get install -qy libzmq3-dev python-zmq python-gevent python-pexpect
RUN apt-get install -qy python-ipy python-m2crypto python-pyclamd liblzma5 libimage-exiftool-perl python-msgpack libfuzzy-dev python-cffi python-dev unrar
RUN apt-get install -qy libssl-dev libtool 

RUN apt-get install -qy wget tar zip unzip

RUN pip install fluent-logger future interruptingcow javatools msgpack-python olefile pylzma py-unrar2 ssdeep

WORKDIR $WORKY
RUN wget https://github.com/smarnach/pyexiftool/archive/master.zip
RUN unzip master.zip
WORKDIR $WORKY/pyexiftool-master
RUN python setup.py build
RUN python setup.py install

WORKDIR $WORKY
RUN wget https://github.com/erocarrera/pefile/archive/pefile-1.2.10-139.tar.gz
RUN tar vxzf pefile-1.2.10-139.tar.gz
WORKDIR $WORKY/pefile-pefile-1.2.10-139
# the setup file chokes on the value of version
RUN sed -i "s/\__version__.*$/\__version__ = '12345'/g" pefile.py
RUN python setup.py build
RUN python setup.py install

# make a non-root user
RUN groupadd -r workerbee && \
	useradd -r -g workerbee -d $WORKY -s /sbin/nologin -c "non-root user" workerbee && \
	chown -R workerbee:workerbee $WORKY
USER workerbee
WORKDIR $WORKY
RUN git clone https://github.com/lmco/laikaboss.git

# install as root
USER root
WORKDIR $WORKY/laikaboss
RUN python setup.py build
RUN python setup.py install

RUN wget -O /usr/local/bin/jq "https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64" && \
	chmod 755 /usr/local/bin/jq

WORKDIR $WORKY
RUN rm -rf master.zip pefile-1.2.10-139.tar.gz pefile-pefile-1.2.10-139 pyexiftool-master
RUN ldconfig && \
	apt-get remove -y --purge automake build-essential libtool && \
	apt-get autoremove -y --purge && \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/*

RUN mkdir -p /lb && \
	chown -R workerbee:workerbee /lb

RUN find / -perm /6000 -type f -exec chmod a-s {} \; || true

USER workerbee
ENV HOME /home/workerbee
ENV USER workerbee

WORKDIR /lb

ENTRYPOINT ["/usr/local/bin/laika.py"]

# docker run --rm -v ~:/lb laikaboss [your-file-to-analyze]
# docker run --rm -v ~:/lb laikaboss [your-file-to-analyze] | jq -C . | less -r

#################################################

# comment out ENTRYPOINT then uncomment below to make interactive with docker exec for testing and poking around (remember to not use --rm if intending to save the container after testing)
# COPY sleepy.sh /usr/bin/
# CMD ["/bin/bash", "/usr/bin/sleepy.sh"]

# for manual testing with sleepy running to keep the container alive
# docker run --rm -v $PWD:/lb -d laikaboss && docker exec -it `docker ps | grep laikaboss | cut -d ' ' -f 1` /bin/bash && docker stop `docker ps | grep laikaboss | cut -d ' ' -f 1`
