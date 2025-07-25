ARG BUILD_FROM="ghcr.io/hassio-addons/base-python:13.1.3"
FROM $BUILD_FROM

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
ARG CODE_OWNER=Teagan42
ARG XCEL_ITRON2MQTT_SHA=4d4599ead77a14888414195977e2853213a594b7

# Copy python source from upstream
RUN curl -L https://github.com/${CODE_OWNER}/xcel_itron2mqtt/archive/${XCEL_ITRON2MQTT_SHA}.zip -o /tmp/main.zip && \
  cd /tmp && unzip /tmp/main.zip && \
  mv /tmp/xcel_itron2mqtt-${XCEL_ITRON2MQTT_SHA}/xcel_itron2mqtt /opt && \
  rm /opt/xcel_itron2mqtt/run.sh && \ 
  rm -rf /tmp/main.zip && \
  apk del libssl3 libcrypto3 && apk add --no-cache openssl && \
  pip3 install --no-cache-dir \
  --prefer-binary \
  -r /opt/xcel_itron2mqtt/requirements.txt

# Copy root filesystem
COPY rootfs /

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
  org.opencontainers.image.title="${BUILD_NAME}" \
  org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
  org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
  org.opencontainers.image.licenses="MIT" \
  org.opencontainers.image.url="https://addons.community" \
  org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
  org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
  org.opencontainers.image.created=${BUILD_DATE} \
  org.opencontainers.image.revision=${BUILD_REF} \
  org.opencontainers.image.version=${BUILD_VERSION}
