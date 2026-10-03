```rust
// rnp.wal: my career as an append-only log.
// State is whatever survives replay. Overwrites are the fixes.

use std::collections::BTreeMap;

enum Op {
    Set(&'static str, &'static str),
    Del(&'static str),
}
use Op::*;

type Entry = (&'static str, Op); // (where it happened, what happened)

const DURABLE: &[Entry] = &[
    ("origin",     Set("name", "Rudra Narayan Panda")),
    ("origin",     Set("from", "Odisha")),
    ("origin",     Set("motto", "Sacrifice is the only way!")),
    ("origin",     Set("studying", "chemistry")),
    ("mca",        Set("studying", "computer applications")),
    ("sambuq",     Del("studying")),
    ("sambuq",     Set("employer", "Sambuq")),
    ("sambuq",     Set("hot_path", "Node.js")),
    ("sambuq",     Set("catalog_search", "1.8s")),
    ("sambuq",     Set("hot_path", "Go, 3x throughput")),
    ("sambuq",     Set("catalog_search", "<80ms (Elasticsearch, n-grams)")),
    ("sambuq",     Set("payments", "idempotent webhooks, SQS dead-letter queues")),
    ("inncircles", Set("employer", "Inncircles")),
    ("inncircles", Set("mttr", "hours")),
    ("inncircles", Set("mttr", "<20 min")),
    ("asbl",       Set("employer", "ASBL")),
    ("asbl",       Set("based_in", "Hyderabad")),
    ("asbl",       Set("mongodb", "Atlas M60")),
    ("asbl",       Set("mongodb", "Atlas M30, ~55% cheaper, p95 <50ms")),
    ("asbl",       Set("cron", "on the servers")),
    ("asbl",       Set("cron", "ECS scheduled tasks")),
    ("asbl",       Set("manual_reconciliation", "yes")),
    ("asbl",       Del("manual_reconciliation")),
    ("asbl",       Set("notifications", "Go, multi-tenant, 100K+ a day")),
];

// Written to memory. Not fsynced yet.
const UNFLUSHED: &[Entry] = &[
    ("now", Set("rust", "the compiler is winning")),
    ("now", Set("cassandra", "reading the write path")),
    ("now", Set("surrealdb", "poking at it")),
    ("now", Set("open_question", "what happens when a node dies mid-write?")),
];

fn replay(log: &[Entry]) -> (BTreeMap<&'static str, &'static str>, usize, usize) {
    let (mut state, mut overwritten, mut deleted) = (BTreeMap::new(), 0, 0);
    for (_, op) in log {
        match op {
            Set(k, v) => overwritten += state.insert(*k, *v).is_some() as usize,
            Del(k) => deleted += state.remove(k).is_some() as usize,
        }
    }
    (state, overwritten, deleted)
}

fn main() {
    let (state, overwritten, deleted) = replay(DURABLE);
    println!(
        "replayed {} entries: {} overwritten, {} deleted, {} live keys\n",
        DURABLE.len(), overwritten, deleted, state.len()
    );
    for (k, v) in &state {
        println!("  {k:<16}{v}");
    }

    let (pending, ..) = replay(UNFLUSHED);
    println!("\nin memory, not yet durable:");
    for (k, v) in &pending {
        println!("  {k:<16}{v}");
    }
}
```

```console
$ cargo run
replayed 24 entries: 8 overwritten, 2 deleted, 12 live keys

  based_in        Hyderabad
  catalog_search  <80ms (Elasticsearch, n-grams)
  cron            ECS scheduled tasks
  employer        ASBL
  from            Odisha
  hot_path        Go, 3x throughput
  mongodb         Atlas M30, ~55% cheaper, p95 <50ms
  motto           Sacrifice is the only way!
  mttr            <20 min
  name            Rudra Narayan Panda
  notifications   Go, multi-tenant, 100K+ a day
  payments        idempotent webhooks, SQS dead-letter queues

in memory, not yet durable:
  cassandra       reading the write path
  open_question   what happens when a node dies mid-write?
  rust            the compiler is winning
  surrealdb       poking at it
```

[LinkedIn](https://linkedin.com/in/0xrnp) · [X](https://x.com/debuggingpanda) · [LeetCode](https://leetcode.com/u/0xrnp/)
