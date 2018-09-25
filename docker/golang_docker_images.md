<html><link rel="stylesheet" href="../assets/css/air.css"></html>

[Home](../index.html)

## Building GoLang Docker Images

##### Basic Dockerfile.Scratch

```dockerfile
FROM scratch
ADD $project /
CMD ["/$project"]
```

##### Dockerfile.Scratch with HTTPS support

```dockerfile
FROM scratch
ADD curl-ca-bundle.crt /etc/ssl/certs/
ADD $project /
CMD ["/$project"]
```

##### Go build with ARM architecture (required for Scratch OS base)

```shell
GO_ENABLED=0 GOARM=7 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -o $project .
```

##### Create and tag the image locally

```bash
docker build -t $project -f Dockerfile.scratch .
```

##### Run the image locally to test

```shell
docker run -it tagname 
```

##### Tag the image for upload to Docker Cloud

```shell
docker tag $project:$version vflagr/$project:$version

e.g
docker tag docker-testing:latest vflagr/docker-testing:latest
```

##### Push the image to Docker Cloud

```shell
docker push vflagr/$project
```

##### Pull the image from Docker Cloud

```shell
docker pull vflagr/$project:$version
```

##### Run the pulled version of the image

```shell
docker run -it vflagr/$project
```