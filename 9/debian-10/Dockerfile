FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages acl ca-certificates curl gzip libbsd0 libbz2-1.0 libc6 libcom-err2 libcurl4 libexpat1 libffi6 libfftw3-double3 libfontconfig1 libfreetype6 libgcc1 libgcrypt20 libglib2.0-0 libgmp10 libgnutls30 libgomp1 libgpg-error0 libgssapi-krb5-2 libhogweed4 libicu63 libidn2-0 libjpeg62-turbo libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 liblcms2-2 libldap-2.4-2 liblqr-1-0 libltdl7 liblzma5 libmagickcore-6.q16-6 libmagickwand-6.q16-6 libmemcached11 libmemcachedutil2 libncurses6 libncursesw6 libnettle6 libnghttp2-14 libonig5 libp11-kit0 libpcre3 libpng16-16 libpq5 libpsl5 libreadline7 librtmp1 libsasl2-2 libsodium23 libsqlite3-0 libssh2-1 libssl1.1 libstdc++6 libsybdb5 libtasn1-6 libtidy5deb1 libtinfo6 libunistring2 libuuid1 libwebp6 libx11-6 libxau6 libxcb1 libxdmcp6 libxext6 libxml2 libxslt1.1 libzip4 procps sqlite3 sudo tar zlib1g
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "python" "3.8.13-2" --checksum 704fe6b545280ae027303b4ec875b495ee6da2256b3d8f877467077b0f031a60
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "php" "8.1.4-3" --checksum 540ca94a39d500ed9e6bba61cda5ff89929d7959b80daf5b3e1e44327bc9f336
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "node" "14.19.1-0" --checksum 806082b15c0eb60e4baca497519b4c0cc9cd636d7a944e9943ebc1b9632fabdc
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "wait-for-port" "1.0.1-10" --checksum 35c818ba3f4b5aae905959bc7d3a5e81fc63786e3c662b604612c0aa7fcda8fd
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "laravel" "9.1.2-0" --checksum 63945a26db11e04c311440549a6df44ba6c446009a9630fd417f733f26297e0f
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "gosu" "1.14.0-7" --checksum d6280b6f647a62bf6edc74dc8e526bfff63ddd8067dcb8540843f47203d9ccf1
RUN apt-get update && apt-get upgrade -y && \
    rm -r /var/lib/apt/lists /var/cache/apt/archives
RUN /build/bitnami-user.sh

COPY rootfs /
RUN /opt/bitnami/scripts/laravel/postunpack.sh
RUN /opt/bitnami/scripts/php/postunpack.sh
ENV APP_VERSION="9.1.2" \
    BITNAMI_APP_NAME="laravel" \
    BITNAMI_IMAGE_VERSION="9.1.2-debian-10-r15" \
    NODE_PATH="/opt/bitnami/node/lib/node_modules" \
    PATH="/opt/bitnami/python/bin:/opt/bitnami/php/bin:/opt/bitnami/php/sbin:/opt/bitnami/node/bin:/opt/bitnami/common/bin:$PATH" \
    PHP_ENABLE_OPCACHE="0"

EXPOSE 3000 8000

WORKDIR /app
ENTRYPOINT [ "/opt/bitnami/scripts/laravel/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/laravel/run.sh" ]
