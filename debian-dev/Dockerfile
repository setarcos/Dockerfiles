FROM debian:trixie-slim

RUN sed -i 's/deb.debian.org/mirrors.pku.edu.cn/g' /etc/apt/sources.list.d/debian.sources && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends ca-certificates curl wget git build-essential \
            libpq-dev openssh-client pkg-config && \
    apt-get install -y libssl-dev flex bison libncurses5-dev cmake file cpio bc unzip rsync && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    groupadd -g 1000 builduser && \
    useradd -u 1000 -g builduser builduser

WORKDIR /build

USER builduser

CMD ["/bin/bash"]
