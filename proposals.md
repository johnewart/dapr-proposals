# Guidlines for creating new Proposals

## What is this?

This proposal is to formalize the structure and lifecycle to proposals with three primary goals: first, make it easier for contributors to both put forth proposals as well as review them, second, increase the clarity and focus of proposals themselves, and, third, provide guidance on what is expected for a well defined feature to be "dev complete". In order to do this, we should:

1. Define the proposal process as two discrete phases 
2. Create a template for each of these two phases
3. Define the core requirements for a feature that is being proposed to be considered complete
4. Provide a common language for proposals (terminology, keywords, etc.) 

## Background

### Why define a proposal process and templatize it?
 
As a community project, Dapr relies on contributors to help advance the project the goal of this proposal is to simplify the process of contributing, and evaluating, new ideas. We want to make it more inviting for community members to propose new ideas (or evaluate them) as well as ensure that the time being spent evaluating proposals or working on new features is well spent.

Adding clarity to the proposal process, as well as some amount of structure, will hopefully make it easier for contributors of all experience levels to both contribute and review new ideas. Splitting the proposal process into two phases, making each step more focused and smaller in scope, would benefit the community by making the process more approachable for new contributors who have ideas to share and also improve the process for those who are reviewing them because it would ensure that a proposal meets a certain set of criteria.

As a new contributor it can sometimes feel a bit daunting to propose a new idea -- not knowing quite where to start, whether or not what you are proposing has the right level of information, etc. Having structure makes it easier for a new contributor who wants to propose a new idea to know what is expected and feel confident that their proposal meets those expectations. In addition, for anyone putting forward a proposal, the structure proposed prompts thinking about how someone else would use the feature, how they might benefit from it, and what other ways the feature they are proposing might be solved using existing features (or other technology).  

On the other side of the equation are the community members who are reviewing those proposals; it can be challenging to review something if you feel that information or context is lacking. A consistent structure means that reviewers can know what to expect out of a proposal document and clearly ask for more information if some is missing. And, the suggested structure would make sure that reviewers have the right information needed to have a conversation about the proposal (as well as reduce the scope of the review). 

As a community, we want to be welcoming of new people and also respectful of the time and energy that everyone devotes to make this project great. I believe that adding this small amount of structure to the proposal process will help not only make it easier to propose new ideas, but also ensure that everyone who is participating can make the best use of the time they have available to improve Dapr!

### Why define minimum requirements for a feature to be complete?

As Dapr increases in scope and brinds on more contributions, it is important that we define what we expect before a new feature is added to Dapr. In order to assure that all aspects of the feature have been completed for release we need to provide clear guidance on what needs to be accomplished before it is accepted into Dapr. This will help us to qualify these features as complete for a particular release milestone and be confident in what is being released. For example, most features would require, at a minumum:

* Completion of the code
* Maintainer signoff on the implementation by the feature freeze date
* Code merged into the main branch well before the code freeze date (feature freeze date at the latest) 
* During the time between feature freeze and code freeze, any P0 regressions/bugs related to this feature that are identified need to be fixed.
* Adding / updating performance tests, e2e tests etc.
* Documentation for the new feature has been committed to `dapr/docs` 
* Creating / updating quick starts, tutorials (if relevant)

In addition, some features would require changes to SDKs or have additional requirements in order for it to be considered fully complete, and so those requirements should also be tracked in order to ensure completion.


## Proposed phases in a proposal: Design vs Build

