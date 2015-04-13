footer: *while42* Paris #13 *(14/04/14)* - by [@moul](https://twitter.com/moul) & [@aimxhaisse](https://twitter.com/aimxhaisse)
slidenumbers: true

# [fit] Building images for **Scaleway**

![](assets/image-board.jpg)

---

![](assets/image-board.jpg)
![right fit](assets/node.png)

# Who We Are

- BareMetal SSD cloud servers
- Compute C1
  - 4 dedicated ARM cores
  - 2GB memory
  - 50GB SSD Disk
  - 1 public IPv4 address
  - 200Mbits/s unmetered bandwidth

---

![](https://www.youtube.com/watch?v=XFhgSKNJP2s)

---

# Example of images

- *distrib images*: Ubuntu, Debian, Fedora, Arch Linux, Gentoo, Alpine Linux ...
- *1-Click apps*: Docker, Wordpress, OwnCloud, Pydio, LEMP, Python, Node.js ...

--

*coming soon*: community images

![right fit](assets/imagehub.png)

---

# Our Needs

- *write*/*build*/*test*/*commit* images
- Encourage *contributions*

---

# The Docker Way

1. inherit from a Docker image
  *FROM my-arm-image*
2. customize
  *RUN apt-get install ...*
3. convert it to a Scaleway image
  *$ make build*

![right zoom=100%](assets/docker-image-to-scaleway-image.png)

---

# *Hello World* Dockerfile

```bash
# Inherit from the Ubuntu Trusty Scaleway image
FROM armbuild/scw-distrib-ubuntu:trusty

# Install the `cowsay` package
RUN apt-get install -y -qq cowsay

# Add local assets
COPY ./patches/ /
```

![right fit](assets/image-helloworld.png)

---

![right fit](assets/make-build.png)

# Let's Build

### `$ make build`

```bash
docker build && docker run && docker export
```
- spawns a C1 instance, export tarball to the volume and snapshot

---

# Advanced: Port a base image (i.e. distrib)

1. port a Docker image to *ARMHF*[^1]
2. enable init scripts[^2]
3. `$ make build`
4. `$ make release`

[^1]: to list the ported Docker images, run: `docker search armbuild/`

[^2]: Docker images aren't built to run systems, but apps -- we need to (re-)enable init scripts

---

# Pros :ok_hand:

### can port existing images from community

```bash
sed -i 's/^FROM .*$/FROM armbuild/scw-distrib-ubuntu:trusty/' Dockerfile
```

---

![right fit](assets/make-help.png)

# Pros :ok_hand:

### benefit from *Docker*/*Dockerfile* features

- *inheritance*: images apps are simple and concise
- *caching*: incrementally build images
- *debug*: drop a shell in the future image thanks to `docker run`
- *pull/push*: sources are on GitHub, builds are on registries

---

![fit right](assets/github-app-docker.png)

# Pros :ok_hand:

### easy to contribute

- *Dockerfile* is a known standard
- **sources** & **issues** are on *GitHub*

```
$ nano Dockerfile
$ git commit -am 'Added cool feature. :neckbeard:'
```

---

# Cons

- no official support of Docker on ARM
- some applications aren't ARM-ready
- no crossbuild

---

# Questions?

scaleway.com
github.com/scaleway
twitter.com/scaleway
