FROM alpine:latest
# RegRipper created by Harlan Carvey (github.com/keydet89)
# Perl cpanm lines from ytnobody (github.com/ytnobody)
# this Dockerfile by Bonifield (github.com/bonifield)

ENV RR=/usr/share/rr

RUN apk add --update \
	bash make perl perl-dev wget curl tar zip \
	&& rm -rf /var/cache/apk/*

RUN curl -L http://xrl.us/cpanm > /bin/cpanm && chmod +x /bin/cpanm
RUN cpanm App::cpm

WORKDIR /usr

RUN cpm install Plack
ENV PERL5LIB=/usr/local/lib/perl5
ENV PATH=/usr/local/bin:$PATH

RUN mkdir -p $RR

WORKDIR $RR
RUN wget https://cpan.metacpan.org/authors/id/J/JM/JMACFARLA/Parse-Win32Registry-1.0.tar.gz \
	&& wget https://github.com/keydet89/RegRipper2.8/archive/master.zip \
	&& tar -xzf Parse-Win32Registry-1.0.tar.gz \
	&& unzip master.zip

WORKDIR $RR/Parse-Win32Registry-1.0
RUN perl Makefile.PL \
	&& make \
	&& make install

WORKDIR $RR/RegRipper2.8-master

RUN sed -i 's/catfile("plugins")/catfile("\/usr\/share\/rr\/RegRipper2.8-master\/plugins")/g' rip.pl \
	&& sed -i 's/c:\\perl\\bin\\perl\.exe/\/usr\/bin\/perl/g' rip.pl \
	&& sed -i 's/c:\\perl\\bin\\perl\.exe/\/usr\/bin\/perl/g' rr.pl \
	&& chmod +x rip.pl \
	&& chmod +x rr.pl

WORKDIR $RR

RUN addgroup -S rr \
	&& adduser -S rr -G rr \
	&& chown -R rr:rr $RR

RUN find / -perm /6000 -type f -exec chmod a-s {} \; || true

WORKDIR /home/rr
VOLUME /home/rr

USER rr

ENTRYPOINT ["/usr/share/rr/RegRipper2.8-master/rip.pl"]

# comment out ENTRYPOINT then uncomment below to make interactive with docker exec
#COPY sleepy.sh /usr/bin/
#CMD ["/bin/bash", "/usr/bin/sleepy.sh"]
