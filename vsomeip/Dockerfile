# Develop Environment
FROM lagavulin16/vsomeip-dev AS builder

# Base Image
FROM ubuntu:22.04 AS baseImage

RUN apt update && apt install -y \
	libboost-system-dev \
	libboost-thread-dev \
	libboost-filesystem-dev

# Copy vsomeip libraries
COPY --from=builder /usr/local/lib /usr/local/lib
COPY --from=builder /usr/local/include /usr/local/include