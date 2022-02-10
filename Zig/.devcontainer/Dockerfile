FROM alpine:3.15

RUN echo "Installing apk packages..." \
    && apk --no-cache add \
    git \
    fish \
    sudo

ENV ZIG_VERSION=0.9.0
ENV ZIG_BINARY=zig-linux-x86_64-${ZIG_VERSION}

RUN echo "Installing Zig ver. ${ZIG_VERSION}..." \
    && cd /opt \
    && wget https://ziglang.org/download/${ZIG_VERSION}/${ZIG_BINARY}.tar.xz \
    && tar -xf ./${ZIG_BINARY}.tar.xz \
    && rm ./${ZIG_BINARY}.tar.xz \
    && ln -s ./${ZIG_BINARY}/zig /usr/local/bin/zig

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USERNAME=tensorush

RUN echo "Creating user ${USERNAME}..." \
    && addgroup -g ${GROUP_ID} -S ${USERNAME} \
    && adduser -u ${USER_ID} -S ${USERNAME} -G ${USERNAME} -s /usr/bin/fish -D ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

USER ${USERNAME}
