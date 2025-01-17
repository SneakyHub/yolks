FROM debian:stretch-slim

LABEL author="Sneaky" maintainer="sneaky@sneakyhub.com"
LABEL org.opencontainers.image.source="https://github.com/sneakyhub/yolks"
LABEL org.opencontainers.image.licenses=MIT

# Install necessary dependencies
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
        wget \
    && apt clean \
    && rm -rf /var/lib/apt/lists/*

# Install Java 9 (from the OpenJDK 9 archive)
RUN wget -q --no-check-certificate https://download.java.net/openjdk/jdk9/archive/9.0.4+11/binaries/openjdk-9.0.4_linux-x64_bin.tar.gz \
    && tar -xzf openjdk-9.0.4_linux-x64_bin.tar.gz -C /opt \
    && rm openjdk-9.0.4_linux-x64_bin.tar.gz \
    && update-alternatives --install /usr/bin/java java /opt/jdk-9.0.4/bin/java 1 \
    && update-alternatives --install /usr/bin/javac javac /opt/jdk-9.0.4/bin/javac 1 \
    && update-alternatives --set java /opt/jdk-9.0.4/bin/java \
    && update-alternatives --set javac /opt/jdk-9.0.4/bin/javac

# Setup user and working directory
RUN useradd -m -d /home/container -s /bin/bash container
USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

STOPSIGNAL SIGINT

COPY --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/usr/bin/tini", "-g", "--"]
CMD ["/entrypoint.sh"]
