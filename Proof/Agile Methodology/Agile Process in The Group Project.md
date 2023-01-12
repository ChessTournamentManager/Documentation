<h1>Agile Process in The Group Project</h1>

<h2>Table of Contents</h2>

- [Introduction](#introduction)
- [GP Agile Process](#gp-agile-process)
  - [The Start of Every Sprint](#the-start-of-every-sprint)
  - [Picking up a Task](#picking-up-a-task)
  - [Stand-up](#stand-up)
  - [Definition of Done](#definition-of-done)
  - [At the End of Every Sprint](#at-the-end-of-every-sprint)
- [Process Benefits](#process-benefits)


# Introduction

In our group project for the third semester, we worked in an Agile way. The Agile methodology that we have chosen is Scrum. For more details about Agile and Scrum, look at [this document](https://github.com/ChessTournamentManager/Documentation/blob/main/Proof/Agile%20Methodology/A%20Deeper%20Dive%20Into%20Agile.md). At the start of our project, I have suggested and documented some guidelines which I think were useful to adhere to. After documenting this, I asked for feedback from the other group members. Together with recieved feedback, we have finalized our 'code of conduct' document.

In this document, our process is clearly explained for everyone in the group and contains certain 'rules' which are good to follow. These processes and rules will be described here.

# GP Agile Process

Our Agile process can be briefly described in this order:

Per day:

1. We perform a stand-up.
2. Developers in the team pick up a task.
3. When a developer finishes a task, they will check the 'definition of done' and after that move the task to 'review' and 'done'.

Per sprint:

1. We do tasks that must be performed at the start of every sprint.
2. We do the usual 'per day' Agile process, until the end of the sprint.
3. We do tasks that must be performed at the end of every sprint.

Each of these cases are described below.

## The Start of Every Sprint

When necessary, new user stories are created and put in the backlog. For these user stories, acceptance criteria are added. Each of these user stories will be given an amount of story points, based on the planning poker of the developer group. Other than acceptance criteria, each of these new user stories are also given sub-tasks.

Some user stories present in the backlog will then be moved to the current new sprint, and the sprint will commence. A short stand-up is performed, so that developers can assign themselves to a task.

## Picking up a Task

After a developer has assigned themselves to a tasks, they must create a branch based from develop. There is a rule for how branches based on tasks are named: The Jira ID of the task must be at the start of the branch name, and is followed by a short version of the description of the task.

Here is an example of how a branch should be named. If this is the task in Jira: MOD-19 – Create the menu page in the front-end, the branch name should be: MOD-19_create-menu-page.

If multiple developers are working on a task branch, they should always make sure they have pulled all pushed code from other developers before pushing code themselves.

## Stand-up

At the start of every day, a stand-up is performed. Please [click here](/Proof/Agile%20Methodology/A%20Deeper%20Dive%20Into%20Agile.md#stand-up-meetings) to learn more about standups.

## Definition of Done

Before developers create a merge request, they must make sure they have tested their code and have a sufficient amount of code coverage. The code must also not contain any errors or commented-out code, unless there is a very good reason for pushing it to the develop branch. The CI/CD pipeline will usually block code from being merged with the develop branch if it contains any of these cases, but it saves time for one developer to fix these issues before another developer sees it when reviewing the code.

After a developers have done these things, they should start a merge request to the develop branch and assign two people to review the merge request. They should also put the task ticket in Jira to ‘to review’.

Once the merge request is approved and if the CI/CD pipeline succeeds, the assigned developer will merge the branch into the develop branch. Then they will move the task ticket in Jira from ‘to review’ to ‘done’ and update the status of the acceptance criteria in the user story that task belonged to.

If all the acceptance criteria in a user story are done and all the tasks are finished, the user story ticket will be moved to ‘done’.

## At the End of Every Sprint

At the end of every sprint, a [sprint review](/Proof/Agile%20Methodology/A%20Deeper%20Dive%20Into%20Agile.md#review-meeting) with the product owners is done and a [sprint retrospective](/Proof/Agile%20Methodology/A%20Deeper%20Dive%20Into%20Agile.md#retrospective) is held. Each sprint retrospective has a GitHub board on GitHub projects.

# Process Benefits

this helped us because blabla