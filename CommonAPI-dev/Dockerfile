# Builder
FROM lagavulin16/vsomeip-dev AS builder

# Install dependencies
RUN apt install -y \
	wget \
	unzip \
	openjdk-11-jre

WORKDIR /root

# CommonAPI
RUN git clone --branch 3.2.0 https://github.com/COVESA/capicxx-core-runtime.git capicxx-core-runtime \
	&& mkdir -p capicxx-core-runtime/build \
	&& cmake -S capicxx-core-runtime -B capicxx-core-runtime/build \
	&& cd capicxx-core-runtime/build \
	&& make && make install

# CommonAPI-SomeIP
RUN git clone --branch 3.2.0 https://github.com/COVESA/capicxx-someip-runtime.git capicxx-someip-runtime \
	&& mkdir -p capicxx-someip-runtime/build \
	&& cmake -S capicxx-someip-runtime -B capicxx-someip-runtime/build \
	&& cd capicxx-someip-runtime/build \
	&& make && make install

# Generator
RUN wget https://github.com/COVESA/capicxx-core-tools/releases/download/3.2.0.1/commonapi_core_generator.zip \
	&& unzip commonapi_core_generator.zip -d core-generator \
	&& wget https://github.com/COVESA/capicxx-someip-tools/releases/download/3.2.0.1/commonapi_someip_generator.zip \
	&& unzip commonapi_someip_generator.zip -d someip-generator \
	&& ln -s /root/core-generator/commonapi-core-generator-linux-x86_64 /usr/local/bin/core-generator \
	&& ln -s /root/someip-generator/commonapi-someip-generator-linux-x86_64 /usr/local/bin/someip-generator \
	&& rm -rf commonapi_core_generator.zip commonapi_someip_generator.zip

COPY ./conf/commonapi.ini /etc/commonapi.ini