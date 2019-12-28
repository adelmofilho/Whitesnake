FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get -y upgrade

RUN apt-get install -y \
  gdebi-core \
  psmisc \
  libapparmor1 \
  libedit2 \
  libclang-dev \  
  wget

RUN wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.2.5033-amd64.deb

RUN gdebi -n rstudio-server-1.2.5033-amd64.deb
