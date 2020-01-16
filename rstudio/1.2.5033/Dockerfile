FROM adelmofilho/r-base:3.6.2

LABEL org.label-schema.license="GPL-3.0" \
      org.label-schema.vcs-url="https://github.com/adelmofilho/Whitesnake/rstudio/1.2.5033" \
      org.label-schema.vendor="Hope Clouds Observation" \
      maintainer="Adelmo Filho <adelmo.aguiar.filho@gmail.com>"

# Assumir defaults nas instalações 
ENV DEBIAN_FRONTEND=noninteractive

# Instalar dependências
RUN apt-get update && apt-get install -y --no-install-recommends \
    gdebi-core=0.9.5.7+nmu2 \ 
    lsb-release=9.20170808ubuntu1 \
    libapparmor1=2.12-4ubuntu5.1 \ 
    libedit2=3.1-20170329-1 \
    libclang-dev=1:6.0-41~exp5~ubuntu1 \
    psmisc=23.1-1ubuntu0.1 \
    sudo=1.8.21p2-3ubuntu1.1 \
&& rm -rf /var/lib/apt/lists/*

RUN wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.2.5033-amd64.deb

RUN gdebi -n rstudio-server-1.2.5033-amd64.deb

RUN mkdir -p /etc/R \
  ## Write config files in $R_HOME/etc
  && echo '\n\
    \n# Configure httr to perform out-of-band authentication if HTTR_LOCALHOST \
    \n# is not set since a redirect to localhost may not work depending upon \
    \n# where this Docker container is running. \
    \nif(is.na(Sys.getenv("HTTR_LOCALHOST", unset=NA))) { \
    \n  options(httr_oob_default = TRUE) \
    \n}' >> /usr/local/lib/R/etc/Rprofile.site \
  && echo "PATH=${PATH}" >> /usr/local/lib/R/etc/Renviron \
  ## Need to configure non-root user for RStudio
  && useradd rstudio \
  && echo "rstudio:rstudio" | chpasswd \
	&& mkdir /home/rstudio \
	&& chown rstudio:rstudio /home/rstudio \
	&& addgroup rstudio staff \
  ## Prevent rstudio from deciding to use /usr/bin/R if a user apt-get installs a package
  &&  echo 'rsession-which-r=/usr/local/bin/R' >> /etc/rstudio/rserver.conf \
  ## use more robust file locking to avoid errors when using shared volumes:
  && echo 'lock-type=advisory' >> /etc/rstudio/file-locks \
  ## configure git not to request password each time
  && git config --system credential.helper 'cache --timeout=3600' \
  && git config --system push.default simple \
  ## Set up S6 init system
  && wget -P /tmp/ https://github.com/just-containers/s6-overlay/releases/download/v1.21.7.0/s6-overlay-amd64.tar.gz \
  && tar xzf /tmp/s6-overlay-amd64.tar.gz -C / \
  && mkdir -p /etc/services.d/rstudio \
  && echo '#!/usr/bin/with-contenv bash \
          \n## load /etc/environment vars first: \
  		  \n for line in $( cat /etc/environment ) ; do export $line ; done \
          \n exec /usr/lib/rstudio-server/bin/rserver --server-daemonize 0' \
          > /etc/services.d/rstudio/run \
  && echo '#!/bin/bash \
          \n rstudio-server stop' \
          > /etc/services.d/rstudio/finish \
  && mkdir -p /home/rstudio/.rstudio/monitored/user-settings \
  && echo 'alwaysSaveHistory="0" \
          \nloadRData="0" \
          \nsaveAction="0"' \
          > /home/rstudio/.rstudio/monitored/user-settings/user-settings \
  && chown -R rstudio:rstudio /home/rstudio/.rstudio

ENV USER rstudio
ENV PASSWORD rstudio

RUN echo "$USER:$PASSWORD" | chpasswd

CMD ["/init"]