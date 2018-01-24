# Base Image
FROM ncbihackathon/ncbihackathonbase:latest

# Metadata
LABEL base.image="ncbihackathonbase:latest"
LABEL version="1"
LABEL software="NCBI Hackathon Image for NGS analysis"
LABEL software.version="0.0.1"
LABEL description="NCBI Hackathons Image for NGS analysis"
LABEL website="https://github.com/NCBI-Hackathons/HackathonDockerImages/Docker/ngs"
LABEL documentation="https://github.com/NCBI-Hackathons/HackathonDockerImages/Docker/ngs"
LABEL license="https://github.com/NCBI-Hackathons/HackathonDockerImages/LICENSE"
LABEL tags="NCBI, Hackathon, Bioconductor"

# Maintainer
MAINTAINER Roberto Vera Alvarez <r78v10a07@gmail.com>

USER biodocker

# Samtools 1.6
ENV ZIP=samtools-1.6.tar.bz2
ENV URL=https://github.com/samtools/samtools/releases/download/1.6/
ENV FOLDER=samtools-1.6
ENV DST=/tmp

RUN wget $URL/$ZIP -O $DST/$ZIP && \
    tar xvf $DST/$ZIP -C $DST && \
    rm $DST/$ZIP && \
    cd $DST/$FOLDER && \
		./configure --prefix=/home/biodocker && \
    make && \
    make install && \
    cd / && \
    rm -rf $DST/$FOLDER

# BAMTools 2.5.1
ENV ZIP=v2.5.1.tar.gz
ENV URL=https://github.com/pezmaster31/bamtools/archive/
ENV FOLDER=bamtools-2.5.1
ENV INSTALL_FOLDER=/home/biodocker/
ENV DST=/tmp
ENV LD_LIBRARY_PATH=$INSTALL_FOLDER/lib/bamtools:$LD_LIBRARY_PATH

RUN cd $DST && \
	wget $URL/$ZIP -O $DST/$ZIP && \
	tar xzfv $DST/$ZIP -C $DST && \
	cd $DST/$FOLDER && mkdir build && cd build && \
	cmake -DCMAKE_INSTALL_PREFIX=$INSTALL_FOLDER .. && make && \
	make install && \
	rm -rf $DST/$FOLDER $DST/$ZIP

# STAR 2.5.3a
ENV ZIP=2.5.3a.tar.gz
ENV URL=https://github.com/alexdobin/STAR/archive/
ENV FOLDER=STAR-2.5.3a
ENV INSTALL_FOLDER=/home/biodocker/
ENV DST=/tmp

RUN cd $DST && \
	wget $URL/$ZIP -O $DST/$ZIP && \
	tar xzfv $DST/$ZIP -C $DST && \
	cd $DST/$FOLDER/source && \
	make && \
	mv STAR /home/biodocker/bin/ && \
	rm -rf $DST/$FOLDER $DST/$ZIP

# NCBI-magicblast 1.3.0
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
