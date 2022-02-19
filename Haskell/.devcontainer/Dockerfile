FROM alpine:3.15

RUN echo "Installing apk packages..." \
    && apk --no-cache add \
    ghc \
    git \
    curl \
    fish \
    sudo \
    cabal

ENV HLS_VERSION=1.6.1.0

RUN curl -L -o /opt/hls.tar.gz https://github.com/haskell/haskell-language-server/releases/download/${HLS_VERSION}/haskell-language-server-Linux-${HLS_VERSION}.tar.gz \
    && tar -xz /opt/hls.tar.gz -C /opt/ \
    && chmod +x /opt/haskell-language-server-Linux-${HLS_VERSION}

RUN echo "Installing cabal packages..." \
    && cabal update

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USER_NAME=tensorush

RUN echo "Creating user ${USER_NAME}..." \
    && addgroup -g ${GROUP_ID} -S ${USER_NAME} \
    && adduser -u ${USER_ID} -S ${USER_NAME} -G ${USER_NAME} -s /usr/bin/fish -D ${USER_NAME} \
    && echo "${USER_NAME} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/${USER_NAME} \
    && chmod 0440 /etc/sudoers.d/${USER_NAME}

USER ${USER_NAME}
