# Base Image for NGS data analysis

The `Base Image for NGS data analysis` definition is into the `ngs` directory. This image should be build before any other image in this project.

## Building the image

```
docker build -t ncbihackathon/ngs Docker/ngs
```

## Software included

This image currently include:

* Samtools (version 1.6)
* BAMTools (version 2.5.1)
* STAR (version 2.5.3a)
* NCBI-magicblast (version 1.3.0)

Please, send us a request if you would like to include any other software in this image.

## Using Samtools

```
hydrus:Docker> docker run ncbihackathon/ngs samtools

Program: samtools (Tools for alignments in the SAM format)
Version: 1.6 (using htslib 1.6)

Usage:   samtools <command> [options]

Commands:
  -- Indexing
     dict           create a sequence dictionary file
     faidx          index/extract FASTA
     index          index alignment

  -- Editing
     calmd          recalculate MD/NM tags and '=' bases
     fixmate        fix mate information
     reheader       replace BAM header
     rmdup          remove PCR duplicates
     targetcut      cut fosmid regions (for fosmid pool only)
     addreplacerg   adds or replaces RG tags
     markdup        mark duplicates

  -- File operations
     collate        shuffle and group alignments by name
     cat            concatenate BAMs
     merge          merge sorted alignments
     mpileup        multi-way pileup
     sort           sort alignment file
     split          splits a file by read group
     quickcheck     quickly check if SAM/BAM/CRAM file appears intact
     fastq          converts a BAM to a FASTQ
     fasta          converts a BAM to a FASTA

  -- Statistics
     bedcov         read depth per BED region
     depth          compute the depth
     flagstat       simple stats
     idxstats       BAM index stats
     phase          phase heterozygotes
     stats          generate stats (former bamcheck)

  -- Viewing
     flags          explain BAM flags
     tview          text alignment viewer
     view           SAM<->BAM<->CRAM conversion
     depad          convert padded BAM to unpadded BAM

hydrus:Docker>
```

### Using BAMTools

```
hydrus:Docker> docker run ncbihackathon/ngs bamtools

usage: bamtools [--help] COMMAND [ARGS]

Available bamtools commands:
	convert         Converts between BAM and a number of other formats
	count           Prints number of alignments in BAM file(s)
	coverage        Prints coverage statistics from the input BAM file
	filter          Filters BAM file(s) by user-specified criteria
	header          Prints BAM header information
	index           Generates index for BAM file
	merge           Merge multiple BAM files into single file
	random          Select random alignments from existing BAM file(s), intended more as a testing tool.
	resolve         Resolves paired-end reads (marking the IsProperPair flag as needed)
	revert          Removes duplicate marks and restores original base qualities
	sort            Sorts the BAM file according to some criteria
	split           Splits a BAM file on user-specified property, creating a new BAM output file for each value found
	stats           Prints some basic statistics from input BAM file(s)

See 'bamtools help COMMAND' for more information on a specific command.

hydrus:Docker>
```

### Using STAR

```
hydrus:Docker> docker run ncbihackathon/ngs STAR
Usage: STAR  [options]... --genomeDir REFERENCE   --readFilesIn R1.fq R2.fq
Spliced Transcripts Alignment to a Reference (c) Alexander Dobin, 2009-2015

### versions
versionSTAR             020201
    int>0: STAR release numeric ID. Please do not change this value!
versionGenome           020101 020200
    int>0: oldest value of the Genome version compatible with this STAR release. Please do not change this value!

### Parameter Files
parametersFiles          -
    string: name of a user-defined parameters file, "-": none. Can only be defined on the command line.
```

### Using NCBI magicblast

```
hydrus:Docker> docker run ncbihackathon/ngs magicblast -h
USAGE
  magicblast [-h] [-help] [-db database_name] [-gilist filename]
    [-seqidlist filename] [-negative_gilist filename]
    [-negative_seqidlist filename] [-db_soft_mask filtering_algorithm]
    [-db_hard_mask filtering_algorithm] [-subject subject_input_file]
    [-subject_loc range] [-query input_file] [-out output_file] [-gzo]
    [-word_size int_value] [-gapopen open_penalty] [-gapextend extend_penalty]
    [-perc_identity float_value] [-penalty penalty] [-lcase_masking]
    [-validate_seqs TF] [-infmt format] [-paired] [-query_mate infile]
    [-sra accession] [-parse_deflines TF] [-sra_cache] [-outfmt format]
    [-no_query_id_trim] [-no_unaligned] [-num_threads int_value]
    [-max_intron_length length] [-score num] [-max_edit_dist num] [-splice TF]
    [-reftype type] [-limit_lookup TF] [-lookup_stride num] [-version]

DESCRIPTION
   Short read mapper
```

## Extending the image

To extend this image installing additional software you should create a `Dockerfile` modifiying this template with your requirements.

This example is adding magicblast


```
# Base Image
FROM ncbihackathon/ngs:latest

# Metadata
LABEL base.image="ngs:latest"
LABEL version="1"
LABEL software="NCBI Hackathon Image for NGS analysis and magicblast"
LABEL software.version="0.0.1"
LABEL description="NCBI Hackathon Image for NGS analysis and magicblast"

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
