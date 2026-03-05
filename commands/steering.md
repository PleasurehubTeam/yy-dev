---
description: 管理项目记忆（steering）— 初始化或同步
argument-hint: [sync]
---

Invoke the `yy:steering` skill to bootstrap or sync project steering.

If no `.yy-dev/steering/` exists or core files are missing → Bootstrap mode.
If steering exists → Sync mode (detect drift, propose updates).
