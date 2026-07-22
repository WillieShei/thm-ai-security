# Room 16 — Checkpoint (Challenge)

> Section 4 (AI Supply Chain Security), Room 5 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity). A single challenge — "The Audit."

![Difficulty](https://img.shields.io/badge/difficulty-Easy-brightgreen)
![Type](https://img.shields.io/badge/type-Challenge-lightgrey)

## Overview

Four candidate code-review models were submitted to SupplySecLab. Automated screening flagged three as unsafe; your job is to assess the remaining candidate and make the production go/no-go call — the capstone decision for Section 4.

## The four candidates (telemetry summary)

| Candidate | Verdict | Why |
|-----------|---------|-----|
| A — `code_reviewer_pro.pkl` | **Reject** | `os` import, reads `/etc/passwd`, `os.system` curl beacon, returns `int`, external `CommunityReview` template, `security_review_flag` disabled |
| B — `code_reviewer_lite.safetensors` | **Approve** | SafeTensors, internal verified template, guardrail enabled, verdict "Needs Changes" |
| C — `pr_analyzer_v3.h5` | **Reject** | Dangerous Lambda layer: `exec(open('/tmp/.cache').read())` |
| D — `api.reviewsvc.io` | **Reject** | Unverified endpoint, undisclosed provenance, no compliance cert, vendor-managed uninspectable prompt, auto-approves |

## Method

Assess Candidate A against the Model Acquisition Framework, correlate telemetry (file reads, disabled guardrails, external policy template, beacon session linkage), and choose the one candidate safe for production.

Full method: [`writeups/the-audit.md`](./writeups/the-audit.md)
Concept recap: [`notes.md`](./notes.md)

## Skills demonstrated

`multi-candidate risk assessment` · `telemetry correlation` · `production go/no-go decision` · applying the 5-gate framework across formats (pickle, SafeTensors, H5, API).

> **Note:** the challenge flag is redacted per THM policy. The writeup documents the decision methodology; the safe production choice is **Candidate B** (SafeTensors, guardrail enabled, verified template).
