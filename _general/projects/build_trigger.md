---
title: Configuring Build Triggers
menus:
  general/projects:
    title: Configuring Build Triggers
    weight: 4
tags:
  - docker
  - basic
  - pro
  - jet
  - git
  - builds
  - testing
  - skipping
  - skip
  - triggers
  - triggering
  - trigger
categories:
  - Projects
  - Testing
  - Configuration
---

* include a table of contents
{:toc}

## Configuring Build Triggers

### Triggering Builds On Commits, Merges, And Tags

You can trigger a build when committing, merging, and pushing tags to your project.  This is the default behavior. See [working with tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) for more information on pushing tags.   


To trigger a build on commit, builds and tags:

1. Go to Project Settings.

2. Select the _Build Triggers_ tab.

3. Select the _Build on commit, merge, and tags_ radio button.

4. Click the _Save Configuration_ button.


### Triggering Builds Only On Pull Requests

You can trigger a build when opening, merging, and updating a Pull Request (PR).

To trigger a build only on PRs:

1. Go to Project Settings.

2. Select the _Build Triggers_ tab.

3. Select the _Build only on PR events_ radio button.
![Build only on PRs]({{ site.baseurl }}/images/general/build_only_PR.png)
4. Click the _Save Configuration_ button.

Note: The following environment variables are populated after the _Build only on PR events_ configuration is saved:
* CI_PR_NUMBER is populated with the pull request number.
* CI_PULL_REQUEST is populated with the URL of the pull request. 

See [CodeShip Basic Environment Variables](https://documentation.codeship.com/basic/builds-and-configuration/set-environment-variables/) or [CodeShip Pro Environment Variables](https://documentation.codeship.com/pro/builds-and-configuration/environment-variables/) for more information.

### Triggering Builds on Commits versus on Pull Requests

The following table shows when a build is triggered.
           

|                       	| Trigger a Build on Commit, Merge, Tags         |      | Trigger A Build On Pull Requests        	|
|-----------------------	|:----------------------------------------------:|:----:|:--------------------------------------------:	|
| Push a Commit                	|                       Yes                      |	|			No			|
| Push a Tag                  	|                       Yes                      |	|                      No                      	|
| Open a Pull Request   	|                       No                       |	|                      Yes                     	|
| Update a Pull Request 	|                       Yes                      |	|                      Yes                     	|
| Merge a Pull Request  	|                       Yes                      |	|                      Yes                     	|


## Configuring Branches

You can run builds for all branches, exclude branches from triggering builds, and run builds only for certain branches. 
The default behavior is to run builds for all branches.
 
### Excluding Branches From Triggering Builds

To exclude branches from triggering a build:

1. Go to Project Settings.

2. Select the _Build Triggers_ tab.

3. Select the _Don't run builds for these branches_ radio button.

4. Enter either full branch names like "master" for exact matches or a regular expressions like "^release.*$" for a search pattern.
![Exclude branches from running builds]({{ site.baseurl }}/images/general/exclude_branches.png)
5. Click the _Save Configuration_ button.

### Running Builds Only For These Branches

To run builds only on certain branches: 

1. Go to Project Settings.

2. Select the _Build Triggers_ tab.

3. Select the _Run build for these branches only_ radio button.

4. Enter either full branch names like "master" for exact matches or a regular expressions like "^release.*$" for a search pattern.

5. Click the _Save Configuration_ button.

## Skipping builds on the same branch

The auto-supersede feature can automatically skip builds in the queue when a newer build on the same branch comes in. By running a build based upon the latest commit, you can streamline the builds and save time. If a code change commit contains an error and a subsequent commit corrects that error, this feature can skip the build with the error and run the fixed, latest build. 

The auto-supersede feature adds a new state, _skipped_, to the build list. 

The following example shows how builds are skipped. First, you have a build that is running and another build that is queued.

![Build is queue]({{ site.baseurl }}/images/general/queued_build.png)

Next, pushing a commit queues a new build. The queued build appears on the top line of the build list. CodeShip Pro, updates the build list in real time, so the status of a build appears as _skipped_ immediately.  

![Build is queue]({{ site.baseurl }}/images/general/build_supercendence.png)

CodeShip Basic only updates a build status to skipped once the build had completed running. In the following, the build succeeded. 

![Build is queue]({{ site.baseurl }}/images/general/basic_build_supercedence.png)

You can not restart a skipped build. You can view the build on your source code management (SCM) system or go to Project Settings by clicking the drop-down arrow, 

To automatically skip builds on the same branch:

1. Go to Project Settings.

2. Select the _Build Triggers_ tabs.

3. Select the _Auto-supersede_ radio button to On.

![Turn on Auto-supersede]({{ site.baseurl }}/images/general/turn_on_auto_supersede.png)

4. Click the _Save the Configuration_ button.
