FROM alpine:3.15

ARG USER_UID=1000
ARG USERNAME=tensorush
ARG USER_GID=${USER_UID}

ARG ZIG_VERSION=0.9.0
ARG ZIG_PLATFORM=linux
ARG ZIG_ARCHITECTURE=x86_64
ARG ZIG_BINARY=zig-${ZIG_PLATFORM}-${ZIG_ARCHITECTURE}-${ZIG_VERSION}

RUN echo "Installing system packages..." \
    && apk --no-cache add sudo

RUN echo "Creating user ${USERNAME}..." \
    && addgroup -g ${USER_GID} -S ${USERNAME} \
    && adduser -u ${USER_UID} -S ${USERNAME} -G ${USERNAME} -s /bin/sh -D ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

WORKDIR /opt

RUN echo "Installing Zig ver. ${ZIG_VERSION}..." \
    && wget https://ziglang.org/download/${ZIG_VERSION}/${ZIG_BINARY}.tar.xz \
    && tar -xf ${ZIG_BINARY}.tar.xz \
    && rm ${ZIG_BINARY}.tar.xz \
    && ln -s /opt/${ZIG_BINARY}/zig /usr/local/bin/zig

WORKDIR /home/${USERNAME}

USER ${USERNAME}

ENTRYPOINT [ "/bin/sh" ]