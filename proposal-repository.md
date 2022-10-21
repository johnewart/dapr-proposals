
## Proposal: Centralized proposal repository 

### What does this propose?

This proposal suggests that we create and maintain a repository specifically for proposals related to Dapr (ie github.com/dapr/proposals) This follows the model that a number of other projects use in order to keep proposals and their lifecycle separate from the day-to-day issues and pull requests that the project, and its related repositories, etc. 

To be clear, this would be a location to make proposals related to Dapr as a holistic entity. This would not be a place to make proposals for, say, a change to the Java SDK to swap out HTTP libraries or something that is specific to a language implementation. That being said, the reverse may be true, a proposal made in `dapr/proposals` could very well affect SDKs if, for example, a new API is being proposed or a new building block is being added. 

### Why should we do this?

Doing this would have two primary benefits (feel free to suggest others):

1. Keeps the lifecycle of proposals separate from daily codebase operations (pull requests, issues, etc.)
2. Provides a centralized, predictable, place for proposals related to any part of the Dapr ecosystem (SDKs, components, core services, etc.) 

Keeping proposals centralized means that they are much more discoverable and easier to follow in that they provide a clear repository for historical design choices and decisions. Currently we have some traces of this in `dapr/dapr/docs` but maintaining that requires out-of-band effort whereas it would come for free in this model. This is beneficial when looking to add a new proposal or other design because it makes it easier to see previous conversations and examples all in one central place. Because the proposals themselves will be Markdown files (and related assets), any changes to the proposals over time can be viewed and things like check-boxes can be updated over time to be clear about what is, or what is not, completed. 

#### Side-effects

This has some added benefits when it comes to proposal reviews, in that it is much easier to make line-level comments and see the comment history about various parts of the doc (as well as when updates are made / comments are addressed). This helps to avoid multi-point comments that sometimes lead to missed information, and be very clear about where a comment / feedback is targeted.

And, as an added bonus, because diagrams and other bits can be stored as files in the repository they can easily be re-used elsewhere (or referenced) such as in documentation. 

### How will we implement this?

Create a new repository (`dapr/proposals`) and begin to store new proposals there as Markdown files. New proposals will come in the form of pull requests to the repository, and once they are accepted / completed the PR will be merged and the proposal / design will be available in the repository. 

To make a proposal, a user would fork the repository, add their proposal (and any related assets) into the repository in their fork and then open a pull request against the main repository. The lifecycle of proposals would then look something like:

* **Draft** Changes made in personal fork 
* **Ready For Review** Pull request opened against `dapr/proposals`
* **Accepted** Pull request has been merged into `dapr/proposals` repo 

As progress is made on an accepted proposal (i.e parts are completed) then PR's can be made to update the check-boxes on those sections and issues / PRs / code lines can be linked to those PRs pointing to where to look for the work done. 

#### Existing Example

The gRPC proposal repository is a good example of this (https://github.com/grpc/proposal)

### What needs to be done?

- [ ] Create a new repository
- [ ] Create a README.md in the new repository outlining the process for creating a new proposal with pointers to examples, templates, etc. 
- [ ] Move any in-flight proposals to PRs against this new repository
- [ ] (Optional) move previous proposals to this repository as Markdown files
- [ ] Update any documentation to point to this new repository
