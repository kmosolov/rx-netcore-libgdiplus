FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-bionic
RUN echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula \
    select true | debconf-set-selections
RUN apt-get update \
    && apt-get install -y --no-install-recommends ttf-mscorefonts-installer gss-ntlmssp libpango1.0-dev libc6-dev language-pack-ru \
     libgif-dev git autoconf libtool automake build-essential gettext libglib2.0-dev libcairo2-dev libtiff-dev libexif-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/mono/libgdiplus
WORKDIR /libgdiplus
RUN ./autogen.sh --with-pango \
    && make \
    && make install \
    && ln -s /usr/local/lib/libgdiplus.so /usr/lib/libgdiplus.so
# Установка локализации в контейнере
ENV LANGUAGE ru_RU.UTF-8
ENV LANG ru_RU.UTF-8
ENV LC_ALL ru_RU.UTF-8
RUN echo "ru_RU.CP866 IBM866" >> /etc/locale.gen \
    && locale-gen
WORKDIR /
RUN rm -rf /libgdiplus
