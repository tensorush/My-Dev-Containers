FROM nvidia/cuda:11.6.0-devel-ubuntu20.04

RUN echo "Installing apt packages..." \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt -y update --no-install-recommends \
    && apt -y install --no-install-recommends \
    git \
    zsh \
    curl \
    sudo \
    ca-certificates \
    && apt autoremove -y \
    && apt clean -y \
    export DEBIAN_FRONTEND=dialog

ENV MICROMAMBA_VERSION=0.21.1
ENV MICROMAMBA_DIR_PATH=/opt/micromamba/

RUN echo "Installing micromamba ver. ${MICROMAMBA_VERSION}..." \
    && mkdir ${MICROMAMBA_DIR_PATH} \
    && curl -L -o ${MICROMAMBA_DIR_PATH}${MICROMAMBA_VERSION} https://micromamba.snakepit.net/api/micromamba/linux-64/${MICROMAMBA_VERSION} \
    && tar -xf ${MICROMAMBA_DIR_PATH}${MICROMAMBA_VERSION} -C ${MICROMAMBA_DIR_PATH} \
    && rm ${MICROMAMBA_DIR_PATH}${MICROMAMBA_VERSION}

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USER_NAME=tensorush

RUN echo "Creating user ${USER_NAME}..." \
    && groupadd -g ${GROUP_ID} ${USER_NAME} \
    && useradd -u ${USER_ID} -g ${GROUP_ID} -s /usr/bin/zsh -m ${USER_NAME} \
    && echo "${USER_NAME} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/${USER_NAME} \
    && chmod 0440 /etc/sudoers.d/${USER_NAME}

USER ${USER_NAME}

RUN echo "Enabling micromamba for current user..." \
    && ${MICROMAMBA_DIR_PATH}bin/micromamba shell init -s zsh -p ${HOME}/micromamba/

# Run these commands upon container start-up to install micromamba environment
# micromamba install -yn base -f ./.devcontainer/environment.yaml \
#     && micromamba clean -ya \
#     && micromamba activate base
