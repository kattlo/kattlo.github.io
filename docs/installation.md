---
layout: default
title: Installation
nav_order: 2
---

# Installation
{: .no_toc }


Run Kattlo natively in Linux, MacOS and Windows.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Linux Binary

```bash
curl 'https://github.com/kattlo/kattlo-cli/releases/download/v0.2.1/kattlo-v0.2.1-linux' \
  -o 'kattlo'

sudo chmod +x kattlo
sudo mv kattlo /usr/local/sbin/kattlo
```

## Linux Packages

The are `.deb` and `.rpm` packages available. Do a check in
[the latest release](https://github.com/kattlo/kattlo-cli/releases/latest).

## MacOS

```bash
curl 'https://github.com/kattlo/kattlo-cli/releases/download/v0.2.1/kattlo-v0.2.1-mac' \
  -o 'kattlo'

sudo chmod +x kattlo
sudo mv kattlo /usr/local/bin/kattlo
```

## Windows

- download the [latest release](https://github.com/kattlo/kattlo-cli/releases/latest) package for windows
- unzip it
- copy `VCRUNTIME140.dll` to `C:\Windows\System32\`
- get the absolute path to that unzipped directory
- add the absolute path of Kattlo to your `PATH` environment variable
- open the prompt and type: `kattlo -V`

