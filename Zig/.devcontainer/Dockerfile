FROM alpine:3.15

RUN echo "Installing apk packages..." \
    && apk --no-cache add \
    git \
    curl \
    fish \
    sudo

ENV ZIG_VERSION=0.9.0
ENV ZIG_DIR_PATH=/opt/zig/

RUN echo "Installing Zig ver. ${ZIG_VERSION}..." \
    && mkdir ${ZIG_DIR_PATH} \
    && curl -o ${ZIG_DIR_PATH}zig.tar.xz https://ziglang.org/download/${ZIG_VERSION}/zig-linux-x86_64-${ZIG_VERSION}.tar.xz \
    && tar -xf ${ZIG_DIR_PATH}zig.tar.xz -C ${ZIG_DIR_PATH} \
    && ln -s ${ZIG_DIR_PATH}zig-linux-x86_64-${ZIG_VERSION}/zig /usr/local/bin/zig \
    && rm ${ZIG_DIR_PATH}zig.tar.xz

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USER_NAME=tensorush

RUN echo "Creating user ${USER_NAME}..." \
    && addgroup -g ${GROUP_ID} -S ${USER_NAME} \
    && adduser -u ${USER_ID} -S ${USER_NAME} -G ${USER_NAME} -s /usr/bin/fish -D ${USER_NAME} \
    && echo "${USER_NAME} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/${USER_NAME} \
    && chmod 0440 /etc/sudoers.d/${USER_NAME}

USER ${USER_NAME}
