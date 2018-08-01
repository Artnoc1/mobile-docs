# Pull Request Etiquette

**Our goal as the mobile developers at Toggl is to create apps of the highest quality in terms of both the user experience and the code base.**

All code changes to our apps are added using GitHub's pull requests. To be able to merge a pull request, it has pass unit tests and be approved by at least one other developer. Therefore it is of supreme importance that each pull request is as easy to review as possible. To facilitate this, follow these guidelines:

1. Pull requests should always result in a functional app and never knowingly introduce bugs or other bad behaviour
2. Pull requests should be as small and straight forward as possible
    - Each pull request should make a single clearly defined change or addition
    - Change as many files as necessary, but as few as possible
    - Do not add unrelated changes - even minor code cleanup - to your pull request
        - Create a separate pull request instead
        - If possible, split larger pull requests into multiple ones
3. Pull requests should be presented well
    - Use a clear and succinct title
        - If this is not possible, the pull request is most likely too big
    - Add a description if the changes are not trivial
        - Rather add too much detail, than too little
    - Add references to related issues/pull requests to the description
        - If the pull request closes an issue, [include `Closes #issue`](https://github.com/blog/1506-closing-issues-via-pull-requests)

To help us write good pull request descriptions, we use [pull request templates](https://help.github.com/articles/creating-a-pull-request-template-for-your-repository/) which automatically populate the description when opening a pull request on GitHub. This provides a common structure which we can fill in with specific details to allow both reviewers and those checking the pull request in the future to quickly understand the changes and their context.

It is the contributor's responsibility to make sure the merging branch is up to date with the base branch. If you would like feedback on a work-in-progress feature, feel free to create a pull request and mark it with the `wip` label. Make sure to comment on what kind of feedback you are looking for.

## Code review

Code review is one of the primary ways we ensure the quality of the apps. **Code can only be merged into the main branches of the repository if it has been read, understood, analysed, and accepted as correct by at least one other developer.** For larger features feedback from multiple developers might be needed to ensure correctness.

### Who reviews

In principle anyone can review any pull request, if they feel confident to do so. Optionally, the author of the pull request, the tech lead, or existing reviewers may request for reviews from specific people, based on their familiarity or experience with the affected systems.

If more than one review is requested, the pull request may only be merged if all reviewers have accepted it.

### How to review

Developers should be thorough and critical with both their own code, but especially when reviewing. Requested changes should only be implemented if the contributor agrees with them. Otherwise the change should be discussed until there is consensus.

A pull request should only be accepted after a full review and if the reviewer is confident of the code's correctness and conformity to our guidelines.

### Making changes to pull requests

After a pull request has been approved it should not be changed except for bringing it up to date with the base branch, assuming the merge does not call into question the correctness of the pull request. Any other changes have to be explicitly agreed upon by reviewers though it is highly preferable to only accept the pull request once it is complete and up to date.

The pull request author should address all comments by reviewers even if they accept a change request without argument so that everyone can see that there is consensus.

When the pull request author thinks they have addressed all comments and change requests sufficiently, they should dismiss the existing reviews stating this reason. This will mark the pull request as 'needing review', making it clear it is once again ready to be reviewed.

This process should never be used to dismiss critical reviews to merge a pull request that was not approved by one of the reviewers. Further, every dismissed reviewer has to approve the pull request again, before it may be merged.

## Merging pull requests

Once a pull request is up to date with the base branch and approved, it should only be merged by the original contributor, unless they explicitly state that a reviewer is allowed to merge.

When merging, consider which type of merge supported by GitHub is the best choice. Most pull requests should be small enough to be squashed into a single commit that still follows the [commit guidelines](https://github.com/toggl/mobile-docs/blob/develop/commit-guidelines.md "Commit Guidelines"). If this can not be done, prefer merging over rebasing to keep history intact.

### Transferring ownership

Should the creator of a pull request be unable to finish it, they can transfer ownership of it to someone else by assigning them to the pull request. In that case, the new owner takes on the responsibility of finishing and merging the pull request and an approval from a third developer is needed.
