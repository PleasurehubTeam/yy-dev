---
description: Manage .yy-dev/steering/ as persistent project knowledge
argument-hint: [sync]
---

Invoke the `yy:steering` skill to bootstrap or sync project steering.

If no `.yy-dev/steering/` exists or core files are missing → Bootstrap mode.
If steering exists → Sync mode (detect drift, propose updates).
