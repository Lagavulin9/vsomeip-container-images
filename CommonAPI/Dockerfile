# Develop Environment
FROM lagavulin16/commonapi:dev as builder

# Base Image
FROM lagavulin16/vsomeip AS baseImage

# Install runtime libraries
RUN apt update && apt install -y \
	openjdk-11-jre

# Copy CommonAPI libraries
COPY --from=builder /usr/local/lib /usr/local/lib
COPY --from=builder /usr/local/include /usr/local/include