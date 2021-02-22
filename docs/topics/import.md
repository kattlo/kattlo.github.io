---
layout: default
title: Import
parent: Topics
---

# Import Existing Topics
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

See how to import existing topics as a managed asset with Kattlo.

## Importing

To import existing topics to Kattlo, run the command bellow:

```bash
kattlo \
  --config-file='/path/to/.kattlo.yaml' \
  --kafka-config-file='/path/to/kafka.properties' \
  --bootstrap-servers='my.kafka:9092' \
  topic \
  --directory='/path/to/migrations/for/my/existing/topic' \
  import \
  --topic='my-existing-topic-name'
```

The operation above will import the existing topic, create the very first
migration with create operation and the necessary stuff to enable that
topic as a managed asset.

And the file `v0001_create-topic.yaml`will be automatically created in the
folder defined by `--directory` option.

