# Whitesnake <img src="https://vignette.wikia.nocookie.net/jjba/images/d/d0/Whitesnake_ASB.jpg/revision/latest/top-crop/width/220/height/220?cb=20151109102630" align="right" height=140/>

[![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](http://www.repostatus.org/#active) 
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0) [![Codacy Badge](https://api.codacy.com/project/badge/Grade/b3791d03b8354eb58e052b0db9862167)](https://www.codacy.com/manual/adelmofilho/Whitesnake?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=adelmofilho/Whitesnake&amp;utm_campaign=Badge_Grade)

<br>

## Descrição

Repositório pessoal de Dockerfiles para estudo e uso em projetos.

<br>

## Imagens disponibilizadas

Para acesso a todas as tags e log das builds acesse o [Dockerhub](https://hub.docker.com/u/adelmofilho) do projeto.

| Imagem  | Descrição                                 | Status                                                                               | Build Status                                                                             | Métricas                                                                       |
|---------|-------------------------------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| r-base  | R versionado com versionamento de pacotes | ![Build Status](https://img.shields.io/docker/cloud/build/adelmofilho/r-base)        | ![Build Status](https://img.shields.io/docker/cloud/automated/adelmofilho/r-base)        | ![Build Status](https://img.shields.io/docker/pulls/adelmofilho/r-base)        | 
| rstudio | Adiciona R-Studio                         | ![Build Status](https://img.shields.io/docker/cloud/build/adelmofilho/rstudio)       | ![Build Status](https://img.shields.io/docker/cloud/automated/adelmofilho/rstudio)       | ![Build Status](https://img.shields.io/docker/pulls/adelmofilho/rstudio)       |

<br>

## Uso

rstudio
```
docker run -d --rm -p 8787:8787 adelmofilho/rstudio:1.2.5033 -e USER=<usuário> -e PASSWORD=<senha>
```

## Licença

Os Dockerfiles neste repositório estão sob licença GPL 3.