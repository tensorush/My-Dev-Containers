FROM ubuntu:20.04
# FROM nvidia/cuda:11.6.0-devel-ubuntu20.04

RUN echo "Installing apt packages..." \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt -y update --no-install-recommends \
    && apt -y install --no-install-recommends \
    git \
    fish \
    sudo \
    python3-dev \
    python3-pip \
    python3-setuptools \
    && apt autoremove -y \
    && apt clean -y \
    export DEBIAN_FRONTEND=dialog

ENV MICROMAMBA_VERSION=0.21.0

RUN echo "Installing micromamba ver. ${MICROMAMBA_VERSION}..." \
    && cd opt \
    && wget https://micromamba.snakepit.net/api/micromamba/linux-64/${MICROMAMBA_VERSION} \
    && tar -xj ./micromamba-${MICROMAMBA_VERSION}*.tar \
    && rm ./micromamba-${MICROMAMBA_VERSION}*.tar \
    && ln -s ./micromamba/micromamba /usr/local/bin/micromamba

COPY ./environment.yaml ./

RUN echo "Installing micromamba packages..." \
    && micromamba env update -n base -f ./environment.yaml \
    && micromamba clean -ya \
    && rm ./environment.yaml

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USERNAME=tensorush

RUN echo "Creating user ${USERNAME}..." \
    && groupadd -g ${GROUP_ID} ${USERNAME} \
    && useradd -u ${USER_ID} -g ${GROUP_ID} -s /usr/bin/fish ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

USER ${USERNAME}
