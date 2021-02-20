---
layout: default
title: Configuration
nav_order: 2
---

# Configuration
{: .no_toc }

With Kattlo you are able to use human readable notation to declare resources
migrations and rules.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Available Notations for Human Readable

- name regex pattern
  - [Java Pattern](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/regex/Pattern.html)
- time: trasformed to millis
  - `seconds`
  - `minutes`
  - `hours`
  - `days`
- size: transformed to bytes
  - `KiB`
  - `MiB`
  - `GiB`
- math: transformed to floating point number between `0` and `1`
  - `%`

__Examples__:

- `1day` will be transformed in `86400000` milliseconds
- `2seconds` in `2000` milliseconds
- `1hour` in `3600000` milliseconds
- `1KiB` in `1024` bytes
- `50%` in `0.5`

