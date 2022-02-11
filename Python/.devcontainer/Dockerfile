FROM nvidia/cuda:11.6.0-devel-ubuntu20.04

RUN echo "Installing apt packages..." \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt -y update --no-install-recommends \
    && apt -y install --no-install-recommends \
    git \
    sudo \
    wget \
    ca-certificates \
    && apt autoremove -y \
    && apt clean -y \
    export DEBIAN_FRONTEND=dialog

ENV MICROMAMBA_VERSION=0.21.1

RUN echo "Installing micromamba ver. ${MICROMAMBA_VERSION}..." \
    && mkdir /opt/micromamba/ \
    && cd /opt/micromamba/ \
    && wget https://micromamba.snakepit.net/api/micromamba/linux-64/${MICROMAMBA_VERSION} \
    && tar -xf ./${MICROMAMBA_VERSION}

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USERNAME=tensorush

RUN echo "Creating user ${USERNAME}..." \
    && groupadd -g ${GROUP_ID} ${USERNAME} \
    && useradd -u ${USER_ID} -g ${GROUP_ID} -s /usr/bin/bash -m ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

USER ${USERNAME}

RUN echo "Setting micromamba environment..." \
    && /opt/micromamba/bin/micromamba shell init -s bash -p ${HOME}/micromamba/

COPY ./environment.yaml ./

ENV MAMBA_ROOT_PREFIX=${HOME}/micromamba
ENV MAMBA_EXE=/opt/micromamba/bin/micromamba

RUN echo "Installing micromamba packages..." \
    && micromamba install -yn base -f ./environment.yaml \
    && micromamba clean -ya \
    && rm ./environment.yaml
