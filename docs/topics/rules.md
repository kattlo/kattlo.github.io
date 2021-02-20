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

_First_ you must declare your Topic rules in `.kattlo.yml`.

__Example with human readable notation:__

- [See human readable options]({{ site.baseurl }}{% link docs/configuration.md %})
- [See full examples of rules](https://github.com/kattlo/kattlo-cli/tree/main/examples/topic/rules)

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
      min.cleanable.dirty.ratio:
        '>=': 1%
```

__Example with machine readable notation:__

- [See full examples of rules](https://github.com/kattlo/kattlo-cli/tree/main/examples/topic/rules)

```yaml
rules:
  topic:
    namePattern: '^[a-z0-9\-]{1,255}$'
    partitions:
      '>=': 3
    replicationFactor:
      '==': 2
    config:
      flush.messages:
        in:
        - 1
        - 10
        - 100
        - 1000
        - 9223372036854775807
      max.message.bytes:
        '<=': 921600
      segment.ms:
        '>=': 7200000
      retention.ms:
        '<=': 1209600000
      min.cleanable.dirty.ratio:
        '>=': 0.01
```

And then run the kattlo to enforce rules during the topic migration,
pointing to you `.kattlo.yaml`:

```bash
kattlo \
  --config-file='/path/to/.kattlo.yaml' \
  --kafka-config-file='/path/to/kafka.properties' \
  topic \
  --directory='/path/to/migrations'
```

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

- [See human readable options]({{ site.baseurl }}{% link docs/configuration.md %})