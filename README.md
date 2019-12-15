# Images

Docker container to manipulate images (imagemagick, exiftool...).

## Example without using the filesystem

Let's say that you have an image `foo.jpg` in your current working directory that you want to extract its metadata:

### Mac/Linux

```
cat foo.jpg | docker run --rm -i --net=none thomasleplus/img identify -
```

### Windows

```
type foo.jpg | docker run --rm -i --net=none thomasleplus/img identify -
```

## Example using the filesystem

Same thing, assuming that you have an image `foo.jpg` in your current working directory that you want to extract its metadata:

### Mac/Linux

```
docker run --rm -t --user="$(id -u):$(id -g)" --net=none -v "$(pwd):/tmp" thomasleplus/img identify /tmp/foo.jpg
```

### Windows

In `cmd`:

```
docker run --rm -t --net=none -v "%cd%:/tmp" thomasleplus/img identify /tmp/foo.jpg
```

In PowerShell:

```
docker run --rm -t --net=none -v "${PWD}:/tmp" thomasleplus/img identify /tmp/foo.jpg
```

## Help

To know more command line options of one of the imagemagick command:

```
docker run --rm --net=none thomasleplus/img identify -help
```

## Request new tool

Please use [this link](https://github.com/thomasleplus/docker-img/issues/new?assignees=thomasleplus&labels=enhancement&template=feature_request.md&title=%5BFEAT%5D) to request that a new tool be added to the image. I am always interested in adding new capabilities to these images.
