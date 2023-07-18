# GitHub action: Create new project 

This GitHub Action enables you to create new GitHub projects using your current project as a template. It simplifies the process of creating new projects for your development team by providing predefined templates. When triggered, this action creates a new GitHub project by duplicating the current project's structure and files.

## Why to use it

It allows you to establish a consistent project setup across your organization or team, saving time and effort in setting up new projects from scratch.

This time-saving aspect is particularly valuable when working on Proof of Concepts (POCs) and spikes. Instead of starting each POC or spike from scratch, you can use this action to quickly spin up new projects based on your existing template. This helps you focus more on the core objectives of your POC or spike rather than spending time on project setup. By leveraging the predefined templates, you can ensure that all POCs and spikes follow a standardized structure and have the necessary configurations in place. This promotes better collaboration, improves efficiency, and allows you to iterate faster on your ideas.

## Usage

The following workflow added to your project enables you to use it as a copy template:

```
name: Create new project

on:
  workflow_dispatch:
    inputs:
      project:
        required: true
        type: string
        description: Name of the project to create

jobs:
  create-new-project:
    runs-on: ubuntu-latest

    steps:
    - id: create
      uses: hekonsek/action-create-new-project@v0.3.0
      with:
        project: deleteme-${{ github.event.inputs.project }}
        token: ${{ secrets.GH_TOKEN }}
    - run: echo ${{ steps.create.outputs.repository }}    
```

## Inputs

| parameter | description | required | default |
| --- | --- | --- | --- |
| project | Name of the new project to be created. | `true` |  |
| token | GitHub token. Should have the following permissions: `all repo`, `all workflow`, `write:org` . | `true` |  |

## Outputs

| parameter | description |
| --- | --- |
| repository | Created repository in owner/repo format. |