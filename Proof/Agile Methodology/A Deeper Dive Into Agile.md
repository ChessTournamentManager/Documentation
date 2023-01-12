<h1>A Deeper Dive Into Agile</h1>

<h2> Table of Contents </h2>

- [What is Agile?](#what-is-agile)
  - [Flexible strategy](#flexible-strategy)
  - [Multidisciplinary teams](#multidisciplinary-teams)
  - [Short cycles](#short-cycles)
  - [Working visually](#working-visually)
- [What Agile methods exist?](#what-agile-methods-exist)
  - [Kanban](#kanban)
  - [Scrum](#scrum)
  - [Extreme Programming (XP)](#extreme-programming-xp)
- [Agile Method of Choice: Scrum](#agile-method-of-choice-scrum)
  - [Why Scrum?](#why-scrum)
- [Scrum roles](#scrum-roles)
  - [Stakeholder](#stakeholder)
  - [Product owner](#product-owner)
  - [Development team](#development-team)
  - [Scrum master](#scrum-master)
- [Meetings](#meetings)
  - [Stand-up meetings](#stand-up-meetings)
  - [Planning meeting](#planning-meeting)
  - [Review meeting](#review-meeting)
  - [Retrospective](#retrospective)
  - [Scrum board](#scrum-board)


# What is Agile?

Agile is a way of working within a project and is done often in professional software development teams. Some key features of Agile are flexible strategy, multidisciplinary teams, short cycles and working visually. 

## Flexible strategy

Teams working with Agile have an end goal. How exactly they get to this end goal can change as they go along. This is also why an Agile team does not have many plans that are already set on paper when the project starts.

## Multidisciplinary teams 

An Agile team is a team that acts quickly and independently. Within a team, there is a lot of experimentation and everyone has the drive to improve their software development and professional skills. Within a team or organisation, it is clearly decided which agile method will be used for the development process. 

## Short cycles

An Agile team often works in short cycles of 1 to 4 weeks. Stakeholders have a big influence on the direction of the project, because there is clear communication between the team and the stakeholders. The client and other stakeholders provide feedback on the results gained after every cycle.  

## Working visually

Within Agile, the idea is to easily see and track project progress. Tools are used to ensure that the whole team is aware of all progress. 

# What Agile methods exist? 

There are many Agile methods used by software developer teams. The best known Agile methods are: 

## Kanban

Kanban is an Agile method where there are no clear division of roles. This allows flexible working and encourages the team to work together in a more unrestricted way. With kanban, a time is decided by the team where a part of the project should be delivered. Kanban works with a board that shows the progress of the project. A project member cannot start the next task until his current task is set to done. The to-do list is then updated with the addition of a new task. With kanban, the backlog can be updated at any time during the project.

## Scrum

In scrum, tasks the roles of product owner, scrum master and development team are clearly designated. Scrum works with sprints in which the length of is determined in advance. After each sprint, a prototype is delivered and reviewed by stakeholders. Scrum also uses a board. The difference with kanban is that in scrum, the to-do list must first be empty before it is supplemented with new tasks for the entire team. With scrum, the backlog can only be adjusted after a sprint

## Extreme Programming (XP)

Extreme programming is also a well-known Agile method. XP, like scrum, works with sprints. However, XP sprints often last shorter, namely 1 to 2 weeks. Just like scrum, planning meetings are held in which the goals for the next sprint are determined. The difference with the scrum method is that scrum focuses mainly on management and productivity, while XP focuses more on coding and testing. An XP sprint is less focused on releasing a prototype each sprint but is more focused on delivering a bug-free system. The customer can also make adjustments to the product's requirements during a sprint. In scrum, this is only possible at the end of a sprint. XP also follows a strict sequence based on task priorities. 

# Agile Method of Choice: Scrum

## Why Scrum?

For our group project (and my individual project), scrum was the preferred Agile method. This is because kanban is often used to release features as quickly as possible. This is not the ideal method for us to use, because we would have to release new versions of our project too quickly. The features in new versions would differ too little for the stakeholders to care enough, causing everyone to waste time in unnecessary meetings. This method is more suited for teams who want to update software consistently, for example if they want to release new (small) features often, or if they want to focus on fixing bugs frequently. It also seems to be better for large teams, where tasks are bigger and if a product is being worked on for a long time.

XP is also not ideal for us, because it is often not the case that the entire team and all stakeholders are in one location. Pair programming therefore becomes very difficult and/or not very effective, and stakeholders cannot easily review our product during a sprint. It is also not the case with our project that requirements often change. However, we can use certain elements of XP, such as 'test-first programming' and the 'ten-minute build'. For implementing 'test-first programming', we will ensure that as much code will be tested as possible. For implementing 'ten-minute build', we will add CI pipelines to almost every repository. The great thing about pipelines is that there is no need to build the application manually, and that it takes a shorter amount of time than 10 minutes.

Scrum is best method for us, because it does not suffer from the above-mentioned issues. Also, the time period of 2 to 4 weeks suits us well, because that is how much time we think we need to get enough user-stories completed for a sprint. This makes us more prepared for a meeting with our stakeholders.

# Scrum roles

## Stakeholder

A stakeholder is anyone who is interested in the developed product who is not part of the development team. These are people who will help the product owner discover, develop, release, support and promote the product.

## Product owner

The product owner is the key stakeholder of the project. They are knowledgeable about the needs of the project's users and are the main source of feedback for the development team. Adjustments to the backlog are made by the product owner. 

## Development team

The development team is responsible for programming and testing the application. 

## Scrum master

The scrum master ensures that the project group works smoothly using the scrum method. He supervises the scrum meetings. 

# Meetings

## Stand-up meetings

A stand-up meeting is a daily meeting of up to 15 minutes, but preferably as short as possible. This meeting takes place at the beginning of the working day. Each project member tells what they have been working on and what task they are going to in this working day. 

## Planning meeting 

A planning meeting is held at the beginning of a sprint. This meeting determines what will happen in the sprint. In this meeting, user stories could be created and be put into the backlog, planning poker is performed, and developers choose which user stories should be done in the current sprints.

## Review meeting 

A review meeting is held at the end of each sprint. During this meeting, feedback is given by the stakeholders. 

## Retrospective

A retrospective meeting is held at the end of each sprint, after the review meeting. In the retrospective, members of the developer team discuss which processes went well in the finished sprint and which processes could be improved.

## Scrum board 

To make it clear for the team and product owner(s), a scrum board is created and maintained. This board consists of the following ticket columns: Backlog, To Do, Doing, Review and Done. This can be done on a board, but also in an online tool such as: Trello, Jira or GitHub Projects.