FROM i386/debian:bullseye

ARG GID=1000
ARG UID=1000

RUN groupadd --gid $GID node \
    && useradd --gid $GID --uid $UID node

RUN sed -i 's|deb.debian.org|mirrors.tuna.tsinghua.edu.cn|g' /etc/apt/sources.list
RUN sed -i 's|security.debian.org|mirrors.tuna.tsinghua.edu.cn/debian-security|g' /etc/apt/sources.list

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
         git \
         curl \
         make \
         python3 \
         ccache \
         g++ \
         xz-utils \
         build-essential

COPY --chown=node:node run.sh /home/node/run.sh

VOLUME /home/node/.ccache
VOLUME /out
VOLUME /home/node/node.tar.xz

USER node

ENTRYPOINT [ "/home/node/run.sh" ]
