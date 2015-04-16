footer: [@scaleway](https://twitter.com/scaleway) Meetup *(16/04/14)* - by [@moul](https://twitter.com/moul) & [@aimxhaisse](https://twitter.com/aimxhaisse)
slidenumbers: true

# [fit] Building images for **Scaleway**

![](assets/image-board.jpg)

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

# Docker

- a Dockerfile describes the image
- docker build creates an image from a Dockerfile
- Docker containers can be started with the image

---

# Workflow

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

- docker build, run, export

### `$ make image`

- spawns a C1 instance, export tarball to the volume and snapshot

---

# Pros :ok_hand:

### can port existing images from community[^1]

```bash
sed -i 's/^FROM .*$/FROM armbuild/scw-distrib-ubuntu:trusty/' Dockerfile
```

[^1]: github.com/moul/port-docker-image

---

![right fit](assets/make-help.png)

# Pros :ok_hand:

### benefit from *Docker*/*Dockerfile* features

- *inheritance*: images apps are simple and concise
- *caching*: incrementally build images
- *debug*: drop a shell in the image thanks to `docker run`
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

{twitter,github}.com/moul <m@42.am>
{twitter,github}.com/aimxhaisse <mxs@sbrk.org>
