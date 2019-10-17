ARG OPENJDK_VERSION=8u222

FROM openjdk:${OPENJDK_VERSION}-jdk-slim-buster
ARG SBT_VERSION=0.13.17

RUN set -eux; \
    \
    savedAptMark="$(apt-mark showmanual)"; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        dirmngr \
        gnupg \
        wget \
    ; \
    rm -rf /var/lib/apt/lists/*; \
    \
    echo "deb https://dl.bintray.com/sbt/debian /" \
        | tee -a /etc/apt/sources.list.d/sbt.list; \
    apt-key adv --keyserver hkps://keyserver.ubuntu.com:443 --recv 0x2EE0EA64E40A89B84B2DF73499E82A75642AC823; \
    apt-get update; \
    \
    apt-mark auto '.*' > /dev/null; \
    apt-mark manual 'sbt'; \
    [ -z "$savedAptMark" ] || apt-mark manual $savedAptMark > /dev/null; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
    \
    apt-get install -y sbt="$SBT_VERSION";
