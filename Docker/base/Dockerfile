# Base Image
FROM biocontainers/biocontainers:latest

# Metadata
LABEL base.image="biocontainers:latest"
LABEL version="1"
LABEL software="NCBI Hackathon Base Image"
LABEL software.version="0.0.1"
LABEL description="Base image for NCBI Hackathons Projects"
LABEL website="https://github.com/NCBI-Hackathons/HackathonDockerImages/Docker/base"
LABEL documentation="https://github.com/NCBI-Hackathons/HackathonBaseImages/blob/master/Docker/README.md"
LABEL license="https://github.com/NCBI-Hackathons/HackathonDockerImages/LICENSE"
LABEL tags="NCBI, Hackathon"

# Maintainer
MAINTAINER Roberto Vera Alvarez <r78v10a07@gmail.com>

USER root

RUN apt-get update && \
    apt-get install -y \
        libncurses5-dev \
        libncursesw5-dev \
		libbz2-dev \
		lzma lzma-dev liblzma-dev \
		libcurl4-gnutls-dev \
		python3 python3-pip \
		nodejs npm \
		liblwp-protocol-https-perl \
		r-base r-base-dev && \
    apt-get clean && \
    apt-get purge && \
	pip3 install numpy pysam scipy && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER biodocker

WORKDIR /data/