_(Note: This doesn't necessarily have to be two separate steps but there are some merits to it being two parts; open to feedback / suggestions here)_

This proposal suggests that we break the proposal process down into two separate phases - the design phase, and the build phase. The design phase is where an idea is put forth regarding new functionality or changes to Dapr; the goal of this step is for the proposal to express to the community the "what" and "why" of the proposal. The second phase is intended to focus on the "how" and the "when" (and possibly even the "who") of the idea. The intent here is to make it easier to not only introduce new ideas but to evaluate them as well by providing a small amount of structure and reducing the scope of the proposal. And, for each of these phases, we will create a template to keep proposals consistent. 


### Design Phase

"Your scientists were so preoccupied with whether they could, they didn’t stop to think if they should." - Dr. Ian Malcolm (Jurassic Park)

The intent of the design phase is to focus on two things: the idea that is being proposed, and why the idea is being proposed. In this step, a proposal must provide both the background on the idea: what it is and how it works (at a high level) as well as  why it should be introduced to Dapr. The why part of this proposal is as important (or more so) than what is being proposed, as it lets the reviewers understand better what kinds of use cases that the feature shall enable, how it shall make Dapr better or improve the experience of Dapr users. In addition, it must also convey what is in scope and what is out of scope (i.e what things have been deliberately omitted) along with any alternatives that have been considered and why they were not a good fit.

### Build Phase

The second phase of the process focuses on the implementation of the proposal - the goal of this part is to show the community not only how it shall operate, but also provide information on how success shall be measured and also include a list of activities that must be completed in order for this proposal to be complete. This is where the technical implementation of the new feature will be discussed with the intention that, because the what and why of the idea have been evaluated ahead of time, the discussion can focus on the technical details of the proposal. 

## Proposed templates for Design and Build Phases

The templates for this must include the following structure:

### Design Phase Template

1. What is being proposed?
2. Why is this being proposed?
3. What is in scope for this proposal?
4. What is deliberately *not* in scope?
5. What alternatives have been considered?


### Build Phase Template

1. How will this work, technically?
  * Design documents
  * System diagrams
  * Code examples
2. How will success be measured?
  * Performance targets
  * Compabitility
3. Checklist of things that will must be done before this proposal is complete
  * Code changes
  * Tests added (e2e, unit)
  * SDK changes (if needed)
  * Documentation
4. Feature lifecycle outline (see below)
  * Expectations
  * Compatability guarantees
  * Deprecation / co-existence with existing functionality
  * Feature flags




## Feature lifecycle outline

Features in Dapr have a lifecycle (e.g [Components](https://docs.dapr.io/operations/components/certification-lifecycle/)) and, as such, should have a defined set of milestones / requirements for progression between the lifecycle phases. For example, can a user expect from a feature when it is Alpha quality? Once that is released, what is the plan to progress from Alpha to Beta, and the subsequent expectations? What is the expectation when this feature becomes Stable? It is important to identify what functionality or perfomance guarantees we are making to users of Dapr when adding something new.

For example, the lifecycle expectations of a "Foobar API" that is going to replace an existing API might look something like:

Alpha: 
 * Initial contract for the Foobar API is complete
 * Performance is expected to be >10TPS 
 * Will not support serialization via XML
 * Data stored will not be compatible with old API, existing data will be unavailable through this API (will need to use old API to access old data)
 * Only available when feature flag `foobar-api` is enabled 
 * No migration of existing data from the old API available
 
Beta:
 * Performance meets or exceeds 1,000TPS
 * Enabled by default, users can opt-out via feature flag / configuration 
 * Existing APIs marked as deprecated
 * Migration from previous data source / format can be done manually
 * XML will be supported
 * Backwards-incompatible changes may be made
 
 
Stable:
 * Enabled by default, existing APIs have been removed fully 
 * Documentation has been changed to remove previous API definitions
 * Migration from previous data source / format will be done automatically (lazily)
 * API is stable and changes will not be backwards-incompatible
 


## Proposal Language

This information can be included either in the template or in a README -- and is designed to provide a common language for proposals so that the expectations are clear. 


### Terminology 

_(This is an incomplete list and should / will be expanded over time)_

| Term	| Meaning                                                                                                                                                     |
|------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Building block	| Capabilities that solve common developmental challenges in building distributed applications                                                                | 
| API	| Application Programming Interface - functionality exposed to end-users that can be used to interact with Dapr's building blocks in the application they are building  | 
| Feature |	New or enhanced functionality that is being added to Dapr |

### Keywords

The keywords “MUST”, “MUST NOT”, "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", 
and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.
