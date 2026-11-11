<h1 align="center">Rudra Narayan Panda</h1>

<p align="center">
  <b>Backend engineer who makes systems faster, cheaper, and harder to break.</b><br>
  <sub>Go · Rust · AWS · Distributed systems</sub><br>
  <sub>SWE L2 @ ASBL · Hyderabad</sub>
</p>

<p align="center">
  <a href="https://linkedin.com/in/0xrnp">LinkedIn</a> ·
  <a href="https://x.com/debuggingpanda">X</a> ·
  <a href="https://github.com/0xrnp/dotfiles">Dotfiles</a> ·
  <a href="https://leetcode.com/u/0xrnp/">LeetCode</a>
</p>

```text
RNP(1)                  Systems & Backend Manual

NAME
    0xrnp - latency hunter, terminal minimalist

DESCRIPTION
    Builds high-throughput Go microservices and distributed
    cloud infrastructure. Started in chemistry, pivoted to
    computer applications, now obsessed with storage engines,
    write paths, and cutting database bills without touching
    latency.

ENVIRONMENT
    Rex + Neovim

STACK
    Go, Rust, TypeScript, AWS (ECS, SQS, EventBridge),
    MongoDB, PostgreSQL, Elasticsearch

HISTORY
    ASBL (current) > Sambuq > Inncircles
```

## Production impact

```diff
# WAL COMPACTION LOG (selected production overwrites)

  [asbl.mongodb]
- Atlas M60 burning compute on unindexed collection scans
+ Rewrote queries + compound indexes
+ Stepped down to M30: ~55% cheaper, p95 < 50ms

  [asbl.infra]
- Ad-hoc cron jobs drifting + manual financial reconciliation
+ Moved to ECS Scheduled Tasks
+ Automated EventBridge/SQS reconciliation pipelines

  [sambuq.search]
- Node.js hot path choking at 1.8s catalog search
+ Rebuilt in Go: 3x throughput
+ Elasticsearch n-grams: p95 < 80ms

  [sambuq.payments]
- Webhook race conditions, dropped state transitions
+ Idempotent Razorpay state machine + SQS DLQs

  [inncircles.ops]
- Multi-hour MTTR on production incidents
+ Standardized telemetry + runbooks: MTTR < 20 min
```

## Public work

Most of my production work lives in private repos. What you can read and run today:

- [**dotfiles**](https://github.com/0xrnp/dotfiles): the Ghostty + Neovim + Tmux setup I use every day.

## Currently

```toml
# /proc/memtable (in memory, not fsynced yet)
[unflushed]
rust          = "the compiler is winning"
cassandra     = "reading the LSM-tree write path & compaction"
surrealdb     = "poking at storage primitives"
open_question = "what happens when a node dies mid-write?"
```

## Ask me about

Query tuning and index design · Go service performance · idempotent payment and webhook flows · cutting database costs without hurting latency · incident response and runbooks

## Say hi

Open to conversations about backend, storage, and infra problems. Best reached on [LinkedIn](https://linkedin.com/in/0xrnp) or [X](https://x.com/debuggingpanda).

<p align="center">
  <sub><i>"Sacrifice is the only way!"</i></sub>
</p>
