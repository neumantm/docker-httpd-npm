ARG HTTPD_VERSION=2.4
ARG NODE_VERSION=v8.11.3

FROM httpd:${HTTPD_VERSION}-alpine

ARG HTTPD_VERSION
ARG NODE_VERSION

LABEL httpd.version = $HTTPD_VERSION
LABEL node.version = $NODE_VERSION

#Most of the code to install NPM is copied from
#https://github.com/mhart/alpine-node
#
#See README.md for more information
RUN set -x; apk add --no-cache curl make gcc g++ python linux-headers binutils-gold gnupg libstdc++

RUN set -x; for server in ipv4.pool.sks-keyservers.net keyserver.pgp.com ha.pool.sks-keyservers.net; do \
    gpg --keyserver $server --recv-keys \
      94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
      B9AE9905FFD7803F25714661B63B535A4C206CA9 \
      77984A986EBC2AA786BC0F66B01FBB92821C587A \
      71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
      FD3A5288F042B6850C66B31F09FE44734EB7990E \
      8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600 \
      C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
      DD8F2338BAE7501E3DD5AC78C273792F7D83545D && break; \
  done

RUN set -x; cd / && \
  curl -sfSLO https://nodejs.org/dist/${NODE_VERSION}/node-${NODE_VERSION}.tar.xz && \
  curl -sfSL https://nodejs.org/dist/${NODE_VERSION}/SHASUMS256.txt.asc | gpg --batch --decrypt | \
    grep " node-${NODE_VERSION}.tar.xz\$" | sha256sum -c | grep ': OK$' && \
  tar -xf node-${NODE_VERSION}.tar.xz

RUN set -x; cd /node-${NODE_VERSION} && \
  ./configure --prefix=/usr && \
  make -j$(getconf _NPROCESSORS_ONLN) && \
  make install

RUN set -x; apk del curl make gcc g++ python linux-headers binutils-gold gnupg

RUN set -x; rm -rf /node-${NODE_VERSION}* /usr/share/man /tmp/* /var/cache/apk/* \
    /root/.npm /root/.node-gyp /root/.gnupg /usr/lib/node_modules/npm/man \
    /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html /usr/lib/node_modules/npm/scripts
