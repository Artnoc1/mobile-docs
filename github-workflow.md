# GitHub Workflow

This document describes the general GitHub based workflow of the Toggl Mobile team.

Our main priorities when designing our workflow are, from most to least important:

1. Quality of the apps from a user experience point of view
    - Well designed and implemented features
    - Minimal (read: no) bugs and other issues
2. Quality of the code base
    - Readability, maintainability, etc.
3. Make our work as developers smooth, uncomplicated, fun
    - Have few hoops in the way of getting things done


## Projects

As our highest level of organisation on GitHub, we use projects. Each project either corresponds to an upcoming release, or groups issues related to a theme or major feature.

There usually are several active projects per app, which includes all the issues relevant at the time. **Issues inside projects are sorted** from highest to lowest priority, and should be worked on in that order. Project usually have deadlines, which indicate the time at which we want all their issues resolved and closed.

We try to schedule our work ahead by at least a month using projects, to make sure things can always keep moving.


## Issues

We try to create issues for any work on the respective app.

Issues are as specific and clear as possible, and should contain all the information needed to start working on them immediately.

To help us write good issues, we use [issue templates](https://help.github.com/articles/about-issue-and-pull-request-templates/). You can choose the appropriate template when creating a new issue and GitHub will populate the description automatically. This provides a common structure which we can fill in with specific details to allow anybody checking or working on the issue to quickly understand the needed changes and their context.

When starting work on an issue, the respective developer should assign the issue to themselves to let others know they are working on it. In general, before starting work on a new issue, those already started on should be resolved first.

Unless an issue is invalidated otherwise, it should only be closed by merging a pull request. When opening such a pull request, the issue should be marked with the `pending-review` label.

If a developer is unable to finish an issue or otherwise stops working on it, they should unassign themself from it so that someone else can continue the work.

### Labels

We use labels sparingly to give further information to issues. Here are the common labels we currently use, and when to use them.

- `blocking` - the issue or pull request blocks other work  
- `bug` - the issue refers to a functional bug inside the app; these usually have high priority
- `cleanup` - deals with refactoring, or other changes that should not change how the app functions
- `crash` - a serious issue that crashes the application
- `critical` - the issue or pull request has the highest priority
- `glitch` - a non-functional issue in the app, usually related to misbehaving UI
- `needs-design` - the issue still needs UI/UX design
- `on-hold` - the issue cannot be resolved at the moment, or is suspected to be invalid and awaits further testing
- `pending-review` - the issue has a pull request, which is awaiting review
- `up-for-grabs` - this issue can be worked on by someone with little experience with the app's intricacies (e.g.: Test weekers)
- `wip` - work in progress; usually applied to pull requests that are not ready for review


## Further documentation

For more detailed information on how to submit changes through pull request, how to structure commits, and the branching model we use, please check the following links.

- [Pull Request Etiquette](https://github.com/toggl/mobile-docs/blob/develop/pull-request-etiquette.md "Pull Request Etiquette")
- [Commit Guidelines](https://github.com/toggl/mobile-docs/blob/develop/commit-guidelines.md "Commit Guidelines")
- [SuperFlow](https://github.com/toggl/mobile-docs/blob/develop/superflow.md "SuperFlow: Toggl Mobile's branching work flow")
