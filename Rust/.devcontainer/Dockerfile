FROM rust:1.58-alpine3.15

RUN echo "Installing apk packages..." \
    && apk --no-cache add \
    git \
    fish \
    sudo

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USERNAME=tensorush

RUN echo "Creating user ${USERNAME}..." \
    && addgroup -g ${GROUP_ID} -S ${USERNAME} \
    && adduser -u ${USER_ID} -S ${USERNAME} -G ${USERNAME} -s /usr/bin/fish -D ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

USER ${USERNAME}
