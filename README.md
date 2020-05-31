[![Docker Build Status](https://img.shields.io/docker/cloud/build/makisyu/texlive-2020.svg)](https://hub.docker.com/r/makisyu/texlive-2020/)

# Dockerfile for TeX Live 2020

This is a Dockerfile repository of TeX Live 2020 with a scheme-full profile. (Almost) monthly updated.

# Usage

A path to TeX Live scripts and binaries (`/usr/local/texlive/2020/bin/x86_64-linux`) is already added to `$PATH`.

```
$ docker run --rm -i -t makisyu/texlive-2020 platex
```

Most users want to add a volume that contains source codes and change the working directory to it.

```
$ docker run --rm --volume $PWD:/workdir --workdir /workdir makisyu/texlive-2020 platex main.tex
```

Docker volume is mounted as `uid=1000,gid=1000` (In most cases, these ids mean `root:root`.), and files in the directories are owned by root. Adding `--user` option is a good idea.

You should use uid/gid instead of user/group names because, in the container, `/etc/passwd` doesn't contain your user/group names. If you use `uid:gid`, the container creates files as specified `uid:gid` without reading `/etc/passwd`.

```
$ docker run --rm --volume $PWD:/workdir --workdir /workdir --user 1001:1001 makisyu/texlive-2020 platex main.tex
```

`latexmk`? Yes, it's very useful, and a scheme-full profile includes a huge collection of other useful tools.

```
$ ls -a
.latexmkrc main.tex
$ docker run --rm --volume $PWD:/workdir --workdir /workdir --user 1001:1001 makisyu/texlive-2020 latexmk
```

This image is based on `fedora:latest` docker image. The login shell and other basic utilities are always available, and you can run a shell script, perl, etc.

```
$ docker run -i -t --rm --volume $PWD:/workdir --workdir /workdir --user 1001:1001 makisyu/texlive-2020 /usr/bin/bash
[root@20629bec6417 workdir]# perl -v
[root@20629bec6417 workdir]# python3 -V
```

# Image is too large.
Ooops. I know!
