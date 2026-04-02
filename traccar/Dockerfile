ARG BUILD_FROM=ghcr.io/hassio-addons/base:19.0.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Copy root filesystem
COPY rootfs /

# Fix permissions on all scripts
RUN find /etc/cont-init.d /etc/services.d -type f | xargs chmod a+x

# Set working dir
WORKDIR /opt/traccar

# Setup base
ARG TRACCAR_VERSION="v6.9.1"
RUN \
    apk add --no-cache \
        mariadb-client \
        nginx \
        nss \
        openjdk17-jre-headless \
        xmlstarlet \
        unzip \
    \
    && curl -J -L -o /tmp/traccar.zip \
      "https://github.com/traccar/traccar/releases/download/${TRACCAR_VERSION}/traccar-other-${TRACCAR_VERSION#v}.zip" \
    \
    && mkdir -p /opt/traccar \
    && unzip -d /opt/traccar /tmp/traccar.zip \
    \
    && rm -fr /tmp/*

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="kolodg@gmail.com" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.authors="kolodg@gmail.com" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
