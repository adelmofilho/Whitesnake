FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get -y upgrade

RUN apt-get install -y gfortran && \
    apt-get install -y libreadline6-dev && \
    apt-get install -y libx11-dev && \
    apt-get install -y libxt-dev && \
    apt-get install -y libpng-dev && \
    apt-get install -y libjpeg-dev && \
    apt-get install -y libcairo2-dev && \
    apt-get install -y xvfb && \
    apt-get install -y gdebi-core && \
    apt-get install -y libcurl4-openssl-dev  && \
    apt-get install -y libssl-dev  && \ 
    apt-get install -y libxml2-dev && \
    apt-get install -y libudunits2-dev && \
    apt-get install -y libgdal-dev && \
    apt-get install -y libbz2-dev && \
    apt-get install -y libzstd-dev && \
    apt-get install -y liblzma-dev && \
    apt-get install -y libcurl4-openssl-dev && \
    apt-get install -y texinfo && \
    apt-get install -y texlive && \
    apt-get install -y texlive-fonts-extra && \
    apt-get install -y screen && \
    apt-get install -y wget && \
    apt-get install -y openjdk-8-jdk && \
    apt-get install -y git

RUN wget https://cran.rstudio.com/src/base/R-3/R-3.6.2.tar.gz

RUN tar zxvf R-3.6.2.tar.gz

RUN cd R-3.6.2 && \ 
    ./configure --with-cairo --with-jpeglib --enable-R-shlib --with-blas --with-lapack && \ 
    make && \
    make install
