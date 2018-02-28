---
title: Machine Learning and FreeNAS
---

**TL;DR:** I have finally found a reasonable way of conducting machine learning
"research" with the help of my FreeNAS.

---

I have been trying all sorts of ways to install TensorFlow (and
Keras) on my FreeNAS.
There is AFAIK *one* guide (of which there are several derivatives) for [How to
install TF on BSD](https://ecc-comp.blogspot.se/2016/06/tensorflow-on-freebsd.html).
Unfortunately, it still seems to be impossible to get `Python 3` to work with
BSD, why I opted to find another solution.

# FreeNAS, DockerVM and Rancher

Lately, FreeNAS has added support for `DockerVM`. Unlike regular VMs (which I
also thought about using, but found [THIS
POST](https://forums.freenas.org/index.php?threads/how-to-boot-ubuntu-desktop-vm-in-uefi-mode.53863/)
and was discouraged) `DockerVM` is simply a VM containing only
[Docker](https://www.docker.com/what-docker).
In addition to this, the FreeNAS docs also suggests one installs
[Rancher](https://doc.freenas.org/11/vms.html#docker-rancher-vm), a management
platform for containers.

I would suggest you simply follow the steps outlined in the [FreeNAS
docs](https://doc.freenas.org/11/vms.html#docker-rancher-vm) in order to get up
and running.

# TensorFlow and Keras

*This is still WIP as I want to find a way of "commiting" programs to be run on
my server. As for now, I use Jupyter.*

When you have your RancherUI VM and an additional host where you plan on running
your machine learning container, it is time to find a suitable docker image.
As for now, the best image I have found is a manipulated version of
`gw000/keras:2.1.3-py3-tf-cpu`, to which I have added Jupyter support.
The original Dockerfile can be found [on
GitHub](https://github.com/gw0/docker-keras/blob/2.1.3/Dockerfile.py3-tf-cpu)
and my modified version can be found
[HERE]({{site.url}}/download/Dockerfile.keras-jupyter-cpu).

In order to build your image you must download the Dockerfile and build it.

    wget erikthorsell.github.io/download/Dockerfile.keras-jupyter-cpu
    docker build -t debian:keras .

`-t debian:keras` tags the image and `.` is the directory where the Dockerfile
resides (current directory).

When your image is built you can use `docker run` to start the container as:

    docker run -d -p 8888:8888 -v $(pwd):/srv gw000/keras-full

which will start the Jupyter web if on `http://<server-ip>:8888/` with password
`keras`.
Notebooks stored in the current directory will be mapped to `/srv`.

---

Good luck approaching the singularity.
