FROM registry.gitlab.com/islandoftex/images/texlive

RUN sed -i 's/deb.debian.org/mirrors.pku.edu.cn/g' /etc/apt/sources.list.d/debian.sources && \
    apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get install -y wget xz-utils openssh-client && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir -p /usr/local/share/fonts/custom

COPY fonts/* /usr/local/share/fonts/custom/
RUN fc-cache -fv

RUN curl -fsSL https://nodejs.org/dist/v24.12.0/node-v24.12.0-linux-x64.tar.xz \
    | tar -xJ -C /usr/local --strip-components=1 \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs

USER texlive

WORKDIR /workspace
