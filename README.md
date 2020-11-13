[![CircleCI](https://circleci.com/gh/RedisLabsModules/redis-docker/tree/master.svg?style=svg)](https://circleci.com/gh/RedisLabsModules/redis-docker/tree/master)
[![Dockerhub](https://img.shields.io/badge/dockerhub-tags-blue)](https://hub.docker.com/r/redisfab/redis/tags/) 

# Redis Docker container

## Images
Docker images generated by this repo named `redisfab/redis:$VERSION-$ARCH-$OSNICK`, where typical parametrized values are:
```
VERSION=5.0.10|6.0.9
ARCH=x64|arm64v8|arm32v7
OSNICK=focal|bionic|xenial|trusty|centos7|stretch|buster
```
Cross-builds generate images named `redisfab/redis-xbuild:$VERSION-$ARCH-$OSNICK`, which in turn allow preforming cross-builds, e.g.:
```
FROM redisfab/redis-xbuild:${VERSION}-${ARCH}-${OSNICK}

RUN [ "cross-build-start" ]

# Build commands

RUN [ "cross-build-end" ]
```

## Building

```sh
$ make help
make [build|publish] [CROSS=1] [X64=1|ARM8=1|ARM7=1] [OSNICK=<nick> | OS=<os>] [VERSION=<ver>] [ARGS...]

build    Build image(s)
publish  Push image(s) to Docker Hub
commons  Build common versions (with DO="<operations>")

Arguments:
CROSS=1          Perform cross-platform builds (typically, ARM7/8 on x64)
OSNICK           buster|stretch|xenial|bionic|centos6|centos7|centos8|fedora30
OS               (optional) OS Docker image name (e.g., debian:buster-slim)
VERSION          Redis version (e.g. 6.0.9)
MASTER=1         Build sources from master branch ("edge" version)
LATEST=1         Build the latest version of branch given by VERSION
TEST=1           Run tests after build
CACHE=0          Build without cache
```
### Building on x64 (native/cross builds)
When building on x64, it's possible to build images for x64 (natively), arm64v8 and arm32v7 (via cross-build).

A typical build/publish session:

```
$ make build publish CROSS=1 OSNICK=bionic VERSION=6.0.9
```

### Native builds

Native builds produce images of architectures that correspond to the build platform's architecture. Such builds always generate `redisfab/redis:$VERSION-$ARCH-$OSNICK` images.

One can use the following Dockerfile excerpt to perform cross-build:

```
FROM redisfab/redis:${VERSION}-${ARCH}-${OSNICK} AS redis
FROM redisfab/xbuild:${ARCH}-${OS} AS builder

RUN [ "cross-build-start" ]

# Build commands

RUN [ "cross-build-end" ] 
```





------
### From original repo:

https://github.com/docker-library/redis

### Maintained by: [the Docker Community](https://github.com/docker-library/redis)

This is the Git repo of the [Docker "Official Image"](https://github.com/docker-library/official-images#what-are-official-images) for [`redis`](https://hub.docker.com/_/redis/) (not to be confused with any official `redis` image provided by `redis` upstream). See [the Docker Hub page](https://hub.docker.com/_/redis/) for the full readme on how to use this Docker image and for information regarding contributing and issues.

The [full image description on Docker Hub](https://hub.docker.com/_/redis/) is generated/maintained over in [the docker-library/docs repository](https://github.com/docker-library/docs), specifically in [the `redis` directory](https://github.com/docker-library/docs/tree/master/redis).

### See a change merged here that doesn't show up on Docker Hub yet?

For more information about the full official images change lifecycle, see [the "An image's source changed in Git, now what?" FAQ entry](https://github.com/docker-library/faq#an-images-source-changed-in-git-now-what).

For outstanding `redis` image PRs, check [PRs with the "library/redis" label on the official-images repository](https://github.com/docker-library/official-images/labels/library%2Fredis). For the current "source of truth" for [`redis`](https://hub.docker.com/_/redis/), see [the `library/redis` file in the official-images repository](https://github.com/docker-library/official-images/blob/master/library/redis).

---

-	[![build status badge](https://img.shields.io/github/workflow/status/docker-library/redis/GitHub%20CI/master?label=GitHub%20CI)](https://github.com/docker-library/redis/actions?query=workflow%3A%22GitHub+CI%22+branch%3Amaster)
-	[![build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/update.sh/job/redis.svg?label=Automated%20update.sh)](https://doi-janky.infosiftr.net/job/update.sh/job/redis/)

| Build | Status | Badges | (per-arch) |
|:-:|:-:|:-:|:-:|
| [![amd64 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/amd64/job/redis.svg?label=amd64)](https://doi-janky.infosiftr.net/job/multiarch/job/amd64/job/redis/) | [![arm32v5 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm32v5/job/redis.svg?label=arm32v5)](https://doi-janky.infosiftr.net/job/multiarch/job/arm32v5/job/redis/) | [![arm32v6 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm32v6/job/redis.svg?label=arm32v6)](https://doi-janky.infosiftr.net/job/multiarch/job/arm32v6/job/redis/) | [![arm32v7 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm32v7/job/redis.svg?label=arm32v7)](https://doi-janky.infosiftr.net/job/multiarch/job/arm32v7/job/redis/) |
| [![arm64v8 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm64v8/job/redis.svg?label=arm64v8)](https://doi-janky.infosiftr.net/job/multiarch/job/arm64v8/job/redis/) | [![i386 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/i386/job/redis.svg?label=i386)](https://doi-janky.infosiftr.net/job/multiarch/job/i386/job/redis/) | [![mips64le build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/mips64le/job/redis.svg?label=mips64le)](https://doi-janky.infosiftr.net/job/multiarch/job/mips64le/job/redis/) | [![ppc64le build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/ppc64le/job/redis.svg?label=ppc64le)](https://doi-janky.infosiftr.net/job/multiarch/job/ppc64le/job/redis/) |
| [![s390x build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/s390x/job/redis.svg?label=s390x)](https://doi-janky.infosiftr.net/job/multiarch/job/s390x/job/redis/) | [![put-shared build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/put-shared/job/light/job/redis.svg?label=put-shared)](https://doi-janky.infosiftr.net/job/put-shared/job/light/job/redis/) |

<!-- THIS FILE IS GENERATED BY https://github.com/docker-library/docs/blob/master/generate-repo-stub-readme.sh -->
