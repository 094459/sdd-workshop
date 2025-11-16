![Header - picture of Kiro ghost and title](/images/header.png)

# Creating new applications with spec driven development

In this lab we are going to apply everything we have learned in the previous sections, and use spec driven development to build a simple web application. We are going to start fresh with a new directory and build up from the ground up to walk you through the workflow. The goal of this lab is to:

* provide a hands on overview of the spec driven workflow
* understand dependencies and ways you can interact and influence with the workflow
* look at the spec lifecycle

At the end of this lab, you will have completed both creating and updating your first spec driven project, for a new (greenfield) application. In the next lab you will apply spec driven workflows to work with an existing project (brownfield).

---


![Lab](/images/lab-header.png)

In this lab we are going to set our project up with everything we need.

#### Lab-01

![Lab](/images/lab-header-end.png)


1. Create a new project workspace on your machine - I am going to call mine "~/kiro/workshop-greenfield"

```
mkdir ~/kiro/workshop-greenfield && cd workshop-greenfield
```

2. Initialize git - we are going to use git to track all specification and code changes within our project - this will allow us to track and revert to a given state as we need.

```
git init
```

3. Now launch Kiro

```
kiro .
```

With Kiro launched we are ready for the next lab.

----

![Lab](/images/lab-header.png)

In this lab we are going to define some steering documents we want Kiro to use as it starts to architect and design solutions against our requirements. We are going to implement two kinds of steering documents so you can see how to configure them. We will create a globally scoped steering document that an organization might typically use to control certain aspects of projects across your organization. Then we will create one that perhaps a developer might want to implement as their own preferences.

#### Lab-02

![Lab](/images/lab-header-end.png)


1. From Kiro, make sure you are on the Kiro screen (click on the Kiro icon on the left hand activity bar) - the "Agent Steering" panel should be empty.

2. Click on the "+" icon, which will bring up the steering document creation menu.

![Steering document pop up menu](/images/adding-steering-menu.png)

3. Select the first option "Workspace agent steering" and in the dialog that appears next, you need to enter a name for this steering file. The rule of thumb here is that it should be short but descriptive enough to help someone know what this might be. We are going to call ours "Project-Standards", so type that and then press enter.

4. This will bring up steering file in the editor. Replace the content with the following:

```
---
inclusion: always
---

# Coding Preference

You have a preference for writing code in Python. 

## Python Frameworks

When creating Python code, use the following guidance:

- Use Flask as the web framework
- Follow Flask's application factory pattern
- Use Pydantic for data validation
- Use environment variables for configuration
- Implement Flask-SQLAlchemy for database operations

## Project Structure and Layout

Use the following project structure

├ app
	├── src
	├── src/static/
	├── src/models/
	├── src/routes/
	├── src/templates/
	├── src/extensions.py

# Python Package Management with uv

Use uv exclusively for Python package management in all projects.

## Package Management Commands

- All Python dependencies **must be installed, synchronized, and locked** using uv
- Never use pip, pip-tools, poetry, or conda directly for dependency management

Use these commands

- Install dependencies: `uv add <package>`
- Remove dependencies: `uv remove <package>`
- Sync dependencies: `uv sync`

## Running Python Code

- Run a Python script with `uv run <script-name>.py`
- Run Python tools like Pytest with `uv run pytest` or `uv run ruff`
- Launch a Python repl with `uv run python`

```

Save the file and you should now have your steering file setup. What have we done? We have provided Kiro that when its thinking about design/code, that it needs to:

- use Python
- use specific Python frameworks
- use uv for package and dependency management

5. From Kiro's IDE, bring up the command palette (on a Mac this is SHIFT + COMMAND + P, and Windows it is CTRL + SHIFT + P) and from the dialog box type "Kiro" and then select "Kiro: Docs force re-index" option.

![re-indexing steering docs in Kiro](/images/kiro-reindex-docs.png)

6. In the Kiro IDE, click on the "+" at the top to open a new session, select Vibe. In the chat interface click on the # and select "Steering" which should bring up the steering file you created. Select this, and you should see it appear in a highlighted block in the chat interface.

