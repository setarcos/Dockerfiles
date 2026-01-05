FROM debian:trixie-slim

RUN sed -i 's/deb.debian.org/mirrors.pku.edu.cn/g' /etc/apt/sources.list.d/debian.sources && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y build-essential qt6-base-dev qt6-tools-dev qt6-serialport-dev qt6-webengine-dev qt6-5compat-dev cmake && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    groupadd -g 1000 builduser && \
    useradd -u 1000 -g builduser builduser

WORKDIR /build
ENV PATH=/usr/lib/qt6/bin:$PATH
USER builduser

CMD ["/bin/bash"]
