---
layout: default
title: Examples
parent: Topics
---

# Examples
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

Examples of how to use topic migrations.

## Command Examples

> All examples are based on these [file examples](https://github.com/kattlo/kattlo-cli/tree/main/examples)

Set the directory with migrations using the `--directory` option:
```bash
kattlo \
  --config-file='examples/.kattlo.yaml' \
  --kafka-config-file='examples/kafka.properties' \
  topic \
  --directory='examples/topics/01_create_with_config'
```

Directory with migrations will be default to current, when `--directory` is
suppressed:
```bash
kattlo \
  --config-file='examples/.kattlo.yaml' \
  --kafka-config-file='examples/kafka.properties' \
  topic
```

The current directory contains `kafka.properties` and `.kattlo.yaml`:
```bash
kattlo \
  topic \
  --directory='examples/topics/01_create_with_config'
```

Want to use the `kafka.properties`, but in another cluster:
```bash
kattlo \
  --config-file='examples/.kattlo.yaml' \
  --kafka-config-file='examples/kafka.properties' \
  --bootstrap-servers='my.kafka:9092' \
  topic \
  --directory='examples/topics/01_create_with_config'
```

The option `--bootstrap-servers` overrides the config
[`bootstrap.servers`](https://kafka.apache.org/documentation/#adminclientconfigs_bootstrap.servers).

Showing topic current state:

> Include the option `--format=JSON` to printout json instead plain text

```bash
kattlo \
  --config-file='examples/.kattlo.yaml' \
  --kafka-config-file='examples/kafka.properties' \
  info --resource=TOPIC \
  '<topic-name>'
```

Showing topic history:

> Include the option `--format=JSON` to printout json instead plain text

```bash
kattlo \
  --config-file='examples/.kattlo.yaml' \
  --kafka-config-file='examples/kafka.properties' \
  info --resource=TOPIC --history \
  '<topic-name>'
```

## File Examples

- [See many examples of migration files](https://github.com/kattlo/kattlo-cli/tree/main/examples/topic)

### Human Readable to Create a Topic

```yaml
operation: create
notes: |
  This is a multiline
  notes about 
topic: my-topic-name
config:
  compression.type: gzip
  cleanup.policy  : compact
  segment.bytes: 900MiB
  max.compaction.lag.ms: 2days
  delete.retention.ms: 10minutes
  flush.ms: 12hours
```

### Human Readable to Path a Topic

```yaml
operation: patch
notes: Add new configurtions
topic: 10_human_readable
config:
  delete.retention.ms: 0
  max.message.bytes: 950KiB
  retention.ms: 2days
  message.timestamp.type: LogAppendTime
```