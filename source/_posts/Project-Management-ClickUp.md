---
title: Project Management & ClickUp
date: 2021-11-09 20:00:18
tags:
- About
- Documentation
- Meta
---
## Introduction to ClickUp
As soon as we started our project, we decided that we needed help managing tasks, planning meetings, and sharing files. To solve these issues, we turned to [ClickUp](https://clickup.com) - an excellent online service for project management. ClickUp has both free and paid plans, suitable for individual or enterprise-scale use.

ClickUp is based around tasks and allows you to organize those tasks by moving them into lists, and then organizing those lists into spaces. You can also create long-term goals, and add targets to those goals to stay on track. You can then add tasks to the targets. Targets can be marked as complete manually, after all tasks are completed, after a certain monetary goal has been reached, and more. Goals can be added to folders, to group like goals together.

You can then create subtasks, and add those to your tasks for a higher level of detail. Subtasks even allow you to add checklists, providing even more detail. The full ClickUp hierarchy is: 
Folders -> Goals -> Targets -> Tasks -> Subtasks -> Checklists -> Checklist Items

Tasks are not just simple to-do's either: Tasks and subtasks can be tagged and marked with a priority to organize them within their respective lists, and different statuses can be created to mark progress as the task or subtask is completed. Tasks, subtasks, and checklist items can all be assigned to users, letting them know there's work to do. ClickUp documents and other files can be attached, sharing them with other users.

## How we use ClickUp
Even though our "team" consists of two people, we have used ClickUp extensively and found it to be a powerful project management tool. We first created the following spaces:
{% asset_img ClickUpSpaces.png [Our ClickUp Spaces [Our ClickUp Spaces: Website, Hardware, Software, and Meetings]] %}

### Website
The "Website" space helps us manage this website. Here, we have one list: "Website Tasks". In this list, we create tasks for website management and the creation of new posts, such as this one. When writing new posts, we first create ClickUp documents and attach them to the respective task. This allows us to easily share the page, so we can both make edits before transferring the site to the actual code and pushing it to GitHub.
{% asset_img WebsiteTasks.png [Website Tasks [Website Tasks]] %}

We created four statuses for our tasks: ToDo, In Progress, Waiting for Review, and Done. ToDo is for tasks that have not yet been started. When a task is started, it is moved to In Progress. Then, when the task is finished, we commit the changed files to our git repository on GitHub and submit a pull request for the other user to review. Then, we link the task to the pull request using the GitHub integration for ClickUp. This automatically moves it to the Waiting for Review status. When the pull request is approved, the commit is merged into the main branch on GitHub, and the task is automatically moved to the Done status.

We have set up a GitHub Action to automatically build and deploy our site using [Hexo](https://hexo.io), a fast, simple & powerful blog framework built on Node.js. When we merge changes into the main branch on GitHub, the [Action](https://github.com/MRegirouard/AutoBoard-Website/blob/main/.github/workflows/deploy.yml) automatically builds our site and then pushes the compiled HTML files to the [gh-pages](https://github.com/MRegirouard/AutoBoard-Website/tree/gh-pages) branch in our repository. GitHub Pages then hosts this website from that branch.

Integrations between ClickUp, GitHub, and GitHub Pages provide a smooth, automated way for us to publish new content to our website, and update ClickUp tasks accordingly by marking them as Done. Because this website is not the project, and merely documentation, we wanted it to take the least amount of time possible, and these tools allow us to do that.

### Hardware
The "Hardware" space contains two lists: "Build Tasks", and "Shopping Tasks". In Build tasks, we create tasks that have to do with the physical aspect of the project, including testing sensors, soldering components, and actually constructing the AutoBoard. This list has four task statuses: ToDo, In Progress, Waiting, and Done. These statuses are similar to the Website statuses, except that "Waiting" is for waiting on things that we can't control, such as waiting for a 3D Print or a CNC job to finish.

The "Shopping Tasks" list is for things to buy. It has five statuses: To Confirm, To Order, Waiting, Ordered, and Done. To Confirm is for things we know we need to buy but are still in the process of deciding where to buy the part from or the exact part we need. To Order is for things we know where to order from, the cost, and are ready to submit to our school as a materials request. Once the request is submitted, the task is moved to Waiting, and once the order is completed, it is marked as Ordered. When the part actually arrives, it is finally moved to Done.

The "Shopping Tasks" list is a good example of the level of control ClickUp gives you over your tasks. ClickUp allows you to create custom fields in the tasks, which has proved very helpful with the Shopping Tasks:
{% asset_img ShoppingTasks.png [Shopping Tasks [Shopping Tasks]] %}

We have added the custom fields Unit Price, Quantity, Shipping, and Link. There is also a Total Cost field, which uses a formula to calculate the total cost of the part. ClickUp allows typed fields, so our cost fields are dollar amounts, and the link field is for URLs.

### Software
The "Software" space contains one list: "Software Tasks". These tasks will be for things to do for the software running on the AutoBoard, not this website. Because we have had no need for software tasks yet, this list is not fully set up and integrated with GitHub. However, we have plans to create a GitHub Action to build our Arduino code, storing a compiled binary in a separate branch of the repository. Then, using the Over-The-Air update feature in networked Arduino boards, the board will periodically check for updates to its software, and flash itself using the binary hosted on GitHub. This is just another way we are using GitHub to automate and integrate the building and deploying process of programming. It will also provide a means of updating the board if the USB port on the Arduino board becomes inaccessible in the build process.

### Meetings
The "Meetings" space contains one list of the same name. In this list, we create tasks for meetings that describe in subtasks our plans for the meeting. This allows us to have an organized agenda and use our limited time wisely. If subtasks go undiscussed in a meeting, they can simply be moved to the next one. We use a ClickUp automation to automatically move our meetings from the status "To Schedule" to "Upcoming" when scheduled, and from "Upcoming" to "In Progress" when the start time arrives. An "Incomplete Tasks" status allows us to temporarily store meetings with incomplete subtasks to be moved to the next meeting.

### Dashboards
ClickUp also allows for the creation of dashboards, where you can view tasks, embedded websites, documents, and much more in a custom layout. We had created a very useful dashboard for our project, but unfortunately, it may be viewed only a certain number of times on the basic free plan. Because of this, we can no longer use our dashboard and do not have any screenshots of this powerful feature.

## Conclusion
ClickUp provides us with all the tools necessary for project management for the AutoBoard. Between tasks, lists, statuses, and priorities, this powerful software makes organization easy. There are many more features that we haven't even explored yet, even on the free plan. Using this software will give us.
