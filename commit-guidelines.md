# Commit Guidelines

We like commits to be clear, concise and easy to review. To achieve this, keep your commits as small and specific as possible.

For a discussion on the importance of good commit messages, please see [this article](https://chris.beams.io/posts/git-commit/ "How to Write a Git Commit Message").

When writing commit messages follow these rules:

- Use the present tense ("Add feature" not "Added feature")
- Use the imperative mood ("Move file to..." not "Moves file to...")
- Do not add full stops to the end of the first line of the commit message
- Limit the first line to 72 characters or less, 50 or less is ideal
    - More information or explanation may be added after an empty line, however the first line should always adequately summarize the change made
- Do not reference issues/pull requests in commit messages
    - The only exception is the automatic reference inserted by GitHub when squashing/merging a pull-request

If you are having trouble writing a succinct commit message, or if it includes the word 'and', consider splitting the commit into smaller ones.

## Emoji Styleguide

Consider selecting an emoji for each of your commits (based on [Atom's emoji styleguide](https://github.com/atom/atom/blob/master/CONTRIBUTING.md#git-commit-messages)).

Examples:

- :bug: `:bug:` - Bug fixes
- :memo: `:memo:` - Adding docs
- :fire: `:fire:` - Removing code
- :package: `:package:` - Adding new packages
- :green_heart: `:green_heart:` - Fixes CI Build
- :art: `:art:` - Adding UI components
- :white_check_mark: `:white_check_mark:` Adding or modifying tests
- :sparkles: `:sparkles:` - Adding a new feature
- :construction: `:construction:` - Refactor
- :lipstick: `:lipstick:` - Cosmetic changes to code style
- :triangular_ruler: `:triangular_ruler:` - Pixel perfect changes to UI

Note that GitHub might use the pull request title as commit message for the squashed commit. In that case, edit the message to include an appropriate emoji before squashing.
