# Base Image
FROM ncbihackathon/ncbihackathonbase:latest

# Metadata
LABEL base.image="ncbihackathonbase:latest"
LABEL version="1"
LABEL software="NCBI Hackathon Image with Entrez Direct"
LABEL software.version="0.0.1"
LABEL description="NCBI Hackathons Image with Entrez Direct"
LABEL website="https://github.com/NCBI-Hackathons/HackathonDockerImages/Docker/eutils"
LABEL documentation="https://github.com/NCBI-Hackathons/HackathonBaseImages/blob/master/Docker/eutils/README.md"
LABEL license="https://github.com/NCBI-Hackathons/HackathonDockerImages/LICENSE"
LABEL tags="NCBI, Hackathon, Bioconductor"

# Maintainer
MAINTAINER Roberto Vera Alvarez <r78v10a07@gmail.com>

USER biodocker

ENV ZIP=edirect-7.80.20180123.tar.gz
ENV URL=ftp://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/versions/7.80.20180123/
ENV FOLDER=edirect
ENV INSTALL_FOLDER=/home/biodocker/
ENV DST=/tmp

RUN cd $DST && \
	wget $URL/$ZIP -O $DST/$ZIP && \
	tar xzfv $DST/$ZIP -C $DST && \
	mv $DST/$FOLDER/* /home/biodocker/bin/ && \
	rm -rf $DST/$FOLDER

WORKDIR /data/
