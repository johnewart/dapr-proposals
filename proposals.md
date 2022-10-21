# Guidlines for creating new Proposals
## What is this?

This proposal is to formalize the structure and lifecycle to proposals with three primary goals: first, make it easier for contributors to both put forth proposals as well as review them, second, increase the clarity and focus of proposals themselves, and, third, provide guidance on what is expected for a well defined feature to be "dev complete". In order to do this, I propose that we:

1. Break up the proposal process into two discrete phases 
2. Create a template for each of these two phases
3. Define the lifecycle for a feature

## Background

### Why define a better proposal process and templatize it?
 
As a community project, Dapr relies on contributors to help advance the project the goal of this proposal is to simplify the process of contributing, and evaluating, new ideas. We want to make it more inviting for community members to propose new ideas (or evaluate them) as well as ensure that the time being spent evaluating proposals or working on new features is well spent.

Adding clarity to the proposal process, as well as some amount of structure, will hopefully make it easier for contributors of all experience levels to both contribute and review new ideas. Splitting the proposal process into two phases, making each step more focused and smaller in scope, would benefit the community by making the process more approachable for new contributors who have ideas to share and also improve the process for those who are reviewing them because it would ensure that a proposal meets a certain set of criteria.

As a new contributor it can sometimes feel a bit daunting to propose a new idea -- not knowing quite where to start, whether or not what you are proposing has the right level of information, etc. Having structure makes it easier for a new contributor who wants to propose a new idea to know what is expected and feel confident that their proposal meets those expectations. In addition, for anyone putting forward a proposal, the structure proposed prompts thinking about how someone else would use the feature, how they might benefit from it, and what other ways the feature they are proposing might be solved using existing features (or other technology).  

On the other side of the equation are the community members who are reviewing those proposals; it can be challenging to review something if you feel that information or context is lacking. A consistent structure means that reviewers can know what to expect out of a proposal document and clearly ask for more information if some is missing. And, the suggested structure would make sure that reviewers have the right information needed to have a conversation about the proposal (as well as reduce the scope of the review). 

As a community, we want to be welcoming of new people and also respectful of the time and energy that everyone devotes to make this project great. I believe that adding this small amount of structure to the proposal process will help not only make it easier to propose new ideas, but also ensure that everyone who is participating can make the best use of the time they have available to improve Dapr!

### Why define the lifecycle for a feature?

As the complexity of Dapr grows, we start adding new building blocks, new APIs or enhancing existing building blocks or API. We also tend to add features that are internal to Dapr and does not directly affect the end user but may provide performance, stability improvements etc.

We need a clear guidance on what needs to be accomplished as part of a new feature contribution, so that it can be qualified as “dev complete” for a particular release milestone. “dev complete” refers to
- Completion of the code
  - Get maintainer signoff on the implementation by the feature freeze date
  - Get the code merged into the main branch of the repo well before the code freeze date (feature freeze date at most) and fix any regressions/bugs that might come up.
- Adding/Updating performance tests, e2e tests etc.
- Creating documentation for any the new feature
- Creating/Updating quick starts, tutorials

## Terminology

| Term	| Meaning                                                                                                                                                     |
|------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Building block	| Capabilities that solve common developmental challenges in building distributed applications                                                                | 
| API	| Application Programming Interface exposed by the building block for developers to use the building block capabilities in the application they are building  | 
| Feature |	New or enhanced functionality |



The keywords “MUST”, “MUST NOT”, "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", 
and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.


## Proposed phases in a proposal: Design vs Build

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

## Feature lifecycle

TBD

### Proposed New API lifecycle

An API is one form of feature that may be proposed by the contributor. Any new APIs can be split into two categories:
- new API for an existing building block e.g.: adding query state API to state management building block 
- new API in a new building block e.g.: configuration building block and adding APIs for that

The scope of this definition is limited to the `dapr/dapr` and `dapr/components-contrib` repos. 
`dapr/docs`, `dapr/quickstarts` repositories may be touched upon referring to the documentation/quickstart updates needed related to the new API definition.
SDK documentation may provide guidance on requirements to enhance the SDK. The SDKs will be touched upon only to mention the requirement of having implementation for the new APIs.
Similarly addition of `dapr/cli` commands may be mentioned, but the guidance for that is out of scope for this proposal.

Additionally the scope is limited to definition of a new API only. Enhancement to existing stable APIs shall be done seperately.

#### Proposed New API lifecycle stages

For new APIs, it is proposed to set three stages for the lifecycle of the API:
- Alpha
  - API is not production ready yet and might contain bugs
  - Recommended for only non-business-critical uses because of potential for incompatible changes in subsequent releases
- Beta
  - API is not production ready yet
  - Multiple components implement the API and API contract is mostly finalized
  - Recommended for only non-business-critical uses because of potential for incompatible changes in subsequent releases
- Stable
  - API is ready for production usage
  - Performance numbers are published for the API

#### Guidance for Alpha stage

**Prerequisite**

For any new `dapr` APIs, it is required to:
- Create a new Build Phase Proposal (assumes that the design phase is completed) in `dapr/dapr` repository, detailing
  - Relevant high level design
  - Contract for the API
    - HTTP and gRPC APIs should be consistent in behavior and user experience.
  - Additions to existing components / creation of new components for this API
  - Clarified Scope for current and following releases
  - Limitations
  - Code examples
