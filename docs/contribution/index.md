---
layout: default
title: Contribution
nav_order: 5
has_children: true
---
# Contributing as a Developer to This Project

## Contributing

1. Familiarize yourself with the codebase by reading the source code and this wiki.
2. Create a new issue before starting your project so that we can keep track of what you are trying to add/fix. That way, we can also offer suggestions or let you know if there is already an effort in progress.
3. Fork this repository.
4. [Development Environment Setup](./Development-Environment-Setup) page has details on how to set up your environment.
5. Create a _feature_ branch in your fork based on the correct branch (usually the **main** branch). Note, this step is recommended but technically not required if contributing using a fork.
6. Edit the code in your fork.
7. Send us a pull request when you are done. We'll review your code, suggest any needed changes, and merge it in.

## Naming Convention
Use CamelCase to name Salesforce custom fields (e.g., `SurveyDate__c`).

## Branches

We use [GitHub-flow](http://scottchacon.com/2011/08/31/github-flow.html) as branch strategy.

## Pull Requests

- Develop features and bug fixes in _feature_ branches.
- _feature_ branches can live in forks (external contributors) or within this repository (committers).
  \*\* When creating _feature_ branches in this repository please prefix with `<developer-name>/`.

### Merging Pull Requests

- Pull request merging is restricted to squash & merge only.