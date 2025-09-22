# Images

Multi-platform Docker container with utilities to process images (`imagemagick`, `exiftool`, `optipng`...).

[![Dockerfile](https://img.shields.io/badge/GitHub-Dockerfile-blue)](img/Dockerfile)
[![Docker Build](https://github.com/leplusorg/docker-img/workflows/Docker/badge.svg)](https://github.com/leplusorg/docker-img/actions?query=workflow:"Docker")
[![Docker Stars](https://img.shields.io/docker/stars/leplusorg/img)](https://hub.docker.com/r/leplusorg/img)
[![Docker Pulls](https://img.shields.io/docker/pulls/leplusorg/img)](https://hub.docker.com/r/leplusorg/img)
[![Docker Version](https://img.shields.io/docker/v/leplusorg/img?sort=semver)](https://hub.docker.com/r/leplusorg/img)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/10073/badge)](https://bestpractices.coreinfrastructure.org/projects/10073)
[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/leplusorg/docker-img/badge)](https://securityscorecards.dev/viewer/?uri=github.com/leplusorg/docker-img)

## Example without using the filesystem

Let's say that you have an image `foo.jpg` in your current working directory that you want to extract its metadata:

**Mac/Linux**

```bash
cat foo.jpg | docker run --rm -i --net=none leplusorg/img magick identify -
```

**Windows**

```batch
type foo.jpg | docker run --rm -i --net=none leplusorg/img magick identify -
```

## Example using the filesystem

Same thing, assuming that you have an image `foo.jpg` in your current working directory that you want to extract its metadata:

**Mac/Linux**

```bash
docker run --rm -t --user="$(id -u):$(id -g)" --net=none -v "$(pwd):/tmp" leplusorg/img magick identify /tmp/foo.jpg
```

**Windows**

In `cmd`:

```batch
docker run --rm -t --net=none -v "%cd%:/tmp" leplusorg/img magick identify /tmp/foo.jpg
```

In PowerShell:

```pwsh
docker run --rm -t --net=none -v "${PWD}:/tmp" leplusorg/img magick identify /tmp/foo.jpg
```

## Help

To know more command-line options of one of the imagemagick command:

```bash
docker run --rm --net=none leplusorg/img magick -help
```

## Software Bill of Materials (SBOM)

To get the SBOM for the latest image (in SPDX JSON format), use the
following command:

```bash
docker buildx imagetools inspect leplusorg/img --format '{{ json (index .SBOM "linux/amd64").SPDX }}'
```

Replace `linux/amd64` by the desired platform (`linux/amd64`, `linux/arm64` etc.).

### Sigstore

[Sigstore](https://docs.sigstore.dev) is trying to improve supply
chain security by allowing you to verify the origin of an
artifcat. You can verify that the image that you use was actually
produced by this repository. This means that if you verify the
signature of the Docker image, you can trust the integrity of the
whole supply chain from code source, to CI/CD build, to distribution
on Maven Central or whever you got the image from.

You can use the following command to verify the latest image using its
sigstore signature attestation:

```bash
cosign verify leplusorg/img --certificate-identity-regexp 'https://github\.com/leplusorg/docker-img/\.github/workflows/.+' --certificate-oidc-issuer 'https://token.actions.githubusercontent.com'
```

The output should look something like this:

```text
Verification for index.docker.io/leplusorg/xml:main --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - The code-signing certificate was verified using trusted certificate authority certificates

[{"critical":...
```

For instructions on how to install `cosign`, please read this [documentation](https://docs.sigstore.dev/cosign/system_config/installation/).

## Request new tool

Please use [this link](https://github.com/leplusorg/docker-img/issues/new?assignees=thomasleplus&labels=enhancement&template=feature_request.md&title=%5BFEAT%5D) (GitHub account required) to request that a new tool be added to the image. I am always interested in adding new capabilities to these images.
