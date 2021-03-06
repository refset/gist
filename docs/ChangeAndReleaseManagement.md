Change and Release Management
=====

This document describes the Semantic Arts change and release management process for gist.

Review and Triage of Outstanding Issues
-----

- Semantic Arts ontologists meet regularly (twice monthly as of April 30, 2020) in order to review and triage GitHub issues. (Refer to [Contributing.md](Contributing.md) for guidelines on submitting an issue.)
- Issues are triaged in reverse chronological order.
- Issues are categorized in one of three ways:
  - **Will not implement**
    - Label as `closed:wontfix`, `closed:duplicate`, or `closed:can't reproduce`.
    - For duplicate issues, add the earlier issue number in a comment.
  - **Will implement**
    - Assign an implementer (could be external to SA under certain circumstances, such as when the issue submitted is external).
    - Assign or re-assign priority, impact level, and effort level. These may have been assigned by the submitter but may be revised as appropriate.
    - Tentatively assign to a release project. This may be reassigned to a later release project as needed.
    - Label as `status:triaged`.
    - Determine and document the resolution to be implemented. For small issues this can be done at the current review meeting; larger issues may require additional discussion, in which case the label `status:in review` should also be added. In such cases the assignee will prepare a summary of alternative implementations, pros and cons, rationales, etc. to be presented at the next meeting. This process will continue until reviewers agree on an implementation. Once an implementation is determined, apply the label `status:implementation specified`.
- **Needs further review**
    - This case is similar to the will implement case, in that an assignee is designated to carry the discussion forward at a subsequent meeting; the difference is that here it is not yet agreed that the issue will be addressed rather than closed. Labels are applied as above.

Workflow: Implementation, Pull Requests, and Merges
- See [Contributing.md](Contributing.md).


Versions and Version Numbering
-----

Version numbers are of the form X.x.x (major.minor.patch), defined following [Semantic Versioning 2.0.0](https://semver.org/):

- **Major:** Non-backward-compatible (i.e., reasoning produces different results).
  - Examples: adding a restriction, domain, range.

- **Minor:** New, backward-compatible functionality. May constitute a large change to the ontology, such as addition to new module.
  - Examples: adding a class or property; removing a restriction.

- **Patch:** No new functionality. 
  - Examples: Fixing a typo in an annotation.

Additional notes:
- Correction of an error, even if not backward-compatible, does not require a major release. The expectation is that users will not have implemented against an obvious error. This would be a patch.
- When a local name is altered, the original term is deprecated to make it a minor rather than major change. The deprecated term receives an `owl:equivalentClass` or `owl:equivalentProperty` assertion to the new term. Deprecated terms may be removed in a future major release. Deprecated terms reside in the `gistDeprecated.owl` file. If a user wants to use a deprecated term, he/she should import this file into his/her ontology, which in turn imports `gistCore.owl` and thus all of gist.

     
Releases
-----

- Releases occur monthly, approximately on the last working day of the month, unless it is determined during a review meeting that there are not a significant number of substantive changes to warrant a release.
- Each release has an associated GitHub project, which includes all the issues and PRs targeted for that release.
- A rotating release manager is assigned to the release. His/her responsibilities are to:
  - Track the status of associated issues, making sure that they are fixed or deferred to a subsequent release.
  - Release notes have been added to the file [ReleaseNotes.md](ReleaseNotes.md) as part of the development process. The release manager will clean up these notes as needed.
  - Submit a PR to develop and request one review. After approval, the reviewer merges the PR.
  - Create and merge a new PR from develop to master.
  - Create the release package by running the bundle function of [ontology-toolkit](https://github.com/semanticarts/ontology-toolkit).. This adds version numbers to ontology IRIs and import IRIs, and includes additional files, such as release notes and license information, in the release package. This package is sent to the lead developer.
  - Close the project.
  - Draft and publish a [new GitHub release](https://github.com/semanticarts/gist/releases/new). The includes the creation of a tag, formatted as `vX.x.x` (e.g., `v9.1.2`).
- Once the lead developer has received the release package:
  - He/she will ut the new download package on the server and repoint the website download link to this new package. 
  - The download will be tested by the release manager and/or automated tools. (Test process TBD.)
  - The release manager will send the release notification to the gist Council mailing list, and the release will also be announced at the following gist Council meeting.
