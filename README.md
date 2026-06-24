# CyberShake Data Access Tutorial
Dockerfile to build image for executing [cs-data-tools](https://github.com/SCECcode/cs-data-tools)
Docker images hosted at https://hub.docker.com/r/sceccode/cs_data_tutorial

[CyberShake Data Access Tool Tutorial](https://docs.google.com/document/d/1J1ou1rqpbdSexcheT22jt_XzXq6uFMumDImMGADbi1g/edit?tab=t.0)

## Dockerfiles

* Dockerfile: The file used for the latest image
  * Image https://hub.docker.com/layers/sceccode/cs_data_tutorial/20260608/
  * Manifest Digest "sha256:4f838adc7181d9039ac795a7d0aba05a9bd9ecd480d294483169c5def983b64d"
  * Created "2026-06-08T06:20:45.462900094Z"

* Dockerfile-20230510: Original dockerfile
  * Image https://hub.docker.com/layers/sceccode/cs_data_tutorial/20230510/
  * Manifest Digest "sha256:35bd277b9cf24af7d1dcbfdbbb45fa6fde4abc05908cba823b22b02c76dbafad"
  * Created "2023-05-10T18:40:34.440921312Z"

## Building
Execute from within this git repository.
```
# Create a new builder instance with docker-container driver
# This driver supports multiple platforms via QEMU emulation
docker buildx create --name multiarch --driver docker-container --bootstrap

# Set the new builder as the default
docker buildx use multiarch

# Verify supported platforms (should show amd64, arm64, arm/v7, etc.)
docker buildx inspect multiarch

docker buildx build \
             --platform linux/amd64,linux/arm64 \
             --build-arg APP_UNAME=cs_data_user \
             --build-arg APP_GRPNAME=staff \
             --build-arg APP_UID=503 \
             --build-arg APP_GID=20 \
             --build-arg BDATE=$(date +%Y%m%d) \
             --tag sceccode/cs_data_tutorial:latest \
             --tag sceccode/cs_data_tutorial:$(date +%Y%m%d) \
             --push .
```

## Sources
* https://oneuptime.com/blog/post/2026-01-06-docker-multi-architecture-images/view
