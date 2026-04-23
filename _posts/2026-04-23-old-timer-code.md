---
layout: post
title:  "Old Timer Code"
date:   2026-04-23 16:20:00 +0200
categories: [AI, Security, Legacy, DevSecOps]
---

## Introduction

Modern AI guardrails are designed to protect systems from prompt injection, unsafe content, and adversarial behaviour. These controls work well for natural language inputs, but they encounter significant challenges when applied to structured legacy code such as PL/I. In particular, constructs commonly found in PL/I—such as SQL statements, CICS transactions, and messaging operations—are frequently misinterpreted as malicious or execution-oriented behaviour.

This creates a fundamental problem for organisations attempting to use large language models (LLMs) to convert legacy PL/I code into modern languages such as Java. The guardrails, rather than protecting the system, become a bottleneck that blocks valid workloads and disrupts processing pipelines.

---

## The Core Problem

PL/I is not just a programming language; it is an operational language tightly integrated with enterprise systems. Typical PL/I code includes:

- Transaction processing (`EXEC CICS`)
- Database interaction (`SELECT`, `UPDATE`)
- Messaging (`MQPUT`, `MQGET`)
- Security controls (`RACF`)

These constructs resemble patterns that AI guardrails are trained to detect as potentially harmful. As a result, guardrails may incorrectly classify valid PL/I code as:

- Command execution
- Data exfiltration
- Privilege escalation
- External system interaction

This leads to high rates of false positives, where legitimate code is blocked before it can be processed.

---

## Observations from Testing

During testing, several patterns emerged:

1. **High-sensitivity filtering** resulted in widespread blocking of valid PL/I constructs.
2. **Reduced filtering** improved throughput but significantly weakened security controls.
3. **Disabling adversarial detection** allowed all inputs through but removed meaningful protection.

These results highlight a key issue: traditional guardrails are not well suited to structured, system-oriented code.

---

## Architectural Options

There are several possible approaches to address this challenge:

### 1. Maintain Current Filtering

Continue using guardrails with reduced sensitivity.

- Pros: Simple to implement, minimal changes
- Cons: Weak security coverage, no reliable adversarial detection

### 2. Inspect-Only Mode

Use guardrails for monitoring rather than enforcement.

- Pros: Full visibility into potential issues
- Cons: Relies entirely on downstream validation

### 3. Classifier-Based Routing

Introduce a classifier to distinguish between code and natural language inputs.

- Pros: More precise application of guardrails
- Cons: Requires significant development effort and ongoing tuning

### 4. Sandboxed Conversion

Process PL/I code in an isolated environment and validate the output.

- Pros: Eliminates false positives, maintains strong security boundaries
- Cons: Requires careful design of sandbox and validation layers

---

## Recommended Approach

A sandboxed conversion model provides the most robust solution. In this approach:

1. PL/I code is processed within an isolated execution environment.
2. The model performs the conversion to Java without external interaction.
3. The generated output is validated using both policy-based and deterministic checks.
4. A decision engine determines whether the output is accepted, rejected, or flagged for review.

This shifts the focus from input filtering to controlled execution and output validation.

---

## Security Model

The security model evolves from prevention to containment:

- **Before:** Block inputs that appear risky
- **After:** Allow inputs in a controlled environment and validate outputs

Key controls include:

- No external network access
- No system-level execution
- Stateless processing
- Post-conversion validation

---

## Conclusion

Applying AI guardrails directly to legacy PL/I code exposes a mismatch between modern security models and historical programming paradigms. Rather than attempting to force guardrails to interpret structured code correctly, a more effective approach is to redesign the architecture around isolation and validation.

By treating PL/I as inert data within a sandboxed environment and enforcing security at the output stage, organisations can achieve both high throughput and strong security. This approach avoids the pitfalls of false positives while maintaining a clear and enforceable security boundary.

---

*This is a working draft and will be expanded with implementation details, benchmarks, and reference architectures in future updates.*