```yaml
RNP(1)                        Systems & Backend Manual                        RNP(1)

NAME
    Rudra Narayan Panda (0xrnp) — backend engineer, latency hunter, terminal minimalist

SYNOPSIS
    rnp --role="SWE L2 @ ASBL" --prev="Inncircles, Sambuq" --loc="Hyderabad, IN"
    rnp --stack="Go, Rust, TypeScript, AWS, MongoDB, PostgreSQL, Elasticsearch"
    rnp --env="Ghostty + Neovim + Tmux (0xrnp/dotfiles)"

DESCRIPTION
    Building high-throughput Go microservices and distributed cloud infrastructure.
    Originated in Odisha ("Sacrifice is the only way!"). Started in chemistry,
    pivoted to computer applications, now obsessed with storage engines, write paths,
    and cutting cloud bills in half.
```

```diff
# WAL COMPACTION LOG (selected production overwrites & tombstones)

  [asbl.mongodb]
- Atlas M60 cluster burning compute on unindexed collection scans
+ Rewrote queries + compound indexes -> stepped down to M30 (~55% cheaper, p95 <50ms)

  [asbl.infra]
- Ad-hoc cron jobs drifting on servers + manual financial reconciliation
+ Migrated to AWS ECS Scheduled Tasks + automated EventBridge/SQS pipelines

  [sambuq.search]
- Legacy Node.js hot path choking at 1.8s catalog search latency
+ Rebuilt hot path in Go (3x throughput) + Elasticsearch n-grams (<80ms p95)

  [sambuq.payments]
- Webhook race conditions and dropped state transitions
+ Idempotent Razorpay webhook state machine backed by SQS Dead-Letter Queues

  [inncircles.ops]
- Multi-hour Mean Time To Recovery (MTTR) on production incidents
+ Standardized telemetry & runbooks -> dropped MTTR to <20 minutes
```

```toml
# /proc/memtable (written to memory, not fsynced yet)
[unflushed]
rust          = "the compiler is winning"
cassandra     = "reading the LSM-tree write path & compaction"
surrealdb     = "poking at storage primitives"
open_question = "what happens when a node dies mid-write?"
```

<div align="center">
  <a href="https://linkedin.com/in/0xrnp">LinkedIn</a> · 
  <a href="https://x.com/debuggingpanda">X (@debuggingpanda)</a> · 
  <a href="https://leetcode.com/u/0xrnp/">LeetCode</a> · 
  <a href="https://github.com/0xrnp/dotfiles">Dotfiles</a>
</div>
