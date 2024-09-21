
FROM rocker/r-ubuntu:20.04

RUN    apt update -qq \
    && apt install -y r-cran-rcppgsl libgsl-dev \
    && Rscript -e 'install.packages("RcppZiggurat")' \
    && Rscript -e 'library(RcppZiggurat); cat("All good\n")'

## Upgrade from focal to jammy, which means GSL 2.3.* to 2.7.*
RUN    sed -i -e 's/focal/jammy/g' /etc/apt/sources.list \
    && sed -i -e 's/focal/jammy/g' /etc/apt/sources.list.d/c2d4u_team-ubuntu-c2d4u4_0_-focal.list

## 326 packages if we upgrade, so skip now, run if you prefer
#RUN    apt update -qq \
#    && apt upgrade -y 

## Now (for expedience just) upgrade RcppGSL, brings upgraded libgsl28, removes libgsl27
RUN    apt update -qq \
    && apt install -y r-cran-rcppgsl

## And RcppZiggurat is borked -- this fails because libgsl23 is gone
## so we comment it out not run break the docker build, but see 'manually'
#RUN Rscript -e 'library(RcppZiggurat)'
