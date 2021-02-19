---
layout: default
title: Rules
parent: Topics
---

# Topic Rules
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

Enforce rules to perform consistent topic configuration changes.

## Rules

Apache Kafka® is awesome, but with wrong configurations we may loose data or
impact the cluster performance. Thinking about that and about patterns, Kattlo
has a way to enforce rules before apply Topic migrations.

First you must declare your Topic rules in `.kattlo.yml`.

__Example with human readable notation:__

```yaml
rules:
  topic:
    namePattern: '^[a-z0-9\-]{1,255}$'
    partitions:
      '>=': 3
    replicationFactor:
      '==': 2
    config:
      compression.type:
        '!in':
        - zstd
        - gzip
      delete.retention.ms:
        '>': 60minutes
      file.delete.delay.ms:
        '<=': 59seconds
      flush.messages:
        in:
        - 1
        - 10
        - 100
        - 1000
        - 9223372036854775807
      index.interval.bytes:
        '<=': 1MiB
      max.message.bytes:
        '<=': 900KiB
      min.in.sync.replicas:
        '>=': 2
      message.timestamp.type:
        '==': LogAppendTime
      segment.ms:
        '>=': 2hours
      retention.ms:
        '<=': 14days
      max.compaction.lag.ms:
        '<=': 7days
      min.cleanable.dirty.ratio:
        '>=': 1%
```

__Example with machine readable notation:__

```yaml
rules:
  topic:
    namePattern: '^[a-z0-9\-]{1,255}$'
    partitions:
      '>=': 3
    replicationFactor:
      '==': 2
    config:
      compression.type:
        '!in':
        - zstd
        - gzip
      delete.retention.ms:
        '>': 3600000
      file.delete.delay.ms:
        '<=': 59000
      flush.messages:
        in:
        - 1
        - 10
        - 100
        - 1000
        - 9223372036854775807
      index.interval.bytes:
        '<=': 1048576
      max.message.bytes:
        '<=': 921600
      min.in.sync.replicas:
        '>=': 2
      message.timestamp.type:
        '==': LogAppendTime
      segment.ms:
        '>=': 7200000
      retention.ms:
        '<=': 1209600000
      max.compaction.lag.ms:
        '<=': 604800000
      min.cleanable.dirty.ratio:
        '>=': 0.01
```

## Available Notations for Human Readable

- topic name regex pattern
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

## Available Conditions

- `'=='`: equals
- `'!='`: not equals
- `'>'`: greater
- `'>='`: greater or equals
- `'<'`: less
- `'<='`: less or equals
- `'in'`: in a list of values 
- `!in`: not in a list of values

## Limitations of Human Readable

In the current version, lists (`'in'` and `'!in'`), `partitions` and
`replicationFactor` does not support human readable values.
