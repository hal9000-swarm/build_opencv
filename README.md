# OpenCV build script

This script builds OpenCV from source on Tegra (Nano, NX, AGX, etc.) or for Nvidia desktop GPUs.

Related thread on Nvidia developer forum 
[here](https://devtalk.nvidia.com/default/topic/1051133/jetson-nano/opencv-build-script/).

[How it Works](https://wiki.debian.org/QemuUserEmulation)
Alternatively just build on a Xavier (takes about an hour).

## Usage:
```shell
./build_opencv_[tegra|gpu].sh
```

## Notes:

The scripts set the relevant compute capability targets to be included. For a list of Nvidia products see: https://developer.nvidia.com/cuda-gpus

Summary:
* PTX (Intermediate format) is disabled.
* CUDNN Version is set to 8
* Supported platforms are marked by *

# Desktop GPUs
- Fermi   2.0
- Kepler  3.0;3.5;3.7
- Maxwell 5.0;5.2
- Pascal  6.0;6.1 *
- Volta 7.0 *
- Turing 7.5 *
- Ampere  8.0;8.6 *

# Jetson 
- Jetson AGX Xavier	7.2 *
- Jetson Nano	5.3 *
- Jetson TX2	6.2 *
- Jetson TX1	5.3 *
- Tegra X1	5.3 *

## Specifying an OpenCV version (git branch)
```shell
./build_opencv[tegra|gpu].sh 4.4.0
```

Where `4.4.0` is any version of openCV from 2.2 to 4.4.0
(any valid OpenCV git branch or tag will also attempt to work, however the very old versions have not been tested to build and may require spript modifications.).

**JetPack 4.4 / Jetson NOTE:** the minimum version that will build correctly on JetPack 4.4 GA is 4.4.0. Prior versions of JetPack may need the CUDNN version adjusted (the `-D CUDNN_VERSION='8.0'` line can simply be removed).

**Package**
It requires the following steps:
- sudo make install
- sudo make package
- sudo make uninstall

The reason is, that the package build references some files by their expected symlinks after installation.
