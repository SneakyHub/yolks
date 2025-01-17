FROM openjdk:9-jdk-slim

LABEL author="Sneaky" maintainer="sneaky@sneakyhub.com"
LABEL org.opencontainers.image.source="https://github.com/sneakyhub/yolks"
LABEL org.opencontainers.image.licenses=MIT

RUN apt update -y \
    && apt install -y \
        curl \
        lsof \
        ca-certificates \
        openssl \
        git \
        tar \
        sqlite3 \
        fontconfig \
        tzdata \
        iproute2 \
        libfreetype6 \
        tini \
        zip \
        unzip \
    && apt clean \
    && rm -rf /var/lib/apt/lists/*

## Setup user and working directory
RUN useradd -m -d /home/container -s /bin/bash container
USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

STOPSIGNAL SIGINT

COPY --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/usr/bin/tini", "-g", "--"]
CMD ["/entrypoint.sh"]
