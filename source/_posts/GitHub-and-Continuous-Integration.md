---
title: GitHub and Continuous Integration
date: 2022-01-09 13:38:20
tags:
- About
- Meta
---
# GitHub and Continous Integration

We wanted to make sure our project was open-source and as replicable as possible. To do this, we used GitHub for code hosting and version control. We also set up numerous [GitHub Actions](https://github.com/features/actions), GitHub's free CI/CD service. This page shows the ways in which we use GitHub to manage our code and automate tasks in our various repositories.

## The AutoBoard Repository
[This repository](https://github.com/MRegirouard/AutoBoard) is for the actual AutoBoard code, running on the Arduino Nano inside of it.

### Code Review System
To help cut down on bugs and accidental pushes, we have set up branch protection for the main branch in our repository. This means that it is not possible to push to the main branch, changes must instead be merged in from other branches via pull requests. This process is pretty standard with open-source projects. When committing code, we first create a new branch to work on. Then, we make the changes needed and push commits to the new branch. When work is done, we submit a pull request for code to be reviewed and then merged into the main branch. However, before the merge can take place, it must pass several checks through the GitHub Actions system. The pull request must also be approved by another contributor to the code.

#### Arduino Sketch Linting
[One of these checks](https://github.com/MRegirouard/AutoBoard/blob/main/.github/workflows/arduino-checks.yml) "lints" the Arduino sketch, running over 175 checks to make sure your project has required files and follows best practices. The tool ["checks Arduino projects for common problems"](https://blog.arduino.cc/2021/01/13/detect-problems-with-your-arduino-projects) and focuses on the "structure, metadata, and configuration of Arduino projects, rather than the code". We use the [arduino-lint-action](https://github.com/arduino/arduino-lint-action) GitHub Action to run these checks. Before merging pull requests, this mandatory check ensures that our project is formatted correctly and has the necessary files.

#### Arduino Sketch Test Compiling
[A second check](https://github.com/MRegirouard/AutoBoard/blob/main/.github/workflows/arduino-test-compile.yml) we run on committed code is the Test Compile workflow. This check prevents code that can't compile from being merged into the main branch. For this workflow, we use the [arduino-test-compile](https://github.com/ArminJo/arduino-test-compile) GitHub Action. This Action cannot, however, check for runtime bugs and other code formatting issues.

#### CodeFactor Quality Check
To check for bad programming practices and general code quality, we have [registered our repository](https://www.codefactor.io/repository/github/mregirouard/autoboard) with CodeFactor. This is an external service that can be used through [CodeFactor.io](https://www.codefactor.io/). The service integrates with GitHub and is free for public repositories. We have it set up as a third mandatory check for pull requests, to prevent poorly written code from merging into the main branch. Although CodeFactor does not run as a GitHub Action, GitHub still allows integration with this service.

CodeFactor gives a code quality rating for your code, and this can be viewed through a live-updating badge:
[![CodeFactor](https://www.codefactor.io/repository/github/mregirouard/autoboard/badge)](https://www.codefactor.io/repository/github/mregirouard/autoboard)

### Automatic Semantic Versioning and Releases
We wanted to have a system of automatically creating GitHub Releases when code for the AutoBoard was updated, and our [Arduino Compile and Release workflow](https://github.com/MRegirouard/AutoBoard/blob/main/.github/workflows/create-release.yml) does this. Our original purpose for this was to support over-the-air updates for the chess board, in case the Arduino's USB port was not accessible to manually update the code. However, wireless updates proved to be either very difficult or impossible with this board, in contrast with the ESP8266 boards we had previously worked with. However, we have kept this release process as there may be other uses for having precompiled binaries for previous code versions. These releases also have a version number that will be useful for referencing previous points in the code history. We make use of three GitHub Actions to do this: [semantic-version](https://github.com/PaulHatch/semantic-version) to tag our commits with [semantic version numbers](https://semver.org/), the [arduino-test-compile](https://github.com/ArminJo/arduino-test-compile) Action we used before, and the [action-gh-release](https://github.com/softprops/action-gh-release) Action for publishing releases. These published releases can be viewed under the [Releases](https://github.com/MRegirouard/AutoBoard/releases) section of the [AutoBoard](https://github.com/MRegirouard/AutoBoard) repository.

## The AutoBoard-Website Repository
[This repository](https://github.com/MRegirouard/AutoBoard-Website) is for this website, hosted on GitHub pages. Our website uses the Hexo blog framework.

### Code Review System
We use a code review system of peer pull request approval similar to what we use on the AutoBoard repository, discussed above. There is only one check our website pages have to pass before merging into the main branch.

#### Hexo Static File Generation Testing
To ensure that our website is never broken, we first test the Hexo static file generation [with a GitHub Actions workflow](https://github.com/MRegirouard/AutoBoard-Website/blob/main/.github/workflows/test-generate.yml). This workflow uses the [setup-node](https://github.com/actions/setup-node) Action to install Node, runs the `npm install` command to install the hexo-cli package, and then runs the `hexo generate` command to generate the static site files. If this generation fails to due configuration file or formating errors, the pull request will not be able to be merged into main.

### Hexo Static File Generation and Deployment
Before our new Hexo blog pages can show up on the actual website, they need to be converted into static HTML pages to be hosted by GitHub Pages, and we use [another workflow](https://github.com/MRegirouard/AutoBoard-Website/blob/main/.github/workflows/deploy.yml) for this. To run the Hexo commands, we use a GitHub Action, [hexo-action](https://github.com/sma11black/hexo-action). This will use Hexo to run the generate and deploy commands, pushing static files to the [gh-pages](https://github.com/MRegirouard/AutoBoard-Website/tree/gh-pages) branch of our repository that GitHub Pages looks at to host this website.

## The hexo-theme-cactus Repository
We are using the Cactus theme for Hexo for this website, and we had to fork the [theme](https://github.com/probberechts/hexo-theme-cactus) to do it. We set up [this repository](https://github.com/MRegirouard/hexo-theme-cactus) as a git submodule inside the AutoBoard website.

### Code Review System
We have not yet set up a code review system in this repository. We may not do this, as our theme is pretty much fully configured and no more changes have to be made.

### Automatic Submodule Updates
We set up [another GitHub workflow](https://github.com/MRegirouard/hexo-theme-cactus/blob/main/.github/workflows/push-updates.yml) to automatically update this submodule inside our website repository. When the theme's main branch receives a push, the workflow checks out our website repository, and recursively updates all submodules inside of it to the latest commit on their respective repositories. We are only using one submodule right now, the theme submodule, but if we add more later, this workflow will update those as well.
