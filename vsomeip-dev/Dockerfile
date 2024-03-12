# Builder
FROM ubuntu:22.04

# Install dependencies
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y \
	git \
	libboost-system-dev \
	libboost-thread-dev \
	libboost-filesystem-dev \
	build-essential \
	cmake

# Build vsomeip
WORKDIR /root
RUN git clone --branch 3.4.10 https://github.com/COVESA/vsomeip.git vsomeip \
	&& mkdir -p vsomeip/build \
	&& cmake -S vsomeip -B vsomeip/build -DENABLE_SIGNAL_HANDLING=1 \
	&& cd vsomeip/build \
	&& make && make install