FROM debian:bullseye

RUN apt-get update && \
    apt-get -y install \
    	wget \
	tar \
	bzip2 \
	build-essential \
	gcc-arm-linux-gnueabihf \
	binutils-arm-linux-gnueabihf

RUN wget https://matt.ucc.asn.au/dropbear/releases/dropbear-2022.82.tar.bz2
RUN tar xvf dropbear-2022.82.tar.bz2

WORKDIR /dropbear-2022.82

ENV CC=arm-linux-gnueabihf-gcc
ENV CFLAGS="-DDROPBEAR_SVR_PASSWORD_AUTH=0"

RUN ./configure --host=arm-linux-gnueabhf --disable-zlib --disable-shadow --disable-syslog --disable-lastlog --enable-static
# RUN cat ./options.h ./default_options.h; false
RUN make PROGRAMS="dropbear scp" MULTI=1

RUN arm-linux-gnueabihf-strip dropbearmulti
