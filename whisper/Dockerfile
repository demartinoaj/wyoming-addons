# grab whatever ubutu Nvida DEVEL base image from the link
# https://hub.docker.com/r/nvidia/cuda/tags#!
FROM nvidia/cuda:12.4.1-devel-ubuntu22.04

# Install Whisper
WORKDIR /usr/src
ARG WYOMING_WHISPER_VERSION='2.1.0'

# Make sure we install libcudnn8 too
RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        python3 \
        python3-dev \
        python3-pip \
        libcudnn8 \
        libcudnn8-dev \
    \
    && pip3 install --no-cache-dir -U \
        setuptools \
        wheel \
    && pip3 install --no-cache-dir \
        --extra-index-url https://www.piwheels.org/simple \
        "wyoming-faster-whisper @ https://github.com/rhasspy/wyoming-faster-whisper/archive/refs/tags/v${WYOMING_WHISPER_VERSION}.tar.gz" \
    \
    && apt-get purge -y --auto-remove \
        build-essential \
        python3-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /
COPY run.sh ./

EXPOSE 10300

ENTRYPOINT ["bash", "/run.sh"]
