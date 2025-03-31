ARG build_as_root=no
ARG base_image="rockylinux:8"

FROM ${base_image} AS base

RUN dnf module reset ruby -y

RUN dnf -y install \
    rpmdevtools \
    rpmlint \
    rsync \
    @ruby:3.0 \
    unzip \
    gem

RUN gem install \
    fpm


FROM base AS build_as_root_yes
WORKDIR /root


FROM base AS build_as_root_no
RUN useradd builder
USER builder
WORKDIR /home/builder


FROM build_as_root_${build_as_root}
RUN rpmdev-setuptree
