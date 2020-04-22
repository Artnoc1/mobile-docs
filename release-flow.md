
# Toggl Mobile App Release Flow

## Overview

Releasing our apps is done in a couple of steps.

1. [Start the release](#1-start-the-release)
	1. Ensure that there are no more issues on the current release project
	2. Create a release branch, pull request and changelog
2. [Test the release](#2-test-the-release)
	1. Create a test issue
	2. Create a release tag
	3. Let Bitrise build the tagged release commit and upload to the respective store
	4. Ensure that the build is available for internal testing
	5. Communicate the build's details with mobile and support teams
	6. Coordinate testing and await results
	7. If necessary, fix issues against the release branch
		- go back to 2.1
3. [Release to users](#3-release-to-users)
	1. Copy changelog and select the correct build on the store
	2. Release with phased rollout
	3. Communicate phased rollout to mobile and support teams
	4. Merge the release branch
	5. Clean up the release project

Each of these steps, as well as differences between the two platforms are broken down further below.

Note that this is an extension of the steps detailed in our [SuperFlow branching model documentation](https://github.com/toggl/mobile-docs/blob/develop/superflow.md) specifically for App/Play Store releases.


## Release manager

Each release has one developer that is responsible for it. They are the **release manager** for this release. They are responsible for creating the branch, pull request, changelog and tags. They make sure that the progress and status of the release are communicated, the release is tested well and that all issues found during testing are addressed appropriately. They give the final go-ahead to release to users.

If necessary, a new release manager can be assigned to a release by assigning the developer to the respective release pull request.


## 1. Start the release

### 1.1 Ensure that there are no more issues on the current release project

As mentioned in the [Release Manager role documentation](https://www.notion.so/Release-manager-acaa6fab78644e9db4cd6beff03667a8#8563e5e2a5c74fcf9a5ae05d35088e47), if for any reason a release still has work on it you should communicate with the teamlead to discuss what's the best course of action. Don't start a release until the release project is empty and don't just move work to the next release: discuss with the team lead to find the optimal solution.

### 1.2. Create a release checklist issue

Create a new issue for the release using the `Release checklist`. That issue is an easy way for the release manager to know what needs to be done next without leaving the context of the main app's repository. It is also way of giving people who are not directly involved in the release an idea of how much of the release process has been done and how much of it is left to do.

### 1.3. Create a release branch, pull request and changelog

The details of how to create a release branch and pull request can be found in the [SuperFlow](https://github.com/toggl/mobile-docs/blob/develop/superflow.md#release-workflow) documentation.

For writing the changelog, follow these guidelines:

#### Look at ALL changes since the previous release

The best way to do this is asking GitHub to compare changes between your release branch or tag and the previous commit tag. As an example, see this comparison made for the Android 2.1 release: https://github.com/toggl/mobileapp/compare/android-2.0.1...android-2.1

*Make sure that you check the exact previous release tag, since there may have been multiple tags for the last version!*

**Also include this comparison link in the release pull request for reference.**

Looking at this comparison you can easily go over all changes and see which affect the platform in question and should be included in the release. If some of the changes are not clear from the commit messages you can follow the link to the pull request and get more context from there.


#### Write a changelog our users can understand

The changelog will be included in the update notes of the release, which means it is a way for us to communicate with our users. Therefore, the changelog has to be written so that our users can understand it and what the changes mean for them.

Generally, it is good to phrase changes such that we emphasize the benefit for our users. They should not be overly technical, but should still be specific enough to not sound vague. If changes happen entirely under the hood and have no visible effect for our users, they do not have to be mentioned.

Some examples would be:

🚫 Increased timeout in sync retry loop  
✅ Improved syncing stability on unreliable networks

🚫 Moved start view parsing to a background thread  
✅ Improved start view performance

🚫 Fixed crash caused by creating two running time entries in a race condition  
✅ Fixed crash on startup  
✅ Fixed crash on startup related to multiple running time entries

🚫 Updated how tags are stored in database  
🚫 Added more metrics to edit view  
(Users don't have to know about these things.)

#### Use passive voice, group items, and sort by importance

We use passive voice and no full stops when writing our changelogs. Each item should start with `Added`, `Fixed` or `Improved` if possible and are grouped by the same, and in this order, with empty lines between the groups. Each group is ordered from most to least important to our users.

We also often group the many smaller changes and fixes not worth mentioning into a last generic point to indicate that the specific points are the highlights of the release.

Generally beware spelling and grammar. Capitalise proper nouns like brands and features.

For example:

```
- Added all-new Calendar View
- Added running timer notification
- Added timezone setting

- Fixed crash when opening reports
- Fixed visual glitches on login screen
- Fixed bug with Google login

- Improved time entry start view performance significantly
- Improved syncing stability on slow networks

- Various other fixes and improvements
```


## 2. Test the release

### 2.1. Create a test issue

Create a new issue for the release using the `Manual Test Template`. Add a new section to the list with tests specific to this release. Add a reference to the release PR (so that the progress of the tests is visible from the PR).

### 2.2. Create a release tag

Our versioning scheme is again detailed in the SuperFlow documentation. There is also a section that details the exact [format of release tags](https://github.com/toggl/mobile-docs/blob/develop/superflow.md#release-tags).

Make sure to not only create the tag, but also the corresponding GitHub release, which should include the changelog.

### 2.3. Let Bitrise build the tagged release commit and upload to the respective store

After creating the correctly formatted release tag, Bitrise will automatically build the respective release.

**Android:** The various APKs (one per CPU architecture) will be automatically uploaded to the Play Store.

**iOS:** The IPA will be automatically uploaded to App Store Connect, and the symbol files to AppCenter.

After successful (and unsuccessful) builds and uploads, Bitrise will post a status message to Slack.

### 2.4. Ensure that the build is available for internal testing

**Android:** Once the build is uploaded to the Play Store, it is automatically available for download through the Play Store by everyone on the internal testing track.

**iOS:** Once the build is uploaded to App Store Connect, Apple takes 5-15 minutes to process it. During that time you can see the build status in the Activity tab. Once processed, the app is available to all App Store Connect users who signed up to our TestFlight. They will get a notification from TestFlight as well.

### 2.5. Communicate the build's details with mobile and support teams

Ping @mobileteam and @support in the #mobile-support channel and inform them about the new build available for internal testing. Include the platform, version number, and changelog.

Emphasize what features need special attention while testing, whether they are already listed in the changelog or not. Also mention any potential known issues or other things to be aware of.

### 2.6. Coordinate testing and await results

Continue communicating with developers, support and QA to make sure the release is tested sufficiently. Make sure everyone is aware of the important changes, known issues, etc.

Unless this is a small hotfix release, make sure the entire app is tested. Every feature, different use cases and different environments and devices should be checked to ensure the stability of the release.

### 2.7. If necessary, fix issues against the release branch

If issues are found during testing, make sure they are well documented using GitHub issues.

Crashes and other critical bugs as well as any other issues introduced since the last release have the highest priority and should be assigned to the release's GitHub project right away. The release should not go public until all such issues are resolved and can no longer be reproduced.

Less critical issues, especially those that already existed in previous releases do not have to be fixed at this point. This decision is up to the release manager and teamlead.

Make sure to also check AppCenter to see if there are no new crashes in the internal releases before releasing to users.

After fixing some or all issues, repeat the steps 2.1 - 2.6 until no more issues are found.


## 3. Release to users

Once the release manager is satisfied that the release has been tested sufficiently and any found issues addressed, they can go ahead and release it to users.

Note that the steps outlined below require advanced permissions in the Google Play Console and on App Store Connect respectively. If you do not have these permissions, ask for them or let someone who has do the required actions for you.

### 3.1. Copy changelog and select the correct build on the store

Note that on Android, we have a lot more control about releases. We can essentially release builds to users at any moment, while with iOS we always wait for their review.

**Android:** On the Play Store the different release tracks can be managed in the Google Play Console under Release Management > App Releases. Before releasing the final internal build to users, you can add the changelog in the release notes there. Then you can release the builds from the internal track to the beta track, and from there to the production track.

**iOS:** On App Store Connect, you need to create a new release with the correct version number. Then you can paste the changelog and select the correct build, before sending the release to review by Apple. Note that you want to make sure to select Manual or Automatic release as you intend, and also already select phased rollout so you don't forget later.

Note that we often add one or two introductory sentences before the changelog. These are written in a casual tone and give a rough overview of the release highlights, but defer to the full changelog for more details. Also beware the character limits for changelogs. Apple's is very high and usually does not matter, however Google does not allow more than 500 characters. Write your changelog accordingly.

### 3.2. Release with phased rollout

We always release our builds in a phased manner, unless the release is a critical hotfix.

**Android:** On the Play Store we can select our own roll out percentage. Usually starting with 5-10% is fine. The percentage can then be increased manually over the coming days. If the build is stable, a full release should take less than a week.

**iOS:** On App Store Connect we can only select between immediate and Apple's own phased rollout scheme.

For both platforms, while the phased release is in progress, check crash statistics regularly to ensure we did not introduce critical issues. If you find that the app is significantly less stable than expected, pause the phased release immediately and consider superseding it with a hotfix.

If you are convinced the app is stable, and at least 20%+ of users have updated to it (check this on App Center/Firebase), you can consider short cutting the rest of the release and go to full release right away.

### 3.3. Communicate phased rollout to mobile and support teams

When starting the phased rollout, notify the mobile and support team of this. Mention the platform, release version, give your expectations for the rollout schedule, and post the changelog again.

During phased rollout, keep both teams up to date at least every other day. If multiple posts are needed during a single day for whatever reason, update in a thread on the first message, and don’t ping again. Additionally make sure everyone is notified if you pause the phased release or unforeseen issues emerge.

When the phased released reaches 100%, again make an announcement including all the information above.

### 3.4. Merge the release branch

The release branch should be merged into `develop` as soon the release goes out to the first user. From that point on, any following release will have its own release branch and version number.

**Make sure to merge the release branch using a MERGE COMMIT** as explained in the SuperFlow documentation. This makes sure that the release tags are part of the history of the main branch instead of dangling to the sides. That allows for the easy changelog generation above and also creates a pretty git log with most tools.

### 3.5. Clean up the release project

Once the release is fully rolled out, and we can be sure that we most likely won't need a hotfix, there should be no more open issues in the release project (with the exception of the release checklist). If there are, triage them as follows:

- If the issue is done or will no longer be relevant after the release, close it.
- If we want to work on the issue soon (e.g. a bug fix that we didn't want a hotfix for), talk to other release managers and get the issue scheduled for the appropriate release.
- If the issue isn't important enough to be scheduled right away but is something we definitely want to do, add it to the backlog.
- Remove any other issues from the release project.

Once this is done, close the release projects together with the release checklist issue.
