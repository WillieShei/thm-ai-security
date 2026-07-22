# Room 21 — Lockdown (Challenge)

> Section 5 (Data Poisoning), Room 5 — the final room of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity). Fix three vulnerabilities in a RAG assistant; each correct remediation yields a flag fragment.

![Difficulty](https://img.shields.io/badge/difficulty-Medium-yellow)
![Type](https://img.shields.io/badge/type-Challenge%20(Defensive)-2ea44f)

## Overview

The defensive capstone. Fix three vulnerabilities in Meridian's assistant "Bastion" — data retrieval, logging, and user-level access — using `SHOW LOGS`, `QUERY AS: [name]`, and `STATUS`. Each correct remediation returns a flag fragment.

## The three vulnerabilities & remediations

| # | Vulnerability | Correct remediation |
|---|---------------|---------------------|
| 1 | **Data retrieval** — confidential docs served | Document-level access control at retrieval time; metadata-based filtering **before** ranking |
| 2 | **Logging** — plaintext sensitive content | Log redaction / data minimisation; log only non-sensitive metadata (IDs, timestamps) |
| 3 | **User-level access** — `QUERY AS` impersonation | Authenticated **server-side** identity + per-user access; derive identity from a verified session/token; scope every query to the user's permissions |

## Method

Work each vulnerability in turn: reproduce it, apply the correct remediation, verify with `SHOW LOGS` / `QUERY AS` / `STATUS`, and collect the flag fragment. The three remediations reinforce the Section 5 thesis: **enforce security before the model sees data**.

Full method: [`writeups/lockdown.md`](./writeups/lockdown.md)

## Skills demonstrated

`pre-query access control` · `log redaction / data minimisation` · `server-side identity enforcement` · layered RAG defence.

> **Note:** the flag and fragments are redacted per THM policy — this is a defensive challenge and the writeup documents the correct remediations (which are legitimate security practices).
