# NCBI Hackathon Docker Images
Base Docker images created from `Biocontainers` images to support NCBi Hackathon Projects.

## Source Code

To use the NCBI Hackathon base images you should clone this GitHub project and build the base image.

```
git clone https://github.com/NCBI-Hackathons/HackathonDockerImages
```

## Base Image

The `Base Image` definition is into the `base` directory. This image should be build before any other image in this project.

```
docker build -t ncbihackathon/ncbihackathonbase base .
```




