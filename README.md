<div align="center">
  <img src="./banner.svg" alt="0xrnp terminal man page" width="100%" />
</div>

<br/>

```diff
# PRODUCTION CHANGELOG (selected incident & cost reductions)

  [asbl.atlas]
- MongoDB Atlas M60 cluster burning compute on unindexed collection scans
+ Rewrote hot queries + compound indexes -> stepped down to M30 (~55% cost cut, p95 under 50ms)

  [asbl.infra]
- Ad-hoc cron jobs drifting on stateful EC2 instances + manual finance reconciliation
+ Migrated to deterministic AWS ECS Scheduled Tasks + automated EventBridge pipelines

  [sambuq.search]
- Legacy Node.js hot path choking at 1.8s latency on catalog queries
+ Rebuilt core service in Go (3x throughput) + Elasticsearch n-gram indexing (under 80ms p95)

  [sambuq.pay]
- Webhook race conditions and dropped payment state transitions
+ Idempotent Razorpay webhook state machine backed by AWS SQS Dead-Letter Queues

  [inncircles.ops]
- Multi-hour Mean Time To Recovery (MTTR) during production incidents
+ Standardized telemetry and runbooks -> dropped MTTR to under 20 minutes
```

<table width="100%">
  <tr>
    <td width="50%" valign="top">
      <b><code>/etc/environment</code> (Daily Drivers)</b>
      <ul>
        <li><b>Languages:</b> Go, Rust, TypeScript</li>
        <li><b>Data & Queue:</b> MongoDB, PostgreSQL, Elasticsearch, SQS</li>
        <li><b>Infra:</b> AWS (ECS Fargate, EventBridge, Lambda), Docker, Terraform</li>
        <li><b>Environment:</b> Ghostty · Neovim · Tmux · Zsh (<a href="https://github.com/0xrnp/dotfiles"><code>0xrnp/dotfiles</code></a>)</li>
      </ul>
    </td>
    <td width="50%" valign="top">
      <b><code>/proc/memtable</code> (Unflushed / Exploring)</b>
      <ul>
        <li>Fighting the Rust borrow checker & async runtime internals</li>
        <li>Dissecting the Cassandra LSM-tree write path & compaction</li>
        <li>Experimenting with SurrealDB storage primitives</li>
        <li><i>Open question:</i> What actually happens when a node dies mid-write?</li>
      </ul>
    </td>
  </tr>
</table>

<div align="center">
  <sub>
    <b>Rudra Narayan Panda</b> · Hyderabad, IN (from Odisha) · <i>"Sacrifice is the only way!"</i><br/>
    <a href="https://linkedin.com/in/0xrnp">LinkedIn</a> · 
    <a href="https://x.com/debuggingpanda">X (@debuggingpanda)</a> · 
    <a href="https://leetcode.com/u/0xrnp/">LeetCode</a>
  </sub>
</div>
