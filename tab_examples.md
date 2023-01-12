---
title: Examples
layout:  null
tab: true
order: 1
tags: examples
---

## Setup

Patton, in its current version, is a shell script that orchestrates the
available tools to search for vulnerabilities in order to be run it needs the
following dependencies:

- zstd
- Docker
- Patton database

## Install

After installing the dependencies run the following commands in order to finish
the installation.

```bash
$ wget https://github.com/OWASP/Patton/releases/download/latest/patton.db.zst
$ wget https://github.com/OWASP/Patton/raw/develop/bin/patton
$ install patton /usr/local/bin/patton
```

By default Patton looks for its database in the current directory, if not the
`-d` option flag can be used to give it the database location.

## Examples

### Usage

```bash
$ patton --help
Usage: patton [OPTION]... [PATTERN]
Try '/usr/local/bin/patton -h|--help' for more information
  -h, --help           display this help text and exit
  -V, --version        display version information and exit
  -d, --database-file  path to database file
  -t, --search-type    type of search to execute: product|pkg_debian|pkg_ubuntu|fulltext
  -s, --search-subtype for search-type:(debian|ubuntu), sets the suite
    e.g.: buster, potato, fossa, xenial, precise, trusty...
  -v, --pkg-version    cpe version when searching by cpe
  -n, --pkg-name       path to database file
  -w, --pkg-vendor     path to database file
```

### Search for vulnerabilities in a Debian system

```bash
patton -t pkg_debian < /var/lib/dpkg/status
```

### Search for vulnerabilities in an Ubuntu system

```bash
patton -t pkg_ubuntu < /var/lib/dpkg/status
```

### Search for vulnerabilities in a Red Hat Enterprise Linux

```bash
patton -t pkg_rhel
```

**NOTE**: Have to be run on RHEL 8 or newer

### Search for vulnerabilities with a free-format string

```bash
patton -d patton.db.zst -t fulltext openssl
```
