# TemplateUpdateRepos
Tooling to update repos which are based on a template

## Problem this solves

If you use a template repo to create new repos, you will have to update the new repos manually when the template repo changes. This tooling automates this process.

This is a problem for the following reasons:

* It is easy to forget to update a repo
* It is easy to make a mistake when updating a repo
* It is time consuming to update a repo
* The repo update process doesn't use a standard git workflow, because the template repo does not share a history with the new repo.
* In addition, the template files have likely been modified within the new repo, so only certain changes should be applied. Examples include version number updates of dependencies should be included, but target repo specific changes should be preserved.

The tooling will compare the template files with the corresponding files in the repository. Some of the template files will have been customized, so a diff will need to be reviewed to pick needed changes. 

Ideally the diff to be reviewed can be done through an LLM agent. This will allow the approver to see the diff in the context of the repo, and to approve the changes. The tooling will then commit the approved changes to the new branch, and create a pull request to merge the new branch into the master branch.

When the pull request is ready it can be merged. The tooling will then delete the new branch.

This process is undoable, by reverting the branch merge.

## How it works

This tool leverages the gh cli. It is assumed that the user has already authenticated to the gh cli.

A list of all the repositories for an account is created with the following command:

```
gh repo list --json <nameWithOwner> --limit 1000
```
For each repository in the list, the following steps are performed:

1. A new branch is created in the repository

2. The template repo is cloned into a temporary directory

3. The template repo is updated to the latest version

4. The template repo is copied into the new branch

5. The new branch is committed

6. A pull request is created to merge the new branch into the master branch

7. The pull request is reviewed by an LLM agent and may be marked for human reviee.

8. If the pull request is accepted, the new branch is merged into the master branch.

9. The new branch is deleted.

## Testing

All testing will be performed on private repositories which are created for testing and then deleted. The tooling will be run on a test repository, and the results will be reviewed. If the results are acceptable, the tooling will be run on the production repositories.

## Undoing the changes

If a generated pull request is not accepted, the changes can be undone by reverting the merge of the new branch into the master branch.

## How to use the tooling

The tooling will compare the template files with the corresponding files in the repository. Some of the template files will have been customized, so a diff will need to be reviewed to pick needed changes. 

Ideally the diff to be reviewed can be done through an LLM agent. This will allow the approver to see the diff in the context of the repo, and to approve the changes. The tooling will then commit the approved changes to the new branch, and create a pull request to merge the new branch into the master branch.

When the pull request is ready it can be merged. The tooling will then delete the new branch.

This process is undoable, by reverting the branch merge. 


