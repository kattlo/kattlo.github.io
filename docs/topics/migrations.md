---
layout: default
title: Migrations
parent: Topics
---

# Topic Migrations
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

This is the Kattlo's way to manage topics lifecycle.

## Migrations

### Create

To __create__ a topic:

```yaml
operation: create # The operation over the resource
notes: |
  Write down whatever you want to describe this.
  This can be a multiline text . . .
topic: topic_name
partitions: 1 #partitions is optional
replicationFactor: 1 #replicationFactor is optional
config: #config is optional
  compression.type: gzip
  cleanup.policy  : compact
  # Any configuration available here:
  #   https://kafka.apache.org/documentation/#topicconfigs
```

Notes about `create`:
- if you want cluster default values for `partitions`, `replicationFactor`
and `config`, just suppress them.

### Patch

To __patch__ a topic:

```yaml
operation: patch # The operation over the resource
notes: Patch partitions to 3 # Describe your patch . . .
topic: 02_create_patch_partitions # Topic that was created before
partitions: 3 #partitions is optional
replicationFactor: 2 #replicationFactor is optional
config: #config is optional
  retention.ms: -1
  # Any configuration available here:
  #   https://kafka.apache.org/documentation/#topicconfigs

  compresstion.type: $default # Patch to cluster default value
```

Notes about `patch`:
- `partitions` can not be reduced
- at least one of `partitions`, `replicationFactor` or `config` must be present
in the migration file
- use the keyword `$default` to patch config to cluster default value

### Remove

To __remove__ a topic:

```yaml
operation: remove
notes: Descrive your motivation to remove this topic
topic: 05_create_and_remove # Topic to remove
```

Notes about `remove`:
- remove will delete the entire topic data
- all migrations history about the topic will be maintained
