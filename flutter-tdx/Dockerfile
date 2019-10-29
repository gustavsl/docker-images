ARG IMAGE_ARCH=arm32v7
FROM torizon/$IMAGE_ARCH-debian-base:buster

RUN \
  DEBIAN_FRONTEND=noninteractive \
    apt update && apt install --assume-yes --no-install-recommends \
      git \
      libgl1-mesa-dev \
      libgles2-mesa-dev \
      libegl-mesa0 \ 
      libdrm-dev \
      libgbm-dev \
  \
  && rm -rf /var/lib/apt/lists/*

RUN echo "deb http://httpredir.debian.org/debian buster main contrib" > /etc/apt/sources.list \
    && echo "deb http://security.debian.org/ buster/updates main contrib" >> /etc/apt/sources.list \
    && echo "ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true" | debconf-set-selections \
    && apt-get update \
    && apt-get install -y ttf-mscorefonts-installer \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

RUN git clone --depth 1 --branch engine-binaries https://github.com/ardera/flutter-pi.git
RUN cp flutter-pi/libflutter_engine.so flutter-pi/icudtl.dat /usr/lib
RUN cp flutter-pi/flutter_embedder.h /usr/include
RUN rm -rf flutter-pi

RUN git clone https://github.com/gustavsl/flutter-tdx.git
RUN cp flutter-tdx/bin/flutter-tdx /usr/bin/

