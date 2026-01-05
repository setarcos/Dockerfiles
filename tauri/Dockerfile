FROM debian:trixie-slim

ARG NODE_VERSION=22.16.0

RUN sed -i 's/deb.debian.org/mirrors.pku.edu.cn/g' /etc/apt/sources.list.d/debian.sources && \
    apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get install -y --no-install-recommends ca-certificates curl wget git build-essential \
            libpq-dev openssh-client pkg-config \
            cmake unzip zip xz-utils llvm clang xdg-utils file \
            libgtk-3-dev libayatana-appindicator3-dev libwebkit2gtk-4.1-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    groupadd -g 1000 builduser && \
    useradd -u 1000 -g builduser builduser && \
    mkdir /home/builduser && \
    chown 1000:1000 /home/builduser

ENV RUSTUP_HOME=/usr/local/rustup \
    CARGO_HOME=/usr/local/cargo \
    PATH=/usr/local/cargo/bin:$PATH \
    CARGO_NET_GIT_FETCH_WITH_CLI=true

# Rustup automatically detects the architecture, so no changes needed here.
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | \
    sh -s -- -y --default-toolchain stable --profile minimal && \
    chmod -R a+w $RUSTUP_HOME $CARGO_HOME

# 2. Dynamic Node.js installation based on Architecture and Version ARG
RUN ARCH= && \
    # Detect Debian architecture (amd64 or arm64)
    dpkgArch="$(dpkg --print-architecture)" && \
    case "${dpkgArch##*-}" in \
      amd64) ARCH='x64';; \
      arm64) ARCH='arm64';; \
      *) echo "unsupported architecture"; exit 1 ;; \
    esac && \
    echo "Downloading Node ${NODE_VERSION} for ${ARCH}..." && \
    curl -fsSL "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-${ARCH}.tar.xz" \
    | tar -xJ -C /usr/local --strip-components=1 \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs

WORKDIR /build
USER builduser

CMD ["/bin/bash"]
