# Dapr Proposals

## Introduction

This repository stores proposals and designs for new features in Dapr (i.e not bug fixes or minor changes) with the intention of improving visibility, historical record-keeping and maintaining a consistent process. 

### What types of changes warrant a proposal here?

As mentioned above, any significant change that needs design and a conversation around that design should go here. As a guideline, anything that would warrant a change in the Dapr SDKs would probably require a proposal. Some specific examples would include:

* New Dapr building blocks
* New APIs or breaking API changes (especially to a non-alpha component) 

## How do I create a proposal?

1. Create a fork of this repository. 
2. Copy the proposal template [templates/proposal.md](templates/proposal.md) following the format outlined below. 
3. Edit the template, filling it in with the proposal (for guides, see information in `guides/`)
5. Submit a PR to `dapr/proposals` for community review. 
 
## Proposal name format

Proposal file are named in the following format: 

> `NNNN-FLAGS-description.md`

Where *NNNN* is the next incremental number in the proposal repository, as a 4 digit number (i.e 0001, 0002...), and *FLAGS* is one (or possibly more)  of:

* B - Building block change / creation
* P - The proposal Process itself
* R - Runtime
* S - Affects SDKs 

So, for example, a proposal to create a new building block, such as the workflow building block, might be something like `0004-BRS-workflow-building-block.md`, whereas a change to the actor system, which does not require any changes to the SDKs themselves, would be something like `0005-R-actor-reminder-system.md`

## Proposal Process

1. Proposals are submitted as PRs.
2. The community evaluates the proposals and, when approved, merges them into this repository.
3. Once merged, the new feature is accepted and can be scheduled for targeting a specific release. 


