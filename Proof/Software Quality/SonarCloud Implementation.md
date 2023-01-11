- Table of Contents
- Introduction
	- What is sonarcloud
	- Why sonarcloud
	- Where did I implement it?
- Show its presence in the CI
- Show what it tells the developer in different scenarios
	- Merge requests
	- when the gateway fails
	- when it passes
- Readme labels
- Next Steps


Describe static code quality process and how you implemented it in more detail here. You only have to do this for the group project.

What is the process actually (in a nutshell)?

Whenever a group member pushes their code to GitHub, the static code analyzer (SonarCloud) will analyze the code and see what code smells, vulnerabilities exist, etc. Every group member will be aware of what needs to be fixed. When someone wants to merge a branch with the develop branch, they will need to pass the Sonar quality gate.

How did I do it?

- I made a Sonarcloud account and gave it access to the Modus Assumption organization. It then got access to all of the repositories, and I could put a sonartoken as a secret for all of the repositories.
- I implemented Sonarcloud into the CI (show how). This CI runs at every push and at every merge to develop and main branch
- I made sure that it could see the code coverage, which it could then use as a requirement for the Sonar quality gate.
    - I did this by making sure every repository generated a test report. This can be picked up by Sonarcloud and be analyzed.
- Later, we found out that the sonar gate was too strict, so after discussion with group members, I made it more lenient. There was no code coverage requirement for the frontends, and for the backends, it was only 60% i believe? for overall code, and not new code.

How did the code quality process go in the group?

After a sonarcloud quality check failed, it is not possible to merge that branch with the develop branch. There always need to be 2 other group members to see whether a branch can be merged with develop, so they will automatically see what SonarCloud says. They will then give feedback to the one who wants to merge the branch and help them fix the issues. If an issue takes too long too fix for a current moment, or for a different important reason, an issue will be made in Jira  about this.
If a sonarcloud gate fails because of this issue, the branch will be force merged. Because of working with this software, our project and code as become much cleaner. Issues that could accidentally slip through main branches, such as commented out code, lack of testing, or security issues, are prevented.