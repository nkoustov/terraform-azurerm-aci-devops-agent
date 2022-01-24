FROM ubuntu:18.04

# To make it easier for build and release pipelines to run apt-get,
# configure apt to not require confirmation (assume the -y argument by default)
ENV DEBIAN_FRONTEND=noninteractive
RUN mkdir -p /etc/apt/apt.conf.d
RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes
RUN cat /etc/os-release

RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository -y "deb http://security.ubuntu.com/ubuntu xenial-security main" 
RUN apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        jq \
        git \
        iputils-ping \
        libcurl4 \
        libicu55 \
        libunwind8 \
        netcat

RUN apt-get install openjdk-11-jdk \
        maven

ENV JAVA_HOME_11_X64 /usr/lib/jvm/java-11-openjdk-amd64/

WORKDIR /azp

COPY ./start.sh .
RUN chmod +x start.sh

CMD ["./start.sh"]