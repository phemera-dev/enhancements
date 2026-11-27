---
tep: 0004
title: Scope, assumptions and operator responsibilities
status: draft
authors:
  - "@The127"
approvers:
  - "@phemera-dev/maintainers"
tracking-issue: https://github.com/phemera-dev/enhancements/issues/4
created: 2026-10-13
last-updated: 2026-10-13
replaces: []
superseded-by: []
---

# TEP-0004: Scope, assumptions and operator responsibilities

## Summary

This TEP says what Phemera assumes about the environment it runs in, and what it leaves to the people who run it. Phemera's security controls, as described in [TEP-0002](../0002-architecture/README.md) and [TEP-0003](../0003-data-model/README.md), only hold while these assumptions hold.

Today Phemera makes no claim to meet any regulation or standard. Whether an installation meets the requirements of its environment, and getting it approved where that's needed, is the operator's job.

## Motivation

Phemera's TEPs describe how it controls access, but not what it expects from the environment around it. Operators need to know that to decide what they have to secure themselves. It matters most where an installation has to meet regulatory requirements. There, operators ask whether Phemera's design fits, from how recordings are retained to whether a user's device has to be trusted. Many of those questions depend on the network, the hosts and the processes of one installation, and only the operator can answer them.

If this isn't written down, every component TEP gets asked to cover the requirements of every possible environment, and an operator can't tell what Phemera promises and what it leaves to them.

### Goals

- List what Phemera assumes about the environment it runs in.
- List what the operator of an installation is responsible for.

### Non-goals

- Deciding whether Phemera gets certified, and against what. That needs its own TEP.
- Defining the requirements of any particular regulation or standard.
- Changing the designs in TEP-0002 or TEP-0003.

## Proposal

Phemera secures access that goes through it: who may reach which asset, with which credentials, for how long, and what gets recorded. How the installation around it is secured is up to the operator: the platform it runs on, the network, the identity provider, the devices users connect from, and which rules of their environment apply. Phemera doesn't try to meet the requirements of every environment. It tells operators what it assumes, so they can decide what they need to add.

### What Phemera does not do

- Today Phemera doesn't check the device a user connects from. It authenticates the user, not the device.
- Phemera doesn't protect data once it reaches the user's device. What a user sees in a session can be copied or captured on that device. A recording shows what happened in the session, but it doesn't prevent this.
- Phemera doesn't secure the targets it connects to, such as the servers, databases and clusters behind it.

### What Phemera assumes

- The hosts Phemera runs on, its Postgres database and the place where recordings are stored are trusted. Phemera encrypts its secrets and makes its audit log tamper-evident, but it can't protect itself against someone who controls these.
- The clocks of all components are in sync, because access grants, the short-lived tokens that admit a session, and certificates all expire by time.

### What the operator is responsible for

- Hardening, patching and running the hosts, Postgres and the recording storage.
- Setting up the network so it matches the trust zones in TEP-0002.
- Deciding which external services the installation depends on, such as the identity provider and, once Phemera supports them, systems that receive a copy of the audit log, like a SIEM, and external secret stores.
- Configuring the identity provider, including multi-factor authentication. Its rules don't cover logins that bypass it, such as the break-glass accounts in TEP-0003.
- Watching the audit log and the session recordings.
- Deciding which requirements apply to cryptography, key storage and the retention of recordings and audit data.
- Deciding whether the installation meets the requirements of its environment, and getting it approved where that's needed.

### Settings and defaults

Phemera adds settings for security-related behavior when operators need them, for example how long recordings are kept or which cryptographic algorithms are allowed. Requests for such settings are welcome. Every setting defaults to the safer choice, so an installation that changes nothing gets the safer behavior.

### User stories

- An operator who has to meet requirements in their environment reads this TEP next to their list of requirements. For each one, they see whether it's something Phemera assumes, something they're responsible for, or still open.
- A contributor writing a component TEP gets asked to cover a requirement that belongs to the operator. They point to this TEP instead of discussing it again.

### Risks and mitigations

- Readers could take this TEP to mean Phemera isn't meant for environments with regulatory requirements. The TEP only says what Phemera leaves to operators, and it keeps the question of certification open.

## Design details

This TEP defines no design.

## Security considerations

- Trust boundaries. This TEP moves no trust boundary. It records that the hosts Phemera runs on, Postgres and the recording storage are trusted.
- Privilege. Not affected.
- Credentials and secrets. Not affected.
- Audit. Not affected.
- Failure behavior. Not affected.
- Threat model. This TEP adds nothing to the threat model in TEP-0002.

## Compatibility and upgrade

Phemera has no released version yet, so this TEP has no compatibility impact.

## Test plan

This TEP defines no code, so it has no test plan.

## Rollout

Once this TEP is `implementable`, Phemera's documentation gets a page for operators that lists their responsibilities and links here.

## Drawbacks

The lists can go out of date when later TEPs change an assumption or add work for operators.

## Alternatives

Doing nothing would leave each component TEP to answer these questions on its own, and operators would have to piece together Phemera's scope from all of them.

## Unresolved questions

- Does Phemera get certified, and against what?
- Is checking the user's device out of scope for good, or only for now?

## Implementation history

- 2026-10-13: First draft.
