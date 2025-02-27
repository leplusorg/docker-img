# Images

Docker container to manipulate images (imagemagick, exiftool...).

[![Dockerfile](https://img.shields.io/badge/GitHub-Dockerfile-blue)](https://github.com/leplusorg/docker-img/blob/main/img/Dockerfile)
[![Docker Build](https://github.com/leplusorg/docker-img/workflows/Docker/badge.svg)](https://github.com/leplusorg/docker-img/actions?query=workflow:"Docker")
[![Docker Stars](https://img.shields.io/docker/stars/leplusorg/img)](https://hub.docker.com/r/leplusorg/img)
[![Docker Pulls](https://img.shields.io/docker/pulls/leplusorg/img)](https://hub.docker.com/r/leplusorg/img)
[![Docker Version](https://img.shields.io/docker/v/leplusorg/img?sort=semver)](https://hub.docker.com/r/leplusorg/img)

## Example without using the filesystem

Let's say that you have an image `foo.jpg` in your current working directory that you want to extract its metadata:

**Mac/Linux**

```bash
cat foo.jpg | docker run --rm -i --net=none leplusorg/img identify -
```

**Windows**

```batch
type foo.jpg | docker run --rm -i --net=none leplusorg/img identify -
```

## Example using the filesystem

Same thing, assuming that you have an image `foo.jpg` in your current working directory that you want to extract its metadata:

**Mac/Linux**

```bash
docker run --rm -t --user="$(id -u):$(id -g)" --net=none -v "$(pwd):/tmp" leplusorg/img identify /tmp/foo.jpg
```

**Windows**

In `cmd`:

```batch
docker run --rm -t --net=none -v "%cd%:/tmp" leplusorg/img identify /tmp/foo.jpg
```

In PowerShell:

```pwsh
docker run --rm -t --net=none -v "${PWD}:/tmp" leplusorg/img identify /tmp/foo.jpg
```

## Help

To know more command-line options of one of the imagemagick command:

```bash
docker run --rm --net=none leplusorg/img identify -help
```

## Software Bill of Materials (SBOM)

To get the SBOM for the latest image (in SPDX JSON format), use the
following command:

```bash
docker buildx imagetools inspect leplusorg/img --format '{{ json (index .SBOM "linux/amd64").SPDX }}'
```

Replace `linux/amd64` by the desired platform (`linux/amd64`, `linux/arm64` etc.).

## Request new tool

Please use [this link](https://github.com/leplusorg/docker-img/issues/new?assignees=thomasleplus&labels=enhancement&template=feature_request.md&title=%5BFEAT%5D) (GitHub account required) to request that a new tool be added to the image. I am always interested in adding new capabilities to these images.
