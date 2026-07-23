# Room 20 — UnIndexed (Challenge)

> Section 5 (Data Poisoning), Room 4 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity). A single challenge — audit an assistant for a retrieval-boundary failure.



## Overview

Audit Cloudwright Labs' assistant "Atlas" and probe for restricted board-level data. The assistant discloses an internal reference identifier with **no access check** — a retrieval-boundary failure straight out of Room 19.

## Method

1. Query Atlas as a normal employee to establish what public data looks like.
2. Probe beyond public scope toward restricted (board-level) material.
3. Observe that the assistant returns an internal reference identifier for a restricted item without any access enforcement — retrieval has no boundary.

Full method: [`writeups/unindexed.md`](./writeups/unindexed.md)

## Skills demonstrated

`RAG boundary testing` · `retrieval-scope probing` · `access-control gap identification`

> **Note:** the challenge flag is redacted per THM policy. The lesson: retrieval with no pre-query access control has no boundary — anything embedded can surface.
