# Base Image
FROM ncbihackathon/ncbihackathonbase:latest

# Metadata
LABEL base.image="ncbihackathonbase:latest"
LABEL version="1"
LABEL software="NCBI Hackathon Image with Bioconductor"
LABEL software.version="0.0.1"
LABEL description="NCBI Hackathons Image with Bioconductor"
LABEL website="https://github.com/NCBI-Hackathons/HackathonDockerImages/Docker/bioconductor"
LABEL documentation="https://github.com/NCBI-Hackathons/HackathonBaseImages/blob/master/Docker/bioconductor/README.md"
LABEL license="https://github.com/NCBI-Hackathons/HackathonDockerImages/LICENSE"
LABEL tags="NCBI, Hackathon, Bioconductor"

# Maintainer
MAINTAINER Roberto Vera Alvarez <r78v10a07@gmail.com>

USER root

RUN R -e "source('http://bioconductor.org/biocLite.R');biocLite()"

USER biodocker

WORKDIR /data/
