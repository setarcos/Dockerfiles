FROM debian:trixie-slim

RUN sed -i 's/deb.debian.org/mirrors.pku.edu.cn/g' /etc/apt/sources.list.d/debian.sources && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y build-essential qtbase5-dev qtbase5-dev-tools libqt5serialport5-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    groupadd -g 1000 builduser && \
    useradd -u 1000 -g builduser builduser

WORKDIR /build

USER builduser

CMD ["/bin/bash"]
