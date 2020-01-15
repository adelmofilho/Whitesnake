FROM ubuntu:18.04

LABEL org.label-schema.license="GPL-3.0" \
      org.label-schema.vcs-url="https://github.com/adelmofilho/Whitesnake/r-base/3.6.2" \
      org.label-schema.vendor="Hope Clouds Observation" \
      maintainer="Adelmo Filho <adelmo.aguiar.filho@gmail.com>"

# Assumir defaults nas instalações 
ENV DEBIAN_FRONTEND=noninteractive

# Instalar dependências
RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-utils \
    gdebi-core \
    gfortran \
    git \
    libreadline6-dev \
    libx11-dev \
    libxt-dev \
    libpng-dev \
    libjpeg-dev \
    libcairo2-dev \   
    libcurl4-openssl-dev \
    libssl-dev \ 
    libxml2-dev \
    libudunits2-dev \
    libgdal-dev \
    libbz2-dev \
    libzstd-dev \
    liblzma-dev \
    libcurl4-openssl-dev \
    locales \
    openjdk-8-jdk \
    screen \
    texinfo \
    texlive \
    texlive-fonts-extra \
    wget \
    xvfb \
&& rm -rf /var/lib/apt/lists/*

# Ajuste o locale
RUN locale-gen pt_BR.UTF-8
ENV LANG pt_BR.UTF-8
ENV LANGUAGE pt_BR.UTF-8
ENV LC_ALL pt_BR.UTF-8

# Instalar R
WORKDIR /generics

RUN wget https://cran.rstudio.com/src/base/R-3/R-3.6.2.tar.gz && \
    tar zxvf R-3.6.2.tar.gz && \
    rm R-3.6.2.tar.gz && \
    cd R-3.6.2 && \ 
    ./configure --with-cairo --with-jpeglib --enable-R-shlib --with-blas --with-lapack && \ 
    make && \
    make install && \
    rm -rf R-3.6.2

# Instalar renv
ENV RENV_VERSION 0.9.2-20
RUN R -e "install.packages('remotes', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "remotes::install_github('rstudio/renv@${RENV_VERSION}')"