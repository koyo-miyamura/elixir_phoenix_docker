FROM elixir:1.12.3-alpine

RUN apk update && apk add \
  inotify-tools git build-base npm bash

ARG host_user_name
ARG host_group_name
ARG host_uid
ARG host_gid

RUN apk add shadow && groupadd -g $host_gid $host_group_name \
  && useradd -m -s /bin/bash -u $host_uid -g $host_gid $host_user_name

USER $host_user_name

RUN mix do local.hex --force, local.rebar --force, archive.install --force hex phx_new
