FROM alpine:3.15

RUN echo "Installing apk packages..." \
    && apk --no-cache add \
    git \
    curl \
    fish \
    sudo \
    zstd

ENV LEAN_VERSION=4.0.0

RUN echo "Installing Lean ver. ${LEAN_VERSION}..." \
    && curl -o /opt/lean4.tar.zst https://github.com/leanprover/lean4/releases/download/v${LEAN_VERSION}-m3/lean-${LEAN_VERSION}-linux.tar.zst \
    && tar --use-compress-program=unzstd -xf /opt/lean4.tar.zst -C /opt/

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USER_NAME=tensorush

RUN echo "Creating user ${USER_NAME}..." \
    && addgroup -g ${GROUP_ID} -S ${USER_NAME} \
    && adduser -u ${USER_ID} -S ${USER_NAME} -G ${USER_NAME} -s /usr/bin/fish -D ${USER_NAME} \
    && echo "${USER_NAME} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/${USER_NAME} \
    && chmod 0440 /etc/sudoers.d/${USER_NAME}

USER ${USER_NAME}
