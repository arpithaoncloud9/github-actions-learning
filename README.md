
### **Git Basics**
#### Git :
Git is a distributed version control system that allows developers to track changes, work on code in parallel using branches, and merge updates efficiently. It keeps a complete history of the project and enables collaboration without overwriting each other’s work.

#### GitHub :
GitHub is a cloud-based  platform that hosts Git repositories. It allows developers to store code, track changes, collaborate, and manage projects using Git version control

#### Repository : 
A GitHub repository is a storage space where your project’s code, files, packages, and documentation live. It keeps track of all changes through version control, so teams can collaborate, review code, and manage updates efficiently.

#### Git Basic Commands :
```
 1. git config --global user.name "Your Name" 
 2. git config --global user.email "you@example.com"
 3. git config --list : View you Git configuration
 4. git init : Initialize a new Git repository 
 5. git clone <repo-url> : Copy a remote repository to your local machine
 6. git status : See changes, staged files, and branch info
 7. git log : View commit history
 8. git add <file> or git add . : Stage all changes
 9. git commit -m "message" : Commit staged changes
 10. git commit -am "message" : Add + commit tracked files in one step
 11. git branch : List branches
 12. git branch <branch-name> : Create a new branch
 13. git checkout <branch-name> : Switch branches
 14. git checkout -b <branch-name> : Create + switch in one step
 15. git branch -d <branch-name> : Delete a branch
 16. git merge <branch> : Merge a branch into the current one
 17. git rebase <branch> : Reapply commits on top of another branch
 18. git remote -v : View remote URLs
 19. git push : Push commits to remote
 20. git push -u origin <branch> : Push and set upstream
 21. git pull : Fetch + merge from remote
 22. git fetch : Download changes without merging
 23. git restore <file> : Undo changes in working directory
 24. git restore --staged <file> : Unstage a file
 25. git reset --hard : Reset working directory and staging area
 26. git reset --soft HEAD~1 : Undo last commit but keep changes staged
 27. git revert <commit-id> : Create a new commit that undoes a previous one
 28. git stash : Save uncommitted changes temporarily
 29. git stash pop : Reapply stashed changes
 30. git stash list : View stashes
 31. git diff : See unstaged changes
 32. git diff --staged : See staged changes
```
#### CI/CD :
Is an automated pipeline that takes code from development to production. 
1. Continuous Integration ensures every code change is automatically built and tested and merged with existing code. 
2. Continuous Delivery or Deployment automates the release process so updates can be shipped quickly, consistently, and with minimal manual effort. It improves speed, reliability, and developer productivity.

## GitHub Actions :
A tool that lets you automate your software development workflow.
It allow you to react to some **events** that can happen in the repository or outside the repository. And run the workflow in response to that event.

#### Why would you choose GitHub Actions instead of Jenkins ?
- Jenkins is powerful and highly customizable, but it requires significant setup, plugin management, and ongoing maintenance. 
- GitHub Actions, on the other hand, is fully managed and integrates directly with GitHub. 
- It automates builds, tests, and deployments using event‑based workflows, which reduces tool complexity and eliminates the need for external CI/CD servers. 
- Because it’s cloud‑hosted and tightly connected to the repository, GitHub Actions helps teams deliver faster, maintain cleaner pipelines, and streamline the entire DevOps process.

### Key Elements:
#### Workflow : 
Workflows are configurable automated processes that you can set up in your repository in order to perform a specific task.
Eg: Deploying an application, Testing your code, Publishing a package etc..
Workflows are attached to repository and it  can have 1 or more jobs. Workflows are triggered upon events.
#### Job :
Job has one or more steps. Each Job can either run independently or parallel because each job will run on its own **Runner machine**.
#### Step :
Step can simply be a cmd, batch script file, action , docker container. You can use custom or third party actions. Steps are executed in order.
#### Action : 
A custom or third party application that performs a typically complex or repeated tasks.
Eg: Fetching code from repository and downloading onto runner machine
#### Runner machine :
  Is a machine that has runner software installed. This s/w is connected to GitHub and it will accept the jobs and execute them.
  Each runner can run a single job at a time.
- Runner machine has 3 different runners: 
    - **Github hosted runners** (linux, windows, MacOS with tools installed by Github. no control)
    - **Self hosted runners** (Full control/Custom) 
    - **Larger runners** (By Github with more CPU and RAM)
#### Events :
Triggers workflow to run. 
1. Repository Events: pull, push, Issue.
2. External Events: Sending a POST request to REST API.
3. Scheduled Times: Start everyday at 6am.
4. Manually: Push a button.

#### Activity Types : 
Some events have **sub‑events**, called activity types which describe what kind of action happened.
   Eg: `pull_request` has many activity types.
```yaml
on:
  pull_request:
    types:
      - opened
      - reopened
      - synchronize
      - closed
```
#### Event Filters : 
Event filters let you **control which specific events trigger your workflow**. 
   Eg: the push  event can be filtered by:
```yaml 
on:
  push:
    branches:
      - main
      - dev
```
#### Artifacts :
Artifacts are **files or folders generated during a workflow** that you want to save, download.
   Eg: How to upload an artifact
```yaml
- name: Upload build output
  uses: actions/upload-artifact@v4
  with:
    name: build-files
    path: build/
```
#### Job Outputs : 
Allow **one job to pass small pieces of data** (like strings, IDs, versions, paths) to another job.
   Eg: Setting an output in a job
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    outputs:
      version: ${{ steps.get_version.outputs.version }}
    steps:
      - id: get_version
        run: echo "version=1.0.3" >> $GITHUB_OUTPUT

