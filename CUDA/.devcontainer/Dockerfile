FROM nvidia/cuda:11.6.0-devel-ubuntu20.04

ARG USER_UID=1000
ARG USERNAME=tensorush
ARG USER_GID=${USER_UID}

ENV DEBIAN_FRONTEND=noninteractive

RUN echo "Installing packages..." \
    && apt -y update --no-install-recommends \
    && apt -y install --no-install-recommends \
    git \
    sudo \
    clang \
    cmake \
    && apt autoremove -y \
    && apt clean -y

RUN echo "Creating user ${USERNAME}..." \
    && groupadd -g ${USER_GID} ${USERNAME} \
    && useradd -u ${USER_UID} -g ${USER_GID} -s /bin/bash ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

ENV DEBIAN_FRONTEND=dialog

WORKDIR /home/${USERNAME}

USER ${USERNAME}

ENTRYPOINT [ "/bin/bash" ]