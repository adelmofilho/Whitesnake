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
    libapparmor1=2.12-4ubuntu5.1 \ 
    libedit2=3.1-20170329-1 \
    libclang-dev=1:6.0-41~exp5~ubuntu1 \
    psmisc=23.1-1ubuntu0.1 \
    sudo=1.8.21p2-3ubuntu1.1 \
&& rm -rf /var/lib/apt/lists/*

RUN wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.2.5033-amd64.deb

RUN gdebi -n rstudio-server-1.2.5033-amd64.deb