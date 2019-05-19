FROM alpine:latest
# evtxdump.pl from Andreas Schuster at http://computer.forensikblog.de/files/evtx/EvtxParser-current.zip (twitter.com/forensikblog)
# Perl cpanm lines from ytnobody (github.com/ytnobody)
# this Dockerfile by Bonifield (github.com/bonifield)

ENV ED=/usr/share/ed

RUN apk add --update \
	bash make perl perl-dev wget curl tar zip perl-app-cpanminus gcc libc-dev binutils \
	&& rm -rf /var/cache/apk/*

RUN cpanm App::cpm

WORKDIR /usr

RUN cpm install Plack
ENV PERL5LIB=/usr/local/lib/perl5
ENV PATH=/usr/local/bin:$PATH

RUN mkdir -p $ED

WORKDIR $ED
RUN wget http://computer.forensikblog.de/files/evtx/EvtxParser-current.zip \
	&& unzip EvtxParser-current.zip

WORKDIR $ED/Parse-Evtx-1.1.1
RUN perl Makefile.PL \
	&& make \
	&& make install

#=============
# long series of Perl modules
#=============

ENV DL=/downloads

RUN mkdir $DL
WORKDIR $DL

# wgets
RUN wget https://cpan.metacpan.org/authors/id/N/NE/NEILB/Carp-Assert-0.21.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/D/DR/DROLSKY/DateTime-1.51.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/E/ET/ETHER/namespace-autoclean-0.28.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/E/ET/ETHER/B-Hooks-EndOfScope-0.24.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/D/DR/DROLSKY/Module-Implementation-0.09.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/F/FR/FREW/Sub-Exporter-Progressive-0.001013.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/V/VP/VPIT/Variable-Magic-0.62.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/Z/ZE/ZEFRAM/Module-Runtime-0.016.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/R/RI/RIBASUSHI/namespace-clean-0.27.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/E/ET/ETHER/Package-Stash-0.38.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/D/DR/DROLSKY/Specio-0.42.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/D/DR/DROLSKY/Devel-StackTrace-2.03.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/D/DO/DOY/Eval-Closure-0.14.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/R/RJ/RJBS/Test-Fatal-0.014.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/H/HA/HAARG/MRO-Compat-0.13.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/H/HA/HAARG/Role-Tiny-2.000006.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/R/RG/RGARCIA/Sub-Identify-0.14.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/D/DR/DROLSKY/Params-ValidationCompiler-0.30.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/D/DR/DROLSKY/Exception-Class-1.44.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/T/TM/TMTM/Class-Data-Inheritable-0.08.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/D/DR/DROLSKY/DateTime-Locale-1.22.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/R/RE/REHSACK/File-ShareDir-1.116.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/P/PE/PEVANS/Scalar-List-Utils-1.50.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/D/DO/DOY/Dist-CheckConflicts-0.11.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/E/ET/ETHER/File-ShareDir-Install-0.13.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/D/DR/DROLSKY/DateTime-TimeZone-2.19.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/S/SH/SHAY/Class-Singleton-1.5.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/O/OL/OLIMAUL/Digest-CRC-0.22.2.tar.gz \
	&& wget https://cpan.metacpan.org/authors/id/J/JV/JV/Data-Hexify-1.00.tar.gz

# tar extracts
RUN tar -xzf Carp-Assert-0.21.tar.gz \
	&& tar -xzf DateTime-1.51.tar.gz \
	&& tar -xzf namespace-autoclean-0.28.tar.gz \
	&& tar -xzf B-Hooks-EndOfScope-0.24.tar.gz \
	&& tar -xzf Module-Implementation-0.09.tar.gz \
	&& tar -xzf Sub-Exporter-Progressive-0.001013.tar.gz \
	&& tar -xzf Variable-Magic-0.62.tar.gz \
	&& tar -xzf Module-Runtime-0.016.tar.gz \
	&& tar -xzf namespace-clean-0.27.tar.gz \
        && tar -xzf Package-Stash-0.38.tar.gz \
	&& tar -xzf Specio-0.42.tar.gz \
	&& tar -xzf Devel-StackTrace-2.03.tar.gz \
	&& tar -xzf Eval-Closure-0.14.tar.gz \
	&& tar -xzf Test-Fatal-0.014.tar.gz \
        && tar -xzf MRO-Compat-0.13.tar.gz \
        && tar -xzf Role-Tiny-2.000006.tar.gz \
        && tar -xzf Sub-Identify-0.14.tar.gz \
	&& tar -xzf Params-ValidationCompiler-0.30.tar.gz \
	&& tar -xzf Exception-Class-1.44.tar.gz \
	&& tar -xzf Class-Data-Inheritable-0.08.tar.gz \
	&& tar -xzf DateTime-Locale-1.22.tar.gz \
	&& tar -xzf File-ShareDir-1.116.tar.gz \
	&& tar -xzf Scalar-List-Utils-1.50.tar.gz \
	&& tar -xzf Dist-CheckConflicts-0.11.tar.gz \
	&& tar -xzf File-ShareDir-Install-0.13.tar.gz \
        && tar -xzf DateTime-TimeZone-2.19.tar.gz \
	&& tar -xzf Class-Singleton-1.5.tar.gz \
	&& tar -xzf Digest-CRC-0.22.2.tar.gz \
	&& tar -xzf Data-Hexify-1.00.tar.gz

# module installs
WORKDIR $DL/Carp-Assert-0.21
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/DateTime-1.51
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/namespace-autoclean-0.28
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/B-Hooks-EndOfScope-0.24
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/Module-Implementation-0.09
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/Sub-Exporter-Progressive-0.001013
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/Variable-Magic-0.62
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/Module-Runtime-0.016
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/namespace-clean-0.27
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/Package-Stash-0.38
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/Specio-0.42
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/Devel-StackTrace-2.03
RUN perl Makefile.PL \   
        && make \
        && make install
WORKDIR $DL/Eval-Closure-0.14
RUN perl Makefile.PL \   
        && make \
        && make install
WORKDIR $DL/Test-Fatal-0.014
RUN perl Makefile.PL \   
        && make \
        && make install
WORKDIR $DL/MRO-Compat-0.13
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/Role-Tiny-2.000006
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/Sub-Identify-0.14
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/Params-ValidationCompiler-0.30
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/Exception-Class-1.44
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/Class-Data-Inheritable-0.08
RUN perl Makefile.PL \
	&& make \
	&& make install
WORKDIR $DL/DateTime-Locale-1.22
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/File-ShareDir-Install-0.13
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/Scalar-List-Utils-1.50
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/Dist-CheckConflicts-0.11
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/File-ShareDir-1.116
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/DateTime-TimeZone-2.19
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/Class-Singleton-1.5
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/Digest-CRC-0.22
RUN perl Makefile.PL \
        && make \
        && make install
WORKDIR $DL/Data-Hexify-1.00
RUN perl Makefile.PL \
        && make \
        && make install

# cleanup
WORKDIR $DL
RUN rm Carp-Assert-0.21.tar.gz \
	&& rm -rf Carp-Assert-0.21 \
	&& rm DateTime-1.51.tar.gz \
	&& rm -rf DateTime-1.51 \
	&& rm namespace-autoclean-0.28.tar.gz \
	&& rm -rf namespace-autoclean-0.28 \
	&& rm B-Hooks-EndOfScope-0.24.tar.gz \
	&& rm -rf B-Hooks-EndOfScope-0.24 \
	&& rm Module-Implementation-0.09.tar.gz \
	&& rm -rf Module-Implementation-0.09 \
	&& rm Sub-Exporter-Progressive-0.001013.tar.gz \
	&& rm -rf Sub-Exporter-Progressive-0.001013 \
	&& rm Variable-Magic-0.62.tar.gz \
	&& rm -rf Variable-Magic-0.62.tar.gz \
	&& rm Module-Runtime-0.016.tar.gz \
	&& rm -rf Module-Runtime-0.016 \
	&& rm namespace-clean-0.27.tar.gz \
	&& rm -rf namespace-clean-0.27 \
	&& rm Package-Stash-0.38.tar.gz  \
        && rm -rf Package-Stash-0.38 \
	&& rm Specio-0.42.tar.gz \
	&& rm -rf Specio-0.42.tar.gz \
	&& rm Devel-StackTrace-2.03.tar.gz \
	&& rm -rf Devel-StackTrace-2.03 \
	&& rm Eval-Closure-0.14.tar.gz \
	&& rm -rf Eval-Closure-0.14 \
	&& rm Test-Fatal-0.014.tar.gz \
	&& rm -rf Test-Fatal-0.014 \
	&& rm MRO-Compat-0.13.tar.gz \
        && rm -rf MRO-Compat-0.13 \
	&& rm Role-Tiny-2.000006.tar.gz \
        && rm -rf Role-Tiny-2.000006 \
	&& rm Sub-Identify-0.14.tar.gz \
        && rm -rf Sub-Identify-0.14 \
	&& rm Params-ValidationCompiler-0.30.tar.gz \
	&& rm -rf Params-ValidationCompiler-0.30 \
	&& rm Exception-Class-1.44.tar.gz \
	&& rm -rf Exception-Class-1.44 \
	&& rm Class-Data-Inheritable-0.08.tar.gz \
	&& rm -rf Class-Data-Inheritable-0.08 \
	&& rm DateTime-Locale-1.22.tar.gz \
	&& rm -rf DateTime-Locale-1.22 \
	&& rm File-ShareDir-1.116.tar.gz \
	&& rm -rf File-ShareDir-1.116 \
	&& rm Scalar-List-Utils-1.50.tar.gz \
	&& rm -rf Scalar-List-Utils-1.50 \
	&& rm Dist-CheckConflicts-0.11.tar.gz \
	&& rm -rf Dist-CheckConflicts-0.11 \
	&& rm File-ShareDir-Install-0.13.tar.gz \
	&& rm -rf File-ShareDir-Install-0.13 \
	&& rm DateTime-TimeZone-2.19.tar.gz \
        && rm -rf DateTime-TimeZone-2.19 \
	&& rm Class-Singleton-1.5.tar.gz \
	&& rm -rf Class-Singleton-1.5 \
	&& rm Digest-CRC-0.22.2.tar.gz \
	&& rm -rf Digest-CRC-0.22 \
	&& rm Data-Hexify-1.00.tar.gz \
	&& rm -rf Data-Hexify-1.00

#=============

RUN addgroup -S ed \
	&& adduser -S ed -G ed \
	&& chown -R ed:ed $ED

RUN find / -perm /6000 -type f -exec chmod a-s {} \; || true

WORKDIR /home/ed
VOLUME /home/ed

USER ed

ENTRYPOINT ["/usr/bin/perl", "/usr/local/bin/evtxdump.pl"]

# comment out ENTRYPOINT then uncomment below to make interactive with docker exec
#COPY sleepy.sh /usr/bin/
#USER ed
#CMD ["/bin/bash", "/usr/bin/sleepy.sh"]

# testing with sleepy to keep the container alive:
# docker build -t evtxdump .
# docker run --rm -v $PWD:/home/ed -d evtxdump && docker exec -it `docker ps | grep evtxdump | cut -d ' ' -f 1` /bin/bash && docker stop `docker ps | grep evtxdump | cut -d ' ' -f 1`
