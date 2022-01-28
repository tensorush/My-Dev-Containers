ARG CUDA_VERSION=10.2
ARG CUDA_FLAVOR=devel
ARG CUDA_PLATFORM=ubuntu18.04

FROM nvidia/cuda:${CUDA_VERSION}-${CUDA_FLAVOR}-${CUDA_PLATFORM}

ARG USER_UID=1000
ARG USERNAME=tensorush
ARG USER_GID=${USER_UID}

ARG CMAKE_VERSION=3.22.2
ARG CMAKE_PLATFORM=Linux
ARG CMAKE_ARCHITECTURE=x86_64
ARG CMAKE_BINARY=cmake-${CMAKE_VERSION}-${CMAKE_PLATFORM}-${CMAKE_ARCHITECTURE}

ENV DEBIAN_FRONTEND=noninteractive
ENV PATH=/usr/local/cuda-${CUDA_VERSION}/bin:${PATH}
ENV LD_LIBRARY_PATH=/usr/local/cuda-${CUDA_VERSION}/lib64:$LD_LIBRARY_PATH

RUN echo "Installing packages..." \
    && apt -y update --no-install-recommends \
    && apt -y install --no-install-recommends \
    git \
    sudo \
    clang \
    && apt autoremove -y \
    && apt clean -y

RUN echo "Installing CMake ver. ${CMAKE_VERSION}..." \
    && wget -q -O ./cmake.sh https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/${CMAKE_BINARY}.sh \
    && mkdir /opt/cmake \
    && sh ./cmake.sh --prefix=/opt/cmake --skip-license \
    && ln -s /opt/cmake/bin/cmake /usr/local/bin/cmake \
    && rm ./cmake.sh

RUN echo "Creating user ${USERNAME}..." \
    && groupadd -g ${USER_GID} ${USERNAME} \
    && useradd -u ${USER_UID} -g ${USER_GID} -s /bin/bash ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

ENV DEBIAN_FRONTEND=dialog

WORKDIR /home/${USERNAME}

USER ${USERNAME}

ENTRYPOINT [ "/bin/bash" ]