Now enter the following in the chat window. 

```
Show (don't create) me some code that implements a simple API that returns a json date object
```

Review the output - you should see that it has respected the preferences we have just defined.

7. From the Kiro activity bar, select the Source Control icon. In the dialog box enter "Steering file created" and then click on the Commit button. When the menu comes up, choose Yes. You should now see your first commit in the graph in the bottom panel. Switch back to the Kiro screen by clicking on the Kiro icon in the activity bar.

---

![Lab](/images/lab-header.png)

We are going to add a number of MCP Servers to show you how you can configure these. We are going to be using the AWS Docs Knowledgebase MCP Server to provide us with the latest AWS docs, and the AWS Pricing MCP Server to provide us with Pricing information.

#### Lab-03

1. From the Kiro tab, click on the edit icon in the MCP Servers widget

2. This will open up the "mcp.json" file, and you should notice that there are two selection boxes: User Config and Workspace Config - click on "Workspace Config" and you should notice that the file path changes.

3. Replace the contents of the mcp.json file in the editor with the following

```
{
  "mcpServers": {
    "awslabs.aws-pricing-mcp-server": {
      "command": "uvx",
      "args": [
        "awslabs.aws-pricing-mcp-server@latest"
      ]
    },
    "awslabs.aws-documentation-mcp-server": {
      "command": "uvx",
      "args": [
        "awslabs.aws-documentation-mcp-server@latest"
      ]
    }   
  }
}
```

4. Save the file - it will take a few minutes as Kiro will be downloading the MPC libraries via uvx. When it is finished, you should now see several MCP servers in the MCP Server widget.

5. Right click on one of the MCP Servers - you will see you are able to disable this MCP Server, as well as enable/disable the tools they make available. Right click and enable all the tools.

6. Explore your project workspace under ".kiro" and look for the MCP Server configuration file.


