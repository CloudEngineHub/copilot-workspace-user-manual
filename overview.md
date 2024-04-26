# Copilot Workspace: Overview

Software development is __task-centric__. Each day as a developer you start with a task, and your goal is to
explore, understand, refine, and complete that task. This journey can be exciting, challenging,
fascinating, and rewarding. And along the way you use tools, tools designed to assist you.

Copilot Workspace is a task-centric AI assistant that takes this journey with you, every step of the way — the journey from task to working code.
You will usually enter Copilot Workspace by a button available on on every GitHub issue. Copilot Workspace then assists you
in exploring a solution through a workflow — a structured timeline of steps that are __AI-generated but human-editable__. This workflow is designed to
orient, assist, and empower you towards completion.

Copilot Workspace is __explorative__. It offers a canvas for you to navigate, understand and complete tasks, augmenting
your existing development workflow with a new kind of AI assistance. You can use Copilot Workspace to explore and understand
unfamiliar codebases and real-world tasks associated with them. Copilot Workspace is a friend helping you
navigate the unfamiliar and learn new skills.

Copilot Workspace is __pervasive__. It is right there, ready and waiting for you, on every issue in every enabled repository
on GitHub. On GitHub, there's an entire universe of software and tasks to explore with Copilot Workspace: any issue, any
repository. And Copilot Workspace is even there for you when generating software from scratch — you can find it on every template repository, where
you can use Copilot Workspace to create new software repositories using natural language.

Copilot Workspace is __iterative__. Unlike fully-automatic AI assistants, Copilot Workspace encourages you to check, review, refine and iterate
on generated specifications, plans and implementations. You can edit, delete, and add to the AI-generated content. You, the developer, are in control.

Copilot Workspace is __collaborative__. It is designed to be used by teams of developers, who can share
a workspace and collaborate on tasks together. You can create and share a sessions with your team, and work
together to complete tasks. You can publish links to your sessions as comments on related GitHub issues or pull requests.
And as a maintainer, we give you controls to help manage the use of AI-assisted development in your repositories.

Finally, Copilot Workspace is __configurable__: you can integrate Copilot Workspace into your existing or
new workflows by creating incoming links that specify common tasks — like adding unit tests — or use
existing documents as indicators of new tasks.

In this manual, we will guide you through the features and workflows of Copilot Workspace, and help you get started with using it effectively.

<img src="images/session.png" width="600" alt="A fully-implemented workspace session">

*A fully-implemented workspace session that illustrates the structured timeline-based workflow (issue-to-PR)*

__Components of the Copilot Workspace end-to-end workflow:__

