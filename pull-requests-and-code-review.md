# Pull Requests and Code Review

This guide covers how to create a pull request on GitHub, what makes a good PR, and how to review other people's code.

## Creating a Pull Request

Once you've pushed your branch to GitHub, you're ready to open a pull request (PR) to merge your changes into `main`.

### How to open a PR

1. Go to your repo on GitHub
2. If you recently pushed, you'll see a banner with your branch name and a green **Compare & pull request** button -- click it
3. Alternatively, click the **Contribute** dropdown on your branch page and select **Open pull request**

### Writing a good PR description

The PR title ends up in the git log when your code is merged, so make it clear and descriptive. Think of it as a one-line summary of what your change does.

In the description body:

- **What does your PR do?** Explain the change in plain language. What was the problem and how did you solve it?
- **How can it be tested?** Give reviewers enough context to verify the change works. Include steps to reproduce, screenshots, or test commands.
- **What should reviewers pay attention to?** Call out anything tricky, risky, or where you'd especially like feedback.

Think about your colleagues and your future self. Six months from now, someone may need to understand why this change was made.

### Tips for good PRs

- **Keep PRs small and focused.** One feature or one bugfix per PR. Small PRs are much easier to review and much easier to track down if they introduce a problem later.
- **Read your own code on GitHub before requesting review.** Seeing your changes in a different context (the GitHub diff view instead of your editor) often helps you spot things you missed.
- **Make sure tests pass.** GitHub will show CI status checks on the PR. Don't request review if tests are failing -- fix them first.
- **Assign yourself** so it's clear whose PR it is.
- **Request at least one reviewer.**

### Merging

When your PR is approved and tests are passing:

- Use **squash merge** (the default for most repos). This collapses all your branch's commits into a single commit on `main`, keeping the history clean and making it easy to revert if needed.
- Regular merge preserves your entire commit history in the destination branch -- including your "oops forgot a file" commits. This is usually only needed for branch maintenance, not feature work.
- After merging, delete the branch on GitHub (it will prompt you) and clean up locally.

## Reviewing Other People's PRs

### Why code review matters

- **Catch bugs** and other issues before they reach production
- **Share knowledge** and best practices across the team
- **Share ownership** -- you learn parts of the codebase you didn't write
- **Increase everyone's skill** -- both the author and the reviewer learn

### Reviewing is a high priority task

When someone requests your review, they are often blocked until you respond. A PR sitting in review is work that can't move forward. Make time for reviews -- treat them as a high priority.

Options to stay on top of reviews:
- Check [github.com/pulls/review-requested](https://github.com/pulls/review-requested) daily
- Check your email notifications from GitHub
- Set up notifications in your team's chat when you're tagged

### What to look for

When reviewing, consider each of these areas:

| Area | What to ask yourself |
|---|---|
| **Design** | Is the code well-designed and appropriate for this system? |
| **Functionality** | Does the code behave as the author intended? Is it good for the users? |
| **Complexity** | Could it be simpler? Would another developer easily understand this code when they come across it in the future? |
| **Tests** | Does the code have correct and well-designed automated tests? |
| **Naming** | Did the developer choose clear names for variables, classes, methods, etc.? |
| **Style** | Does the code follow applicable style guides? |
| **Documentation** | Did the developer update relevant documentation? |

You don't have to find something wrong. If the code looks good, say so -- an "LGTM" (looks good to me) is a perfectly valid review.

### How to give good feedback

**Talk about the code, not the author.** Say "this function could be simplified" not "you wrote this wrong." The code has a bug, not the person.

**Use "I" statements.** "I think this might break if the list is empty" lands better than "you didn't handle the empty list case."

**Follow the Observation - Impact - Request pattern:**
- Observation: what you noticed
- Impact: why it matters
- Request: what you'd suggest

**Be mindful of tone.** Text doesn't convey tone the way a face-to-face conversation does. A comment that reads as neutral to you can feel blunt to the receiver. Consider prefixing your comments with a label to clarify your intent:

| Label | Meaning |
|---|---|
| **praise:** | Highlight something positive |
| **nitpick:** | Trivial preference-based request; non-blocking |
| **suggestion:** | Propose an improvement; be clear on *what* and *why* |
| **issue:** | A specific problem that should be fixed; pair with a suggestion when possible |
| **question:** | You have a potential concern and want to understand the reasoning |
| **thought:** | An idea that popped up; non-blocking, but could lead to future improvement |
| **chore:** | A simple task that should be done (formatting, renaming, etc.) |
| **note:** | Something for the reader to be aware of; non-blocking |

For example, instead of writing "Do this thing," write "suggestion: Do this thing." This makes it clear whether a comment is blocking or just a nice-to-have, and prevents unnecessary back-and-forth.

See [Conventional Comments](https://conventionalcomments.org/) for more on this approach.

### How to receive a review

- **Be humble.** You are not your code. Feedback on your PR is not a judgment of you as a person.
- **QTIP -- Quit Taking It Personally.** Easier said than done, but worth practicing.
- **Remember it's collaborative.** Everyone wants the code to be good. The reviewer is on your side.
- **Treat it as a chance to learn.** Even experienced developers learn from reviews. A second set of eyes almost always makes the code better.

## Further Reading

- [Conventional Comments](https://conventionalcomments.org/)
- [Code Review Guidelines for Humans](https://phauer.com/2018/code-review-guidelines/)
- [How to Make Good Code Reviews Better](https://stackoverflow.blog/2019/09/30/how-to-make-good-code-reviews-better/)
- [Google's Code Reviewer Guide](https://google.github.io/eng-practices/review/reviewer/)
- [Google's Change Author Guide](https://google.github.io/eng-practices/review/)
- [The 10 Commandments of Egoless Programming](https://blog.codinghorror.com/the-ten-commandments-of-egoless-programming/)
