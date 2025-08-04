# CMake Buildpack

This is a Cloud Native Buildpack that adds support for building CMake based projects.

## Example Usage

Build dependencies need to be satisfied with another buildpack e.g. by using `Aptfile`.

Example `Aptfile`:
```
build-essential
libconfig++-dev
```

This pack will then handle installing `CMake` and executing the build.

## Development usage

Setup the images
```
pack config default-builder tools-harbor.wmcloud.org/toolforge/heroku-builder:22
pack config trusted-builders add tools-harbor.wmcloud.org/toolforge/heroku-builder:22
```

Download the example app:
```
git -C .. clone https://github.com/InfraBits/hello-world-cmake.git
```

Download the hacked apt buildpack:
```
git -C .. clone https://gitlab.wikimedia.org/repos/cloud/toolforge/buildpacks/apt-buildpack.git
```

Execute a build targeting the example app, using this build pack:
```
pack build --path ../hello-world-cmake --buildpack ../apt-buildpack --buildpack . hello-world-cmake-app
```
