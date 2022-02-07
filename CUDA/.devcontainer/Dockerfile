FROM nvidia/cuda:11.6.0-devel-ubuntu20.04

RUN echo "Installing apt packages..." \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt -y update --no-install-recommends \
    && apt -y install --no-install-recommends \
    git \
    fish \
    sudo \
    clang \
    && apt autoremove -y \
    && apt clean -y \
    export DEBIAN_FRONTEND=dialog

ENV CMAKE_VERSION=3.22.2
ENV CMAKE_PLATFORM=Linux
ENV CMAKE_ARCHITECTURE=x86_64
ENV CMAKE_BINARY=cmake-${CMAKE_VERSION}-${CMAKE_PLATFORM}-${CMAKE_ARCHITECTURE}

RUN echo "Installing CMake ver. ${CMAKE_VERSION}..." \
    && wget -q -O ./cmake.sh https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/${CMAKE_BINARY}.sh \
    && mkdir /opt/cmake \
    && sh ./cmake.sh --prefix=/opt/cmake --skip-license \
    && ln -s /opt/cmake/bin/cmake /usr/local/bin/cmake \
    && rm ./cmake.sh

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USERNAME=tensorush

RUN echo "Creating user ${USERNAME}..." \
    && groupadd -g ${USER_GID} ${USERNAME} \
    && useradd -u ${USER_UID} -g ${USER_GID} -s /usr/bin/fish ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

USER ${USERNAME}
