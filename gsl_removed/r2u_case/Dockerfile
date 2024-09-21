
FROM rocker/r2u:20.04

## under r2u this installs RcppZiggurat binary and its dependencies
RUN    apt update -qq \
    && Rscript -e 'install.packages("RcppZiggurat")' \
    && Rscript -e 'library(RcppZiggurat); cat("All good\n")'

## Upgrade from noble to oracular, which means GSL 2.3.* to 2.7.*
RUN    sed -i -e 's/focal/jammy/g' /etc/apt/sources.list \
    && sed -i -e 's/focal/jammy/g' /etc/apt/sources.list.d/r2u.list

## Now (for expedience just) upgrade RcppGSL,
## brings upgraded libgsl27, removes libgsl23
RUN    apt update -qq \
    && apt install -y r-cran-rcppgsl

## So RcppZiggurat is not broken as it got upgraded too
Rscript -e 'library(RcppZiggurat); cat("All good\n")'
