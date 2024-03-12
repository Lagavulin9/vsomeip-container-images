# Builder
FROM ubuntu:22.04 AS builder

ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y \
	git \
	libboost-system-dev \
	libboost-thread-dev \
	libboost-filesystem-dev \
	build-essential \
	cmake

# vSomeIP
WORKDIR /root
RUN git clone --branch 3.4.10 https://github.com/COVESA/vsomeip.git vsomeip \
	&& mkdir -p vsomeip/build \
	&& cmake -S vsomeip -B vsomeip/build -DENABLE_SIGNAL_HANDLING=1 \
	&& cd vsomeip/build \
	&& make && make install

# Base Image
FROM ubuntu:22.04 AS baseImage

RUN apt update && apt install -y \
	libboost-system-dev \
	libboost-thread-dev \
	libboost-filesystem-dev

COPY --from=builder /usr/local/lib /usr/local/lib
COPY --from=builder /usr/local/include /usr/local/include