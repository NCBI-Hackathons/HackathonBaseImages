# NCBI Hackathon Docker Images
Base Docker images created from `Biocontainers` images to support NCBi Hackathon Projects.

## Source Code

To use the NCBI Hackathon base images you should clone this GitHub project and build the base image.

```
git clone https://github.com/NCBI-Hackathons/HackathonBaseImages
```

## Base Image

The `Base Image` definition is into the `base` directory. This image should be build before any other image in this project.

```
docker build -t ncbihackathon/ncbihackathonbase Docker/base .
```

## Base Image with Bioconductor

The `Base Image with Bioconductor` definition is into the `bioconductor` directory. This image should be build before any other image in this project.

### Building the image

```
docker build -t ncbihackathon/bioconductor Docker/bioconductor .
```

### Using the image

Creates a `data` directory to be mounted into the Docker container.

```
docker run -it -v `pwd`/data:/data ncbihackathon/bioconductor R
```

For R scripts store in the `data` directory:

```
docker run -it -v `pwd`/data:/data ncbihackathon/bioconductor Rscript --vanilla my_R_test.R
```

## Base Image with Entrez Direct

The `Base Image with Entrez Direct` definition is into the `eutils` directory. This image should be build before any other image in this project.

### Building the image

```
docker build -t ncbihackathon/eutils Docker/eutils .
```

### Using the image

Creates a `data` directory to be mounted into the Docker container.