- The issue should be reviewed by community and owner of the issue is accountable to
  - Address questions/comments in the proposal
  - Incorporate Review feedback
  - Align with maintainers on the build phase proposal scope for implementation
- Once a proposal has been accepted, the final design, links to relevant issues or comments that provide context on design decisions, and any future changes to the API  must be added to a markdown file under “docs/decision_records/api”
  - The decision record must be maintained to accurately reflect the latest state of the API.

**Creating new API as part of a new building block in `dapr/dapr`**

- Both HTTP and gRPC protocols need to be supported for the new API
- Any changes to existing API(assumes it is alpha see open question 1) in an “alpha building block” as part of implementing the new API
  - Mandates additional / modifications to existing UTs
  - Existing E2E tests if any must execute successfully
- Documentation:
  - For HTTP API – Dapr API reference doc must be updated
  - Building block concepts page must be updated
- At least one SDK shall have implementation that exposes the new APIs from runtime (giving preference to gRPC protocol in handcrafted SDKs for communication from App to Dapr)
- Quickstarts:
  - Quickstarts should be defined for the new API to enable users to easily explore the new functionality provided by the API
- Dapr CLI changes
  - If a new command/modifications to existing command is required to facilitate ease of use of the new API, it should be defined in the Dapr CLI

**Creating new API as part of an existing building block in `dapr/dapr`**

- Both HTTP and gRPC protocols must be supported.
- Behavior of existing APIs must not be modified as part of implementing the new API unless the other API is also in alpha stage. Any such changes to existing alpha APIs:
  - Mandates additional / modifications to existing UTs
  - Existing E2E tests if any must execute successfully
- If the new API is considered an optimization to an existing API (say addition of BulkGetSecrets vs GetSecret)
  - The performance improvement gained due to this API should be documented
  - Guidance must be provided to the users in docs as to when to use this API vs using the older one
- Documentation :
  - For HTTP API – Dapr API reference doc must be updated
  - Breaking changes to existing alpha APIs must be tracked and updated in docs/release notes
- Quickstarts for this new API must be added
  - This will help users comprehend the usage of the API
  - Understand the difference between this API and existing APIs. (if its an optimization)
- Dapr CLI changes
  - If a new command/modifications to existing command is required to facilitate ease of use of the new API, it should be defined in the Dapr CLI
- At least one SDK must support this API. Multiple SDKs may support this API
- E2E tests for the new API in `dapr/dapr` must be added:
  - If this new API interacts with an existing API, E2E testing that interaction must be added


Finally on addition of a new API, there may be addition of the capability to either an existing component or if it is a new building block, creation of a new set of components in the `dapr/components-contrib` repo.


**Creating new API as part of a new building block in `dapr/components-contrib`**

- Interfaces to be used by `dapr/dapr` code must be defined and agreed upon
- New building block package is defined in `components-contrib` repo, new code must only be added inside that building block package
- Conformance tests enable validating the components compliance with defined interface for the building block and creates a baseline for conformance testing any new components added. Conformance tests may be added for the new API with the understanding that it may evolve


**Creating new API for an existing building block in `dapr/components-contrib`**

- Interfaces changes for the new API must be defined and agreed upon
- Existing components that support the new API must be enhanced to be in compliance with the proposed interface as per the defined and agreed upon scope of the original proposal
- Conformance tests must be updated
  - Get sign off on a basic suite of conformance tests for the interface method(s)
  - Implement the suite of conformance tests as part of the existing suite of tests for the building block
- Ensure successful execution of existing conformance and certification tests for any modified components


#### Requirements for graduating an API from Alpha to Beta stage

In addition to the requirements for an Alpha API, the following requirements must be met so that the API can graduate to Beta.

**In `dapr/dapr`**
- E2E test with extensive positive and negative scenarios must be defined
- Most if not all changes needed in the user facing structures must be completed
  - Approvals for changes to the user facing request and response in a Beta API, will be handled on a case by case basis (Reduce number of breaaking changes)
- Multiple SDKs must have support for this API
- Documentation of the API must be up-to-date for the API/Building block
- Quickstarts must be defined for the API allowing users to quickly explore the API
- Performance tests may be added(if not already available in Alpha stage)/updated
- This API must have been a part of atleast one prior release in Dapr

**In `dapr/components-contrib`**
- Conformance test must be added/updated. (this is for scenario for new building block not having conformance test in the Alpha stage)
- Conformance tests should test both positive and negative cases 
- Certification tests should be added to the different components and this API must be exercised in the certification tests
- Multiple component implementations must be present for this API

#### Requirements for graduating an API from Beta to Stable

In addition to the requirements for a Beta API, the following requirements must be met so that the API can graduate to Stable.

**In `dapr/dapr`**
- This API must have reached Beta stage in atleast one prior release in Dapr
- E2E scenarios must be well defined and must be executed across at least two different components that implement this API
- Performance tests must be added/updated (this is for scenario where new building block does not have performance tests in the Alpha/Beta stage)
- The Performance numbers must be added to the documentation.

**In `dapr/components-contrib`**
- Conformance tests testing both positive and negative cases must be defined
- Certification tests for multiple components exercising this API must be defined
