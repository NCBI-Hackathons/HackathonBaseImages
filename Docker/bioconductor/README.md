# Base Image with Bioconductor

The `Base Image with Bioconductor` definition is into the `bioconductor` directory. This image should be build before any other image in this project.

The image is based on R version 3.2.3 (2015-12-10) -- “Wooden Christmas-Tree”

## Building the image

```
docker build -t ncbihackathon/bioconductor Docker/bioconductor
```

## Using R

Creates a `data` directory to be mounted into the Docker container.

```
docker run -it -v `pwd`/data:/data ncbihackathon/bioconductor R
```

For R scripts store in the `data` directory:

```
docker run -it -v `pwd`/data:/data ncbihackathon/bioconductor Rscript --vanilla my_R_test.R
```

## Extending the image

To extend this image installing additional R packages you should create a `Dockerfile` modifiying this template with your requirements.


```
# Base Image
FROM ncbihackathon/bioconductor:latest

# Metadata
LABEL base.image="bioconductor:latest"
LABEL version="1"
LABEL software="NCBI Hackathon Image with Bioconductor and Extra R packages"
LABEL software.version="0.0.1"
LABEL description="NCBI Hackathons Image with Bioconductor and Extra R packages"

# Modify these next lines
LABEL website="https://github.com/NCBI-Hackathons/HackathonDockerImages"
LABEL documentation="https://github.com/NCBI-Hackathons/HackathonDockerImages"
LABEL license="https://github.com/NCBI-Hackathons/HackathonDockerImages/LICENSE"
LABEL tags="NCBI, Hackathon, Bioconductor"

# Maintainer
MAINTAINER Roberto Vera Alvarez <r78v10a07@gmail.com>

USER root

RUN R -e "install.packages('plotly', repos = 'http://cran.us.r-project.org')" && \
    R -e "install.packages('dplyr', repos = 'http://cran.us.r-project.org')" && \
    R -e "install.packages('reshape2', repos = 'http://cran.us.r-project.org')"

USER biodocker

WORKDIR /data/
```

