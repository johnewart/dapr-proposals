
## Proposal: API Design Guide

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
