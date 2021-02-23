---
layout: default
title: Best Practices
nav_order: 4
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


## Best Practices

- Always create a new migration file and never change an applied one
- Create a directory for each resource that you want to manage
  - Kattlo is able to process many distinct resources migrations within same
    directory, but you get better organization following that practice

## File Naming

All migrations are defined using physical files, and they must follow
this naming pattern:

- `v[0-9]{4}_[\\w\\-]{0,246}\\.ya?ml`

Simplifing:

- `v0000_the-name-of-my-migration.yaml`
- where `v0000` will be the version of resource migration, from `1` to `n`
- when a new migration is created, increase the version

## File Content

Every migration file must have exatcly one resource migration.

Never mix `create`, `patch` or `remove` in the same file or same operations
for distinct resources.