# docker-android-rn-build
Docker image for automated Android builds and distribution with nodejs & volta, fastlane, gradle, ImageMagick, jq

## Usage

Simply run the container and mount your project to the `/app` folder, then run `fastlane` commands as you usually do.

```
$ docker run --rm -v \ 
  ${PWD}:/app \ 
  davidgovea/docker-android-rn-build \
  bundle exec fastlane [lane]
```

## Docker hub link

https://hub.docker.com/r/davidgovea/docker-android-rn-build

## What Is Inside

Built upon the `:latest` branch of the great [`runmymind/docker-android-sdk/`](https://hub.docker.com/r/runmymind/docker-android-sdk/) image. In addition it installs `ruby`, the latest `fastlane`, `bundle` (fast execution of fastlane), [jq](https://github.com/stedolan/jq), [ripgrep](https://github.com/BurntSushi/ripgrep), [fd](https://github.com/sharkdp/fd), ImageMagick and `gradle 6.5.1`.

## Inspired by

https://hub.docker.com/r/opengamer/android-sdk-gradle-fastlane but with new version of `gradle`, and extra utilities
