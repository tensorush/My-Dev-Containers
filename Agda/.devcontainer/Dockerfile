FROM alpine:3.15

RUN echo "Installing apk packages..." \
    && apk --no-cache add \
    git \
    curl \
    fish \
    sudo \
    cabal

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USER_NAME=tensorush

RUN echo "Creating user ${USER_NAME}..." \
    && addgroup -g ${GROUP_ID} -S ${USER_NAME} \
    && adduser -u ${USER_ID} -S ${USER_NAME} -G ${USER_NAME} -s /usr/bin/fish -D ${USER_NAME} \
    && echo "${USER_NAME} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/${USER_NAME} \
    && chmod 0440 /etc/sudoers.d/${USER_NAME}

USER ${USER_NAME}

RUN echo "Installing Agda..." \
    && cabal update \
    && cabal v2-install -j Agda --ghc-options -j

ENV AGDA_STDLIB_VERSION=1.7.1

RUN RUN echo "Installing Agda Standard Library ver. ${AGDA_STDLIB_VERSION}..." \
    && curl -o /opt/agda-stdlib.tar.gz https://github.com/agda/agda-stdlib/archive/refs/tags/v${AGDA_STDLIB_VERSION}.tar.gz \
    && tar -xf /opt/agda-stdlib.tar.gz -C /opt/ \
    && cd /opt/agda-stdlib-${AGDA_STDLIB_VERSION} \
    && cabal install \
    && mkdir .agda/ \
    && echo "/home/{USER_NAME}/agda-stdlib-${AGDA_STDLIB_VERSION}/standard-library.agda-lib" > .agda/libraries \
    && echo "standard-library" > .agda/defaults

ENV PATH=/home/${USER_NAME}/.cabal/bin/:${PATH}