1. [Task](#task)
1. [Topic](#topic)
1. [Specification](#specification)
1. [Plan](#plan)
1. [Implementation](#implementation)
1. [File Iteration](#file-iteration)
1. [Integrated Terminal](#integrated-terminal)
1. [Session Sharing](#session-sharing)
1. [Task Completion](#task-completion)
1. [Session Dashboard](#session-dashboard)

## Task

Everything in Copilot Workspace begins with a “task”, which is a natural language description of intent. The task always has a context: a GitHub repository.

For this technical preview, Copilot Workspace supports four types of tasks, each with its own distinct entry point from GitHub.com and the GitHub mobile app:

| Task type | Entrypoint | Task definition |
|-----------|-----------------|-----------------------------|
| Solve Issue | [Open in Workspace](images/open-in-workspace-full.png) | The title and body of the issue and the issue’s comment thread |
| Create Repository | [Template Repository](images/create-repo-from-template.png) or [Copilot Workspace](https://copilot-workspace.githubnext.com/new) | The description of the software and the README of the template repo |
| Refine PR |  [Open in Workspace](images/pr.png) | The task description and the specific code changes in the PR |
| Ad-hoc | [Repository](images/ad-hoc-task.png) | The task description | 

Copilot Workspace displays the current task as the root of the timeline, and when needed, includes a panel with any additional context.

| Task type |Timeline representation |
|-----------|:----------------------:|
| Solve Issue | <img src="images/issue-timeline-representation.png" width=600 alt="Issue task timeline representation"><br>*The task is labeled as “Issue”* |
| Create Repository | <img src="images/repo-task-timeline-representation.png" width=600 alt="Repo task timeline representation"><br>*The task is labeled as “Repository”, and the “Template” panel indicates the template repo* |
| Refine PR | <img src="images/pr-task-timeline-representation.png" width=600 alt="PR task timeline representation"><br>*A “Pull Request” panel includes the title and description of the PR, along with the task* |
| Ad-hoc | <img src="images/adhoc-task-timeline-representation.png" width=600 alt="Ad-hoc task timeline representation"><br>*The timeline starts with the ad-hoc task and has no associated metadata* |

Once a task is defined, Copilot Workspace will progress to the next step in the timeline. Since an issue inherently represents a task definition, you can open it in Copilot Workspace and get started immediately.

## Topic

In order to help summarize a non-trivial task definition (e.g. an issue with a long comment thread), Copilot Workspace generates a “topic” for the task, which takes the form of a question that can be posed against the codebase, and used to define the before/after success criteria (see the [specification](#specification) section below). 

<img src="images/topic-question.png" width=600 alt="Topic question">

*Note how the topic introduces clarity that is completely missing from the issue title*

You can think of the topic as a way to distill the task down to its essence, and to give the developer an early and fast opportunity to see if Copilot Workspace is on the right track. If the topic is wrong, you don't need to continue. But if the topic is right, we’ve found that this helps developers to better understand the task, and to focus on the most important aspects of the codebase that are relevant to the task.

## Specification

In order to help contextualize the task for developers, Copilot Workspace takes the task details and topic, and generates a bulleted list which articulates the current behavior of the codebase, based on the topic being posed. We’ve found that this helps build developers' confidence (because they can verify that Copilot Workspace understands the project/task), and also, serves as a means of onboarding folks to a task, when they might not fully understand the current state.

<img src="images/current-spec.png" width=600 alt="Current specification">

*The current specification answers the question in the topic based on the current state*

And if Copilot Workspace gets anything wrong, then the developer can easily edit/delete steps from the current spec, or even choose to regenerate an entirely new spec (“try again”). But in practice, we find that these tend to be pretty good on the first try.

Additionally, if we detect that a user’s task is overly ambiguous/unclear (e.g. it doesn’t seem aligned with the goals/focus of the repo), then we’ll warn them about that and ask them to clarify the task further, before they can carry on. This is done to prevent hallucination in the plan and help guide users towards the “pit of success”, since subsequent stages of the workflow work best when they have sufficient detail.

<img src="images/ambiguous-spec.png" width=600 alt="Ambiguous specification">

*The user is warned that their task is too ambiguous and that their intent needs to be clarified*

After the current specification, Copilot Workspace generates a “proposed specification”, which is a bulleted list which articulates the state that the codebase would be in after resolving the task (effectively answering the question in the topic). And in particular, the proposed specification is focused on defining the success criteria of the task, as opposed to getting into implementation details (which is the role of the [plan](#plan)).

<img src="images/proposed-spec.png" width=600 alt="Proposed specification">

*The proposed specification indicates how to edit the codebase in order to solve the task*

## Content Selection

To generate the current and proposed specifications, and for all following steps, Copilot Workspace needs to identify which files in the codebase are relevant to understanding and completing the task. It does this by a combination of LLM techniques and traditional code search. The contents of the highest-ranked files are then used as context for nearly all steps in the workflow.

Users may review the files selected by Copilot Workspace using the View references” button in the Specification panel. To adjust which files are selected, users can edit the task and use natural language to specify which files are relevant.

<img src="images/references.png" width=600 alt="Show references dialog">

*The references that the model used to generate the original and modified specifications*

## Plan

Once the developer is happy with the current and proposed specs, they can request Copilot Workspace to generate a plan, which is a list of the files that need to be modified (e.g. edited, created, deleted, moved, or renamed) in order to accomplish the success criteria of the proposed spec. Additionally, each changed file includes a list of specific steps that indicate the exact changes that need to be made.

Like the spec, the plan is fully editable and regeneratable, which allows the developer to refine and steer Copilot Workspace in the right direction.

<img src="images/plan.png" width=600 alt="Plan">

*A plan, showing the steps needed to edit one file and add a second one*

## Implementation

When the developer is happy with the plan, they can click the “Implement” button in order to begin implementing it. This will update the UI to display a series of queued file updates on the right side, and then begin generating the updated file contents one-by-one. When a file begins generating, its associated entry in the plan will show it as being in progress. And when it completes, the plan will indicate it as being done.

Once a file is implemented, Copilot Workspace renders a diff view for it, and automatically scrolls to the first change. The diff editors are editable, which allows making minor tweaks directly to the code, as opposed to iterating via changes to the task, spec, or plan.

## File Iteration

We don't expect Copilot Workspace to always get everything right, and so we make it easy for users to iterate on the implementations file by file. Simply add, remove, edit the items in the plan steps for each file, select the checkbox,
and click the "Update selected files" button. This will re-generate the contents of the selected files and update the diff view.

For example, they can edit the diff directly, or they can go back to the plan and make changes there. And if they need to make more extensive changes, they can regenerate the plan entirely.

<img src="images/file-iteration.png" width=600 alt="Plan panel with file iteration">

*The plan panel enables users to iterate on implementation file by file*

## Integrated Terminal

Once the developer has implemented their plan, Copilot Workspace enables them to validate the changes for correctness by bringing up an integrated terminal and executing shell commands. This allows performing a build, lint, test, etc. against the changes, and can be a quick and effective way to gain confidence about the task and its completion status. The terminal is backed by a Codespace, so it is a secure sandbox with a full development environment installed. 

<img src="images/terminal.png" width=600 alt="Integrated terminal">

*Integrated terminal, showing the generated branch name and access to just-in-time compute*

If the developer wants to make any more extensive changes or leverage rich editor features (e.g. step debugging), they can open the Copilot Workspace session in a Codespace, using any of Codespace’s supported clients.

## Session Sharing

In order to make it easy to share a workspace session with others (e.g. for doing an ad-hoc code review or sharing an initial implementation idea), Copilot Workspace allows users to generate shared links. These links can be shared with guests, even if they are not part of the Copilot Workspace preview.

Shared sessions are copies of the original session. Non-guest users can use them a as a starting point to continue the task or explore alternative solutions without interfering with the original session. Guest users can view the session but cannot use the workspace to make changes.

<img src="images/share-link.png" width=600 alt="Generating a share link">

*Generating a share link from the header bar*

When working with issues and pull requests, additional sharing options are offered

* Publish to issue comment. Copilot Workspace automatically generates a comment with a share link for the session, which is included in the issue. This allows reviewers to quickly access the workspace session and see the proposed changes.

* Publish to pull request comment. Similar to the issue comment, Copilot Workspace automatically generates a comment with a share link for the session, which is included in the pull request. This allows reviewers to quickly access the workspace session and see the proposed changes.

## Task Completion

When a task is implemented, validated, and reviewed, developers can complete the task by taking one of a few different types of “exit paths”, depending on the type of task they’re working on.

<img src="images/task-completion.png" width=600 alt="Creating a pull request">

*Creating a pull request for the implemented changes*

| Task type | Available exit paths | 
|-----------| -------------------- |
| Issue | — Create pull request <br> — Create draft pull request <br> — Push to new branch <br> — Push changes to current branch (only available if you have commit permissions to the repo) <br> <br> These may fork the repository if you do not have write access |
| Ad-hoc task | — *As for issues* |
| PR task | — Update pull request (pushes a new commit with the changes) <br> — *As for issues* |
| Repo task | — Create repository (creates a new repo from the selected template repo, and includes the changes) |

## Session Dashboard

In order to make iteration feel lossless, Copilot Workspace automatically saves your work. It also provides a session dashboard, which allows you to easily resume your work later. Additionally, because Copilot Workspace is fully optimized for usage on mobile devices, you can even start a task from your phone and then finish up on your laptop, or vice versa. 

<img src="images/dashboard-2.png" width=600 alt="Copilot Workspace dashboard">

*The Copilot Workspace dashboard showing recent, bookmarked and completed sessions*

## Undo/Redo

Undo and redo are supported via the standard keyboard shortcuts: `Ctrl-Z` and `Ctrl-Y` on Windows and Linux, and `Cmd-Z` and `Cmd-Y` on macOS.

## Appendix: Glossary

| Term | Definition |
|------|------------|
| Copilot Workspace | A Copilot-native dev environment that’s designed for exploring and completing every day tasks  |
| Target | A branch of a codebase at a specific commit | 
| Task | A natural language description of a change to a target | 
| Topic | A brief single-sentence summary of a task, usually in question form |
| Specification | A description of the current and proposed state of the target as it relates to the task |
| Plan | A list of files to add, remove or change, with notes about each of them, that together transform the target from its current state to its proposed state |
| Implementation | A set of changes to the target that, when applied, will complete the task |
| Session | A user’s saved progress towards completing a task, a single task can have many sessions |
| Snapshot session | A snapshot of a user’s session, created when you click “Share link”, including both the task progress and UX state |