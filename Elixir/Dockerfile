FROM ubuntu:15.04
MAINTAINER Johnny Mejias jmejias17@gmail.com

RUN locale-gen en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN apt-get update && \
    apt-get -y install wget curl

RUN echo "deb http://packages.erlang-solutions.com/ubuntu vivid contrib" >> /etc/apt/sources.list

RUN mkdir /Downloads
WORKDIR /Downloads

RUN wget http://packages.erlang-solutions.com/ubuntu/erlang_solutions.asc
RUN apt-key add erlang_solutions.asc
RUN apt-get update && \
    apt-get -y install erlang && \
    apt-get -y install erlang-base-hipe && \
    apt-get -y install elixir && \
    mkdir /app

COPY mix.exs /app/mix.exs

WORKDIR /app

RUN mix local.hex --force && \
    mix local.rebar --force

RUN mix do deps.get, compile
