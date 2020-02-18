<p align="center"><img src="https://vignette.wikia.nocookie.net/jjba/images/d/d0/Whitesnake_ASB.jpg/revision/latest/top-crop/width/220/height/220?cb=20151109102630" align="center" height=220/>
</p>

<h2 align="center">Whitesnake</h2>

<p align="center">
<a href="http://www.repostatus.org/#active"><img alt="Project Status: Active – The project has reached a stable, usable state and is being actively developed." src="https://www.repostatus.org/badges/latest/active.svg"></a>
<a href="https://www.codacy.com/manual/adelmofilho/Whitesnake?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=adelmofilho/Whitesnake&amp;utm_campaign=Badge_Grade"><img alt="Codacy Badge" src="https://api.codacy.com/project/badge/Grade/b3791d03b8354eb58e052b0db9862167"></a>
<a href="https://www.gnu.org/licenses/gpl-3.0"><img alt="License" src="https://img.shields.io/badge/License-GPLv3-blue.svg"></a>
<a href="https://doi.org/10.5281/zenodo.3610719"><img src="https://zenodo.org/badge/DOI/10.5281/zenodo.3610719.svg" alt="DOI"></a>
</p>

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

As imagems `r-base` e `rstudio` foram criadas com objetivo de serem utilizadas para deploy e desenvolvimento, respectivamente.

Em ambos os casos, o uso do pacote [`renv`](https://rstudio.github.io/renv/articles/renv.html) foi associado para garantir a consistência nos pacotes R.

### R-Studio

A imagem `rstudio` inicializa com o serviço do [rstudio-server](https://rstudio.com/products/rstudio/) exposto na porta 8787 de seu localhost.

Por padrão, login e senha são `rstudio` em ambos os casos.

Finalmente, para não será necessário instalar todos os pacotes R sempre que o docker for executado, montamos o `~/.local/share/renv` da máquina e do docker. Mais detalhes na documentação oficial do [`renv`](https://rstudio.github.io/renv/articles/renv.html#cache).

Todas os pontos levantados, resultam na seguinte chamada da imagem `rstudio`.

```sh
docker run -d --rm -p 8787:8787 \
-v /path/projeto:/home/project \
-v /home/${USER}/.local/share/renv:/home/rstudio/.local/share/renv \
adelmofilho/rstudio:1.2.5033
```

Na chamada acima, `/path/projeto` corresponde ao caminho para o diretório do seu projeto.

Ao acessar `localhost:8787` em seu navegador e entrar com login e senha no rstudio-server, execute no console o comando `renv::init()`. Com isso seu diretório passará a ser considerado um projeto R e os pacotes instalados terão seu cache armazenado no `~/.local/share/renv`.

<br>

## Licença

Os arquivos neste repositório estão sob licença GPL 3.
