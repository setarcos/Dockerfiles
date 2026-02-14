FROM debian:trixie-slim

ARG USERNAME=builduser
ARG USER_UID=1000
ARG USER_GID=1000

RUN sed -i 's/deb.debian.org/mirrors.pku.edu.cn/g' /etc/apt/sources.list.d/debian.sources && \
    apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get install -y --no-install-recommends ca-certificates curl wget git build-essential \
            libpq-dev openssh-client pkg-config && \
    apt-get clean && \
    groupadd -g ${USER_GID} ${USERNAME} && \
    useradd -u ${USER_UID} -g ${USERNAME} ${USERNAME} && \
    mkdir /home/${USERNAME} && chown ${USER_UID}:${USER_GID} /home/${USERNAME} && \
    rm -rf /var/lib/apt/lists/*

ENV RUSTUP_HOME=/usr/local/rustup \
    CARGO_HOME=/usr/local/cargo \
    PATH=/usr/local/cargo/bin:$PATH

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | \
    sh -s -- -y --default-toolchain stable --profile minimal && \
    chmod -R a+w $RUSTUP_HOME $CARGO_HOME

RUN curl -fsSL https://nodejs.org/dist/v24.13.1/node-v24.13.1-linux-x64.tar.xz \
    | tar -xJ -C /usr/local --strip-components=1 \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs

USER ${USERNAME}

WORKDIR /workspace
