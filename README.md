# Tensorflow Build

## Local Builds on Docker or Podman

### 1\. create the build Image

```
docker build --build-arg BAZEL_VERSION=0.24.1 --build-arg DEV_TOOLSET_VERSION=7 \
--build-arg PIP_LIST="wheel==0.31.1 setuptools==39.1.0 six==1.12.0 absl-py protobuf==3.6.1 enum34 futures mock numpy pixiedust pillow pyaml keras_applications==1.0.8 keras_preprocessing==1.0.5 tf-estimator-nightly" \
--build-arg PYTHON_VERSION=3.6 -t manylinux_tf_build -f Dockerfile.centos6 .
```

### 2\. edit the build env file

```
vim tf_env_v2.0
```

### 3\. start the bazel build in the build Image container

```
docker run -it -u 0 --env-file ./tf_env_v2.0 -v $(pwd):/tmp/build_pip_package:Z manylinux_tf_build /usr/libexec/s2i/manylinux2010
```
