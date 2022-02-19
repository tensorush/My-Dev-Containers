FROM nvidia/cuda:11.6.0-devel-ubuntu20.04

RUN echo "Installing apt packages..." \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt -y update --no-install-recommends \
    && apt -y install --no-install-recommends \
    git \
    curl \
    fish \
    sudo \
    clang \
    && apt autoremove -y \
    && apt clean -y \
    export DEBIAN_FRONTEND=dialog

ENV CMAKE_VERSION=3.22.2
ENV CMAKE_DIR_PATH=/opt/cmake/

RUN echo "Installing CMake ver. ${CMAKE_VERSION}..." \
    && mkdir -p ${CMAKE_DIR_PATH} \
    && curl -o ${CMAKE_DIR_PATH}cmake.sh https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-Linux-x86_64.sh \
    && sh ${CMAKE_DIR_PATH}cmake.sh --prefix=${CMAKE_DIR_PATH} --skip-license \
    && ln -s ${CMAKE_DIR_PATH}bin/cmake /usr/local/bin/cmake \
    && rm ${CMAKE_DIR_PATH}cmake.sh

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USER_NAME=tensorush

RUN echo "Creating user ${USER_NAME}..." \
    && groupadd -g ${GROUP_ID} ${USER_NAME} \
    && useradd -u ${USER_ID} -g ${GROUP_ID} -s /usr/bin/zsh -m ${USER_NAME} \
    && echo "${USER_NAME} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/${USER_NAME} \
    && chmod 0440 /etc/sudoers.d/${USER_NAME}

USER ${USER_NAME}
