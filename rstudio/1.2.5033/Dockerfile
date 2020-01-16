FROM adelmofilho/r-base:3.6.2

LABEL org.label-schema.license="GPL-3.0" \
      org.label-schema.vcs-url="https://github.com/adelmofilho/Whitesnake/rstudio/1.2.5033" \
      org.label-schema.vendor="Hope Clouds Observation" \
      maintainer="Adelmo Filho <adelmo.aguiar.filho@gmail.com>"

# Assumir defaults nas instalações 
ENV DEBIAN_FRONTEND=noninteractive

# Criação do usuário para rstudio-server
ENV USER rstudio
ENV PASSWORD rstudio

RUN useradd rstudio \
  && echo "${USER}:${PASSWORD}" | chpasswd \
  && mkdir /home/${USER} \
  && chown ${USER}:${USER} /home/${USER}

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

# Instala RStudio-Server
RUN wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.2.5033-amd64.deb

RUN gdebi -n rstudio-server-1.2.5033-amd64.deb

# Seta configurações adicionais (adaptado do projeto Rocker)
WORKDIR /etc/R

RUN  echo 'if(is.na(Sys.getenv("HTTR_LOCALHOST", unset=NA))) { options(httr_oob_default = TRUE) }' >> /usr/local/lib/R/etc/Rprofile.site \
  && echo "PATH=${PATH}" >> /usr/local/lib/R/etc/Renviron \
  && echo 'rsession-which-r=/usr/local/bin/R' >> /etc/rstudio/rserver.conf \
  && echo 'lock-type=advisory' >> /etc/rstudio/file-locks

# Configura sistema s6 para inicialização do rstudio-server com o container (adaptado do projeto Rocker)
RUN git config --system credential.helper 'cache --timeout=3600' \
  && git config --system push.default simple \
  && wget -P /tmp/ https://github.com/just-containers/s6-overlay/releases/download/v1.21.7.0/s6-overlay-amd64.tar.gz \
  && tar xzf /tmp/s6-overlay-amd64.tar.gz -C / \
  && mkdir -p /etc/services.d/rstudio 

RUN echo -e "#!/usr/bin/with-contenv bash \
          \n## load /etc/environment vars first: \
  		  \n for line in $( cat /etc/environment ) ; do export $line ; done \
          \n exec /usr/lib/rstudio-server/bin/rserver --server-daemonize 0" \
          > /etc/services.d/rstudio/run

RUN echo -e "#!/bin/bash \
          \n rstudio-server stop" \
          > /etc/services.d/rstudio/finish \
  && mkdir -p /home/rstudio/.rstudio/monitored/user-settings

RUN echo -e "alwaysSaveHistory='0' \
          \nloadRData='0' \
          \nsaveAction='0'" \
          > /home/rstudio/.rstudio/monitored/user-settings/user-settings \
  && chown -R rstudio:rstudio /home/rstudio/.rstudio

CMD ["/init"]