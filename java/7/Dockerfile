# Use the official OpenJDK 7 base image
FROM openjdk:7-jdk

LABEL author="Sneaky" maintainer="sneaky@sneakyhub.com"
LABEL org.opencontainers.image.source="https://github.com/sneakyhub/yolks"
LABEL org.opencontainers.image.licenses=MIT

# Update and install required packages
RUN apt-get update -y \
    && apt-get install -y \
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
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set up user and working directory
RUN useradd -m -d /home/container -s /bin/bash container
USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

# Signal handling
STOPSIGNAL SIGINT

# Copy the entrypoint script
COPY --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# Define entrypoint and command
ENTRYPOINT ["/usr/bin/tini", "-g", "--"]
CMD ["/entrypoint.sh"]
