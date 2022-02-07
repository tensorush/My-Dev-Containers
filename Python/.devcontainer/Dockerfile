FROM nvidia/cuda:11.6.0-devel-ubuntu20.04

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

COPY ./requirements.txt ./

RUN echo "Installing pip packages..." \
    && python3 -m pip install -U pip \
    && pip3 --no-cache-dir install -r ./requirements.txt \
    && rm ./requirements.txt

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USERNAME=tensorush

RUN echo "Creating user ${USERNAME}..." \
    && groupadd -g ${GROUP_ID} ${USERNAME} \
    && useradd -u ${USER_ID} -g ${GROUP_ID} -s /usr/bin/fish ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

USER ${USERNAME}
