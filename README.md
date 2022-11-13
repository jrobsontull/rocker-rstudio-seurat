# rocker-rstudio-seurat
Dockerfile for RStudio Server with Seurat dependencies. At present, build time on this image is painfully long because of the R package installs. This could be omitted if you only want the barebones Seurat package.

### Install
First you must clone the repo, or copy the `Dockerfile`, to your local machine. Assuming you have docker installed, you can then build the docker image from the `Dockerfile`.
``` bash
git clone https://github.com/jrobsontull/rocker-rstudio-seurat.git
cd rocker-rstudio-seurat
docker build . -f Dockerfile -t rocker/rstudio-seurat
```
If you want a faster build time, build the `Dockerfile.min`. This lacks the `bioconductor` and `CRAN suggests` packages.
```bash
docker build . -f Dockerfile.min -t rocker/rstudio-seurat
```

### Running the image
This container will run the RStudio server on localhost:8787 so this command will bind the port to the local machine's IP address.
``` bash
docker run --rm -ti -p 8787:8787 rocker/rstudio-seurat
```
 I also like to mount a volume to container. By default, this will be the working directory for RStudio if you run this command as is.
 ``` bash
docker run --rm -ti -p 8787:8787 -v /home/username/working_directory:/home/rstudio rocker/rstudio-seurat
```