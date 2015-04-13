# Building Images for Scaleway

@moul @aimxhaisse

---

![right](assets/image-board.jpg)

# Who We Are


- BareMetal SSD cloud servers
- Compute C1
	- 4 dedicated ARM cores
	- 2GB memory
	- 50GB SSD Disk
	- 1 public IPv4 address
	- 200Mbits/s unmetered bandwidth

---

# Example of Images

- Base images: Ubuntu, Debian, Fedora, ArchLinux, Gentoo, ...
- App images: Wordpress, OwnCloud, Pydio, LEMP, ...

---

# Our Needs

- Write/Build/Test images
- Encourage contributions

---

# The Docker Way

- we ported base images to armhf
- we inherit from these base images to build apps

---

# Hello World App

```
FROM armbuild/scw-distrib-ubuntu:trusty
RUN /usr/local/sbin/builder-enter
RUN apt-get install -y -qq cowsay
ADD ./patches/ /
RUN /usr/local/sbin/builder-leave
```

---

# Let's Build

## $ make image

Under the hood

- docker build && docker run && docker export
- spawns a C1 instance, export tarball to the volume and snapshot

---

# Pros :ok_hand:

## can port existing images from community

```
sed -i 's/^FROM .*$/FROM armbuild/scw-distrib-ubuntu:trusty/' Dockerfile
```

---

# Pros :ok_hand:

## benefit from Docker features

- inheritance: images apps are simple and concise
- cache: we can incrementally build our images

---

# Pros :ok_hand:

## easy to contribute

```
$EDITOR Dockerfile && git commit -am 'Added cool feature.'
```

---

# Cons

- no official support of Docker on ARM
- some applications aren't ARM-ready
- no crossbuild

---

# Questions?