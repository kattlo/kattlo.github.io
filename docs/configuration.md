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

## Initialization

To initialize new Kattlo project you just run the following command:

```bash
kattlo init --directory='/path/to/initialize'
```

Use the `--bootstrap-servers` to generate the Kattlo config
with right Kafka addresses:

```bash
kattlo --bootstrap-servers='my-kafka-b1:9092,my-kafka-b2:9092' \
  init --directory='/path/to/initialize'
```

> If you suppress the `--directory` option, the current folder will be
initialized.

## Available Notations for Human Readable

- name regex pattern
  - [Java Pattern](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/regex/Pattern.html)
- time: transformed to millis
  - `seconds` or `second`
  - `minutes` or `minute`
  - `hours` or `hour`
  - `days` or `day`
- size: transformed to bytes
  - `KiB`
  - `MiB`
  - `GiB`
- math: transformed to floating point number between `0` and `1`
  - `%`

> For bytes Kattlo uses the [quibibyte notation](https://en.wikipedia.org/wiki/Byte#Multiple-byte_units)

__Examples__:

- `1day` will be transformed in `86400000` milliseconds
- `2seconds` in `2000` milliseconds
- `1hour` in `3600000` milliseconds
- `1KiB` in `1024` bytes
- `50%` in `0.5`

## `--config-file`

Relative or absolute path to Kattlo's configuration file.

In the `.kattlo.yaml` configuration file you may define the following
properties or use the [init command](#initialization) to generate it.

Example of `.kattlo.yaml`

```yaml
rules:
  topic:
    namePattern: 'your pattern'
    # more rules constraints...
```

- [See a full example of .kattlo.yaml](https://github.com/kattlo/kattlo-cli/blob/main/examples/topic/rules/human/.kattlo.yaml)

## `--kafka-config-file`

Relative or absolute path to Apache Kafka® configuration file used by
Kattlo to perform Admin, Producer and Consumer operations.

> Created by [init command too](#initialization)

You may put the properties described at
[official documentation](https://kafka.apache.org/documentation/#adminclientconfigs).

Example of `kafka.properties`:

```properties
bootstrap.servers=localhost:19092,localhost:29092
client.id=kattlo-cli
```