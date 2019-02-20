# SuperFlow: Toggl Mobile's branching work flow

To ensure - as much as possible - the quality and correctness of our code, and to enable many contributors to work on our apps at the same time without getting in each other's way we use a modified version of the GitFlow work flow [by Vincent Driessen](http://nvie.com/posts/a-successful-git-branching-model/ "Original Blog post 'A successful Git branching model' by Vincent Driessen").

We call this work flow **SuperFlow**.

Below you will find Vincent's original diagram adapted and extended corresponding to SuperFlow followed by an explanation of the various concepts and steps involved.

## SuperFlow

![SuperFlow diagram](https://github.com/toggl/mobile-docs/blob/develop/images/superflow.png)

**Legend:**
- Purple bubble: start of a release or hot fix branch
- Yellow bubble: release tag
- Green arrow: merge that requires review

### Branches

**Unless explicitly stated otherwise (either here or by the branch's owner), only a branch's creator may push changes to it.** Other developers may always create pull requests to submit changes to the branch.

#### `develop`

`develop` is our main branch. It corresponds with the current work-in-progress state of the app, that we deal with most often as developers.

`develop` is a protected branch and no commits can be pushed to it directly. The only way to add features, fix bugs, and make other changes is through pull requests that pass review and automated tests. For more details, see our [pull request etiquette](https://github.com/toggl/mobile-docs/blob/develop/pull-request-etiquette.md "Pull Request Etiquette").

**`develop` should always be stable and ready for release**. Any features that are merged only partially must be disabled in code or using a pre-compiler directive so that they do not affect release builds.

#### Feature branches

Feature branches are branches created by developers based on `develop` which are used to create new features, fix bugs, and make other changes to the app.

When a feature or change is done, it is merged into develop via a reviewed and tested pull request. **This merge should always happen using a squash**, unless there is a special case that requires an exception.

#### Release branches

Release branches are one of the only two ways of creating a new public release. They are branched off of `develop` and stay alive until the corresponding version is released.

The only commits that may be pushed directly to release branches are version and build number increments. All other changes must be applied using pull requests from release bug fix branches.

After incrementing version and/or build numbers, release tags can be created on the release branch to trigger a release build for testing.

Once work on a release branch is completed and sufficiently tested, the last release build is released to users and the branch is merged back into `develop` to incorporate all changes there. **This merge always happens using a merge commit** to ensure the release tags do not point to orphaned commits.

#### Release bug fixes

Release bug fix branches are branched off of a release branch if bugs are found during testing of a pre-release build. The bug is fixed on that branch, after which it is squashed back into the release branch using a reviewed pull request. **The owner of the release branch must always agree to this** to ensure only minimally necessary changes are included in the release.

#### Hot fixes

Hot fix branches are branched off of the latest release tag in the case of a critical bug in a released build. They are the second of two ways of creating a new public release.

In most cases the bug can be fixed directly on the branch and does not require pull requests.

After incrementing version and/or build numbers, release tags can be created on the hot fix branch to trigger a release build for testing.

Once work on a hot fix branch is completed and sufficiently tested, the last release build is released to users and the branch is merged back into `develop` to incorporate all changes there. **This merge always happens using a merge commit** to ensure the release tags do not point to orphaned commits.

### Release workflow

The above explanations of SuperFlow are not only a sub-set of allowed operations, but are in fact exhaustive. This means that there are no other valid ways to create releases, than outlined above.

In summary:
- Release and hot fix branches are the only two ways of creating new public releases.
- Release branches branch from `develop` and hot fix branches branch from the latest release tag.
- Release and hot fix branches are always merged into `develop` on completion. This merge is always performed using a non-fast-forward, non-squashed merge commit.

#### Versioning

Our apps follows the following versioning scheme:

    major.minor[.maintenance]

- The `major` component is changed only upon special considerations.
- The `minor` component is incremented by one as the first commit of every release branch **(and in no other case)**. The same commit also removes the `maintenance` component.
- The `maintenance` is added and incremented by one as the first commit of every hot fix branch **(and in no other case)**.

In addition, there is also the build number which is not visible to the public and only used to distinguish different builds internally. This number is incremented automatically for most of our apps. If it is not, it should be incremented for each created release tag.

In essence, the versioning scheme can thus be thought of as:

    major.release[.hot_fix]

#### Release tags

Release tags are our way of marking commits as (potential) releases, and trigger appropriate builds.

Each release tag should point to a commit with a unique build number on a release or hot fix branch, and represents a release candidate that will be tested and if found sufficient, released to users.

The first release tags on release and hot fix branches are named `*.*` and `*.*.*` respectively. Additional release tags are appended with a `-#` count, starting at `-2`. Further, depending on the app, prefixes may apply as well.

So for example, for the [main Toggl app](https://github.com/toggl/mobileapp) release tags look like:

- `giskard-0.2` (second android beta)
- `daneel-1.5`, `daneel-1.5-2`, `daneel-1.5-3` (three candidates for iOS release 1.5)
- `daneel-1.5.1`, `daneel-1.5.1-2` (release candidates for a follow up bug fix)
- `daneel-1.5.2` (another bug fix)
- `daneel-1.6` (the next proper release)

Each release tag should be accompanied by a GitHub release which includes the changelog since the previous release tag.


## How to make a release

Refer to the [App Release Flow](https://github.com/toggl/mobile-docs/blob/develop/release-flow.md) for detailed instructions.