![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

We are going to develop a new application using the spec driven approach. The application itself is not important, but is a useful way to show the SDD workflow. We are going to create a deliberately simplified application (a web application to manage our tasks) so that we can complete a full iteration in the time of the workshop. 

#### Lab-04

1. We are going create an initial specification,so from the "Lets Build" panel, make sure that "Spec" is selected.

2. In the dialog box, enter the following

"I want to create a simple todo web application to track things I need to do"

3. Review what happens. Kiro will begin the spec workflow, and will create a new spec for you by generating a new "requirements.md" file. This might take 2-3 minutes, so a great time to grab your favorite drink and rehydrate!

4. Switch to the File Browser tab, and you should see a new directory called ".kiro" which now contains a new directory which will be named after your spec. What is your directory called? Within this directory you should also see the requirements.md file.

5. Switch back to the Kiro tab, and you will notice that in the top left of the Kiro widgets you will see your new spec listed. Click on this, which should reveal your requirements.md file in the main editor. You should also see that there are three boxes that contain the three steps of the workflow: requirements, design, and tasks.

6. Look at the chat interface, do you see a button with "Move to design phase"? - **don't** click on this as we need to first of all review our requirements.md file which we will do in the next lab.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

With the first artefact (requirements.md) created, we now need to review and refine. In this lab we will look at the different approaches you can take and how to then move to the next step in the workflow.

#### Lab-05

1. Open up the requirements.md and review the introduction, which expands upon the initial prompt. You will typically not need to review/edit this section, but it is worth making sure this has aligned with the feature you are trying to create.

2. Review each Requirement and User Story - do they make sense? Do they include things that you would have expected, and maybe some you did not? Are the requirements defined to the right level (i.e. not over engineered)?

3. Add a new requirement of your own. We can do this one of two ways. We can directly edit the file, or we can ask Kiro to add a new requirement via the chat interface. Lets add a new requirement to add a help page to this application (assuming this requirement was not generated after the initial generation)

First of all try via the chat interface and enter the following:

"Can you add a new requirement that adds a help page to help users understand how to use the application"

Review the output and check the requirements.md file. It should now have a new requirement. Does it look ok? Once you have looked at this delete this new requirement - don't worry, we are going to add it again, but this time by directly editing the document.

4. You can directly update the requirement.md if you prefer. Edit your requirements.md file and append the following new requirement to the end, making sure to change the number "6" below so that its the next in sequence.

```
### Requirement 6

**User Story:** As a User, I want to access a help page, so that I can understand how to use the application

#### Acceptance Criteria

1. THE Todo Application SHALL provide a navigation control to access the help page
2. WHEN the User navigates to the help page, THE Todo Application SHALL display instructions for creating todo items
3. WHEN the User navigates to the help page, THE Todo Application SHALL display instructions for marking items as complete
4. WHEN the User navigates to the help page, THE Todo Application SHALL display instructions for deleting items
5. THE Todo Application SHALL provide a navigation control to return from the help page to the Task List
```

Save the document.

5. As we have made this change ourself, we need to nudge Kiro and remind it to reload the requirements. From the chat interface, type in the following:

"I have updated the requirements - please reload and review"

> We did not need to do this when we asked Kiro to add a new requirement via the chat interface. This is something to think about as you start to work more in creating your specs. 

Review the output to confirm that Kiro has understood the changes you have made - it will typically echo these back to you.

6. We are now ready to proceed to the design phase. Click on the "Move to design phase" button in the chat interface. If that has disappeared, type "Move to the design phase" in the chat interface and hit return.

Kiro should start to work on the next artefact, the design.md, which we will dive into in the next lab.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

Kiro will now use the steering documents we created initially, together with the requirements we defined in the requirements.md file to build out an initial architecture and design. In this lab we are going to dive into this.

#### Lab-06

![Lab](/images/lab-header-end.png)

1. In the chat interface take a look at the output of the generation process. It should provide some details as to what Kiro has done when creating the design.md file.

2. If the design.md document is not already loaded into the main editor window, click on the Kiro icon on the activity bar, select your spec in the top left and this should allow you to navigate to the design document.

![Navigating to the design document](/images/kiro-design.png)

Alternatively you can switch to the file explorer, and you will see that you now have a new document in the spec directory that you explored in a previous lab. 

![opening design via file explorer](/images/kiro-design-via-explorer.png)

3. When reviewing specs, it is easier to temporary remove the chat interface. Kiro makes this easy by providing some icons in the top right of the IDE. You can see that we can toggle the chat interface by clicking on the chat icon.

![toggling chat interface](/images/kiro-window-manager.png)

Click on this to expand the editor so that its full screen.

4. Go through the design document and review the design. Check for the following:

- Did it respect the steering document we created in a previous lab?
- Did the structure look like the layout we defined in the steering doc?
- Does the data model look reasonable? Data models are an important context anchor, so it is always worth checking and double checking that the data model looks good
- Review the routes/APIs that are created - do they map to our requirements?
- Look at the design decisions - do they make sense?

5. In this lab we are not going to make any changes to the design, unless you find issues with what has been produced in your design.md. We are going to proceed to the next step in the workflow, implementation. To do this, we can click on the "Move to implementation phase" in the chat interface, or if that is not present, we can type in the chat interface:

"Move to implementation phase"

and hit return. This is going to start the next step in the workflow, and Kiro is going to start creating the next artefact, the tasks.md. This might take 2-3 minutes.

----

![Lab](/images/lab-header.png)

In this lab we will take a look at how Kiro has taken our requirements, together with the design, and creates an implementation plan. This plan outlines all the tasks needed to create our application. Each task will be used by Kiro to generate code.

#### Lab-07

1. Review the chat interface again. You should notice that you are being asked a question. It should look something like this:

![MVP or Prod](/images/kiro-mvp.png)

Kiro provides a way of marking tasks as required or optional. If we were testing Kiro out on an idea, we might only want to create an MVP. What Kiro will do is the review the tasks it has created and mark some of these as optional (typically this will be things like tests)

Click on the "Keep optional tasks (faster MVP)" button.

2. Review the tasks.md in the main editor (use the chat icon to expand the editor like we showed in the previous lab). Review the tasks.

- Find the tasks that have been marked as optional - these are greyed out, and easily identifiable as they have an "*" before the task number
- Review the high level task activity, and the order in which they are sequenced
- Look at the linked requirements and check back to the requirements.md file to make sure they align
- Notice that above each task we have a "Start task" link - don't click on these yet.

3. From the source control icon in the activity bar, we are going to check in our changes. In the changes window enter "spec-workflow-completed" and click on the commit button. After you confirm, it should look something like this.

![committing spec to source control](/images/kiro-spec-commit-source.png)

Using source control to version our Kiro project allows us to revert back and maintain state between our spec and any other artifacts created. This is our baseline, the start of the project before we have created any code.

> You should use your own preferred way of managing artifacts if you have them - the above example is a simplified approach just for the purpose of this workshop

4. We are now ready to get Kiro to start generating some code from our spec. From the task.md, go to the very first task, and click on the "Start Task" icon. You should see the task.md update in the main editor change, and you should see the task change like the following:

![task started](/images/kiro-task-in-progression.png)

As you do this, pay attention to the chat interface. Whilst Kiro will be generating code, you will still be in the driving seat and Kiro will be prompting you as it asks your permission to run and execute various commands.

5. At some point you will see a message like this appear:

![asking permission to run commands](/images/kiro-run-commands.png)

We have four options when Kiro asks us that it needs to do something:

- Edit the command -we can use the editor to make changes, which can be useful if we see that Kiro has made a mistake in the command
- Reject - we can block Kiro from running this command
- Trust command and Accept - we can add this command to Kiro's trusted commands (see more of this in the [Kiro Tools Reference section](/workshop/05-tools-and-resources.md))
- Accept command - allow Kiro to run the command

During this lab we are going to click on the "Accept command". So as it appears, click on that icon. You should now see the command run, and the output proceed in the chat interface.

6. After a short period of writing code, Kiro will announce that it has completed the task. It will typically provide a short summary of what it has done, and you will notice that in the main editor, the first task should now show as "Task Completed"

![task completed](/images/kiro-task-completed.png)

7. You should notice that for any completed task:

- All items under the task should show as completed, with the task box changing from [ ] to [x]
- You will see a "View Changes" link next to the Task Completed text - this will allow you to view a summarized diff of code changes made
- You will see a "View Execution" link which will take you to the start of the chat history where a given task started, allow you to review the commands that were run and the output

8. Click on the source control icon in the activity bar - you should see a list of all changes made. This will include code but also changes to your spec files.

In the message window enter "Task One" and click on Commit, answering Yes when prompted. 

You should now see Task One appear in the graph. Click back on the Kiro icon in the activity bar to get back to the Kiro screen.

9. We started the first task by clicking on the "Start task" link, but we can also do this via the chat interface. In the chat interface, type the following:

"Start the next task"

You should see Kiro begin the next task. You will follow the same process as for the first task.

- Monitor activity of what Kiro does
- When prompted, help Kiro to review and act
- Review the task summary

When finished, repeat the step and add a new commit in source control, naming the commit message after each task.

10. We can also use the chat interface to complete a number of tasks if we think there are a number of related tasks that can be executed together. We do this from the chat interface.

"Start tasks three and then four"

Review the chat interface. You should see now that it starts working on Task 3 and when complete Task 4. Once complete, add another commit (call this one Tasks three and four)

11. You might be wondering what happens if I click on multiple "Start Tasks" links? Kiro has a queue in which it will queue tasks as they are started. In the chat interface, you will see the following icon which will display the current task queue.

![Kiro task queue icon](/images/kiro-task-queue-icon.png)

If you click on another task before the current task has finished, it will do nothing. You will see it however in the task queue.

![view task queue](/images/kiro-task-queued.png)

11. Now work through the remaining tasks. Experiment with using the chat interface, the UI links. Make sure you commit changes to source control as you progress.

This will take around 20 minutes to complete, so feel free to grab some refreshments or stretch yours legs whilst you complete the remaining tasks.

![Lab](/images/lab-header-end.png)


----

![Lab](/images/lab-header.png)

In previous labs we showed how you can use the chat interface to change (add) the requirements.md and we are now going to do the same thing to add a task to the implementation plan file, tasks.md.

In the previous lab we Kiro generated code from our specs. How do we now test our application? Kiro may (or may not) have created a README based on the tasks defined in your tasks.md. In most cases it does not create this so we are going to use the chat interface to add a new task to our task list.

#### Lab-08

1. From the chat interface, type the following:

"Add a new task that generates a README file that explains how to start/run this application"

After a few moments, you should see that you now have a new task that has appeared in your task list.

2. Click on the "Start Task" link to complete the task, and keep an eye on the chat interface. If Kiro asks you for help, guide it to completing this task.

You should start see Kiro reading files from the project as it collects information and formulates a README file. This might take around 2-3 minutes to complete.

3. Review the finished README file that is created. Look for how to run the application. From the Terminal section of Kiro, use the command to start the application. It should look something similar to this:

```
$ cd app
$ uv run python run.py
 * Serving Flask app 'src'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on http://127.0.0.1:5000
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 103-566-284
```

Open up a web browser, and open up http://127.0.0.1:5000

After testing the application, shut it down (CTRL + C).

4. As with the previous tasks that you completed, use the source control page to commit changes (you can label the commit message "Adding a README file").

Congratulations, you have now completed your first spec driven project. Now lets look at how we make changes or add new features.

![Lab](/images/lab-header-end.png)

----

![Lab](/images/lab-header.png)

It is quite common that we might need to change or add new requirements after we have completed an iteration of the spec driven development workflow. In this lab we are going to show you how this works. We are going to add a new requirement to add a Contact Us page and then work through how Kiro supports this change through the spec driven workflow.

#### Lab-09

1. Make sure any files that are open in the editor are close, and that you have stopped the application. Open up the "requirements.md" file in the main editor.

2. From the chat interface, enter the following prompt:

"Add a new requirement to add a Contact Page"

Review the output from the chat interface, and then review the requirements.md file for changes. A new requirement should be added to the end of the requirements.md file. This is an example of what it might look like:

```
### Requirement 7

**User Story:** As a User, I want to access a contact page, so that I can submit feedback or get support for the application

#### Acceptance Criteria

1. THE Todo Application SHALL provide a contact page accessible from the main interface
2. THE Todo Application SHALL display a contact form with fields for name, email address, and message
3. WHEN the User submits the contact form with all required fields completed, THE Todo Application SHALL accept the submission
4. WHEN the User submits the contact form with missing required fields, THE Todo Application SHALL reject the submission and display validation errors
5. THE Todo Application SHALL display a confirmation message after successful form submission
```

3. For the purpose of this workshop, we want a much simpler Contact Us page, one that just displays some text and contact details (phone and email), so lets change this directly by editing the requirements.md file. Use the following, making sure you check the requirement number and adjust it so that it is the next in sequence.

```
### Requirement 7

**User Story:** As a User, I want to access a contact page, so that I can find contact information for support

#### Acceptance Criteria

1. THE Todo Application SHALL provide a contact page accessible from the main interface
2. THE Todo Application SHALL display a telephone number on the contact page
3. THE Todo Application SHALL display an email address on the contact page
4. THE Todo Application SHALL display supporting text with instructions for contacting support
```

Save the file after you have made the change.

4. As we have made a change ourselves, we now need to ask Kiro to re-load the requirements via the chat interface.

"I have updated the requirements.md so please re-load and check"

You should get confirmation and a summary from Kiro.

5. Click on the "2. Design" link at the top of the editor which will bring up the design document. You will notice that next to this on the right hand side is a "Refine" link.

Move your cursor and hover (do not click yet) over the Refine link - you will notice that it says "Refresh your design based on the requirements". As you make changes to your requirements, Kiro needs to potentially update the design. In this particular change, as it is simple it is unlikely that there will be significant changes to the design.

Click on the Refine link, and watch the output in the chat interface. You should notice that it:

- reviews any changes it identifies in the requirements and compares it against the design document
- provides feedback of changes needed to be made
- makes updates to the design.md

6. We can review changes quickly by using the diff feature in Kiro. You will have seen this as we have been working, but as we were generating files from scratch, the diff feature was not so useful. When we already have stuff in our design.md, the diff feature allows us to quickly see and review changes.

![view diff](/images/kiro-diff.png)

Take a few moments to review the diff and see how the design has been updated. To close the diff, just located the X in the main editor and you will close this view.

7. In the chat interface, you should now see that you will be prompted on whether you want to "Move to implementation plan". Click on that link. Kiro will begin working, and after 1-2 minutes, you should now see that your tasks.md file has been updated with new tasks.

You can use the diff icon to quickly view the changes in the tasks.md as you did in the previous steps with the design updates.

8 You will be prompted whether you want to implement all tasks or just keep optional tasks for MVP, so click on the optional tasks for MVP.

Once that has finished, the output in the chat interface will tell you that you can now being completing the new tasks. As we did before, we can do this via the UI (by clicking on the Start Task) or via the chat interface.

"Complete any outstanding tasks"

After a short while, Kiro will begin working through these new tasks. Again, you might be prompted as Kiro needs to request permissions to run various commands. 

9. When Kiro has completed this new task, re-start the application and see if you now have a Contact Us page.


![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

We can create many specs for a given application. In this next lab we are going to create a completely new spec, building on from the code that Kiro has already generated for us. We are going to add a new feature to export our todo's in csv format.

#### Lab-10

1. Ensure the application is stopped, and that all open files are closed in the editor. Switch to the Kiro tab using the Kiro icon in the activity bar.

2. Located the Specs section in the top left, which should already have the first spec we created (todo-web-app or something similar). Click on the "+" on the right hand side.

3. From the dialog that pops up, enter the following text:

"Create a new spec that add a new capability to allow me to export my todos as a csv file"

Review the output in the chat interface. You should notice the following text appear"

> I can see you already have a spec for the todo-web-app. Let me check the existing spec to understand the current feature set, then I'll create a new spec for the CSV export capability.

Kiro will review existing specs you have created. In our case, it is going to create a new spec. However, if Kiro thinks that what you are asking for might be better as a new requirement to an existing spec, it will inform you and start that process (which we have done in previous labs)

4. After a few moments, we should now see a new requirements.md appear in the main editor. If you look at the left hand side in the Spec section, you will also see that we have a new spec listed (csv-export or something similar). If you switch to the file explorer, you will see that under the .kiro directory, under specs you now have a new directory that has been created for this new spec.

5. Switch back to the Kiro view, and now work through the three steps of the workflow to complete this new spec. This will take around 5-10 minutes. As you do this, look for the following:

- notice how Kiro checks the existing application functionality during the three phases of the workflow
- as this is a net new set of specs, these are blank documents

6. Once Kiro has completed all the tasks, start the application and test out this new feature.


![Lab](/images/lab-header-end.png)

----

### Lab Completed

Congratulations, you have now completed the first set of labs and are now ready to explore the world of spec driven development. If you found this workshop useful (or not) please let me know - this will help me justify creating more workshops like this. Please complete [this short survey](https://pulse.aws/promotion/VWOXGKXF) - thank you!

Click on [Existing Codebases](/workshop/04-brownfield.md) to proceed to the next section where we show how you can use SDD with existing code you have

Click on [Home](/README.md) to go back to the landing page


---

# Additional reading material

* [Official Kiro docs](https://kiro.dev/docs/)

* [Your first project on Kiro](https://kiro.dev/docs/getting-started/first-project/)

* [Spec best practices](https://kiro.dev/docs/specs/best-practices/)

