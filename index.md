---
layout: default
title: Home
nav_order: 1
description: "Kattlo gives a way to manage topics, ACLs, users, schemas, ksqlDB, employing a evolutionary configuration. Easy to understand, easy to write and easy to apply."
permalink: /
---

# Apache Kafka® configuration made easy
{: .fs-9 }

Kattlo gives a way to manage topics, ACLs, users, schemas, ksqlDB, employing a
evolutionary configuration. Easy to understand, easy to write and easy to apply.
{: .fs-6 .fw-300 }

[Get started now](#getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on GitHub](https://github.com/kattlo/kattlo-cli){: .btn .fs-5 .mb-4 .mb-md-0 }

---

## Getting started

### Install Kattlo

```bash
curl 'https://github.com/kattlo/kattlo-cli/releases/download/v0.1.1/kattlo-v0.1.1-linux' \
  -o 'kattlo'

sudo chmod +x kattlo
sudo mv kattlo /usr/local/sbin/kattlo
```

- [See installation options]({{ site.baseurl }}{% link docs/installation.md %})

### Initialize new project directory

```bash
kattlo init --directory='/path/to/initialize'
```

### Generate new migration file

```bash
kattlo gen migration \
  --resource=TOPIC \
  --diretory='/path/to/migration'
```

### Apply the migration

```bash
kattlo \
  --config-file='/path/to/.kattlo.yaml' \
  --kafka-config-file='/path/to/kafka.properties' \
  topic \
  --directory='/path/to/migrations'
```

- [See configuration options]({{ site.baseurl }}{% link docs/configuration.md %})

---

## About the project

Kattlo is &copy; 2020-{{ "now" | date: "%Y" }} by [Fábio José](https://github.com/fabiojose).

### License

Kattlo is distributed by an [Apache 2.0](https://github.com/kattlo/kattlo-cli/blob/main/LICENSE).

### Contributing

When contributing to this repository, please first discuss the change you wish to make via issue,
email, or any other method with the owners of this repository before making a change. Read more about becoming a contributor in [our GitHub repo](https://github.com/kattlo/kattlo-cli#contributing).

### Code of Conduct

Kattlo is committed to fostering a welcoming community.

[View our Code of Conduct](https://github.com/kattlo/kattlo-cli/tree/main/CODE_OF_CONDUCT.md) on our GitHub repository.
