FROM rust:1.58-alpine3.15

ARG USER_UID=1000
ARG USERNAME=tensorush
ARG USER_GID=${USER_UID}

RUN echo "Installing packages..." \
    && apk --no-cache add \
    git \
    sudo

RUN echo "Creating user ${USERNAME}..." \
    && addgroup -g ${USER_GID} -S ${USERNAME} \
    && adduser -u ${USER_UID} -S ${USERNAME} -G ${USERNAME} -s /bin/sh -D ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

WORKDIR /home/${USERNAME}

USER ${USERNAME}

ENTRYPOINT [ "/bin/sh" ]