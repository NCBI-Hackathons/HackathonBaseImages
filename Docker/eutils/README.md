# Base Image with Entrez Direct

The `Base Image with Entrez Direct` definition is into the `eutils` directory. This image should be build before any other image in this project.

The image is based on Entrez Direct version 7.80.20180123.

## Building the image

```
docker build -t ncbihackathon/eutils Docker/eutils
```

## Using eUtils

For a simple search

```
hydrus:HackathonDockerImages> docker run ncbihackathon/eutils esearch -db pubmed -query Human
<ENTREZ_DIRECT>
  <Db>pubmed</Db>
  <WebEnv>NCID_1_16997612_130.14.22.215_9001_1516807053_874294722_0MetA0_S_MegaStore_F_1</WebEnv>
  <QueryKey>1</QueryKey>
  <Count>17437321</Count>
  <Step>1</Step>
</ENTREZ_DIRECT>
```

For a complex search using `pipes` you should create a bash script. Then, creates a `data` directory to be mounted into the Docker container and put your bash script on it.

Run your script like this

```
docker run -it -v `pwd`/data:/data ncbihackathon/eutils my_eutils_test.sh
```

## Extending the image

To extend this image installing additional software you should create a `Dockerfile` modifiying this template with your requirements.

This example is adding magicblast


```
# Base Image
FROM ncbihackathon/eutils:latest

# Metadata
LABEL base.image="eutils:latest"
LABEL version="1"
LABEL software="NCBI Hackathon Image with Entrez Direct and magicblast"
LABEL software.version="0.0.1"
LABEL description="NCBI Hackathon Image with Entrez Direct and magicblast"

# Modify these next lines
LABEL website="https://github.com/NCBI-Hackathons/HackathonDockerImages"
LABEL documentation="https://github.com/NCBI-Hackathons/HackathonDockerImages"
LABEL license="https://github.com/NCBI-Hackathons/HackathonDockerImages/LICENSE"
LABEL tags="NCBI, Hackathon, Bioconductor"

# Maintainer
MAINTAINER Roberto Vera Alvarez <r78v10a07@gmail.com>

USER biodocker

ENV ZIP=ncbi-magicblast-1.3.0-x64-linux.tar.gz
ENV URL=ftp://ftp.ncbi.nlm.nih.gov/blast/executables/magicblast/1.3.0/
ENV FOLDER=ncbi-magicblast-1.3.0
ENV INSTALL_FOLDER=/home/biodocker/
ENV DST=/tmp

RUN cd $DST && \
	wget $URL/$ZIP -O $DST/$ZIP && \
	tar xzfv $DST/$ZIP -C $DST && \
	mv $DST/$FOLDER/LICENSE $DST/$FOLDER/README /home/biodocker/bin/ && \
	mv $DST/$FOLDER/bin/* /home/biodocker/bin/ && \
	rm -rf $DST/$FOLDER

WORKDIR /data/
```
