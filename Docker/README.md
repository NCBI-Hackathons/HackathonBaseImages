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

```
docker build -t ncbihackathon/ncbihackathonbase Docker/bioconductor .
```


## Base Image with Entrez Direct

The `Base Image with Entrez Direct` definition is into the `eutils` directory. This image should be build before any other image in this project.

```
docker build -t ncbihackathon/ncbihackathonbase Docker/eutils .
```



