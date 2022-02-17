FROM alpine:3.15

RUN echo "Installing apk packages..." \
    && apk --no-cache add \
    git \
    curl \
    fish \
    sudo

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USER_NAME=tensorush

RUN echo "Creating user ${USER_NAME}..." \
    && addgroup -g ${GROUP_ID} -S ${USER_NAME} \
    && adduser -u ${USER_ID} -S ${USER_NAME} -G ${USER_NAME} -s /usr/bin/fish -D ${USER_NAME} \
    && echo "${USER_NAME} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/${USER_NAME} \
    && chmod 0440 /etc/sudoers.d/${USER_NAME}

USER ${USER_NAME}

ENV GHCUP_VERSION=0.1.17.4
ENV GHCUP_DIR_PATH=${HOME}/.ghcup/bin/

RUN sudo mkdir -p ${GHCUP_DIR_PATH} \
    && sudo curl -o ${GHCUP_DIR_PATH}ghcup https://downloads.haskell.org/~ghcup/${GHCUP_VERSION}/x86_64-linux-ghcup-${GHCUP_VERSION} \
    && sudo chmod +x ${GHCUP_DIR_PATH}ghcup

ENV PATH=${GHCUP_DIR_PATH}:${PATH}

ENV GHC_VERSION=8.10.7

RUN echo "Installing Glasgow Haskell Compiler ver. ${GHC_VERSION}..." \
    && sudo ghcup install ghc ${GHC_VERSION} --set

ENV CABAL_VERSION=3.6.2.0

RUN echo "Installing Cabal ver. ${CABAL_VERSION}..." \
    && sudo ghcup install cabal ${CABAL_VERSION} --set

ENV HLS_VERSION=1.6.1.0

RUN echo "Installing Haskell Language Server ver. ${HLS_VERSION}..." \
    && sudo ghcup install hls ${HLS_VERSION} --set
