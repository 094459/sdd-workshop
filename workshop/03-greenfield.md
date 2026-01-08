![Header - picture of Kiro ghost and title](/images/header.png)

# Creating new applications with spec driven development

In this lab we are going to apply everything we have learned in the previous sections, and use spec driven development to build a simple web application. We are going to start fresh with a new directory and build up from the ground up to walk you through the workflow. The goal of this lab is to:

* provide a hands on overview of the spec driven workflow
* understand dependencies and ways you can interact and influence with the workflow
* look at the spec lifecycle

At the end of this lab, you will have completed both creating and updating your first spec driven project, for a new (greenfield) application. In the next lab you will apply spec driven workflows to work with an existing project (brownfield).

**Make sure you have your dependencies installed**

Before beginning, make sure you have installed the dependencies required for this workshop as outlined in the [README](/README.md).

---

![Lab](/images/lab-header.png)

In this lab we are going to set our project up with everything we need.

#### Lab-01

![Lab](/images/lab-header-end.png)


1. Create a new project workspace on your machine. Create a directory called "kiro" and from within that directory, create a project workspace called "sdd-greenfield". Use the following commands if you are using a Linux or MacOS machine, or use an equivalent command or Windows Explorer to create these directories.

Open up a new terminal, and from your home directory enter the following commands:

```
mkdir ~/kiro/sdd-greenfield && cd sdd-greenfield
```

2. Initialize git - we are going to use git to track all specification and code changes within our project - this will allow us to track and revert to a given state as we need.

```
git init
```

3. Now launch Kiro

```
kiro .
```

With Kiro launched we are ready for the next lab. Before you proceed though, spend some time navigating and exploring Kiro.

----

![Lab](/images/lab-header.png)

In this lab we are going to create a steering document that we want Kiro to use as it starts to architect and design solutions against our requirements.

#### Lab-02

![Lab](/images/lab-header-end.png)


1. From Kiro, make sure you are on the Kiro screen (click on the Kiro icon on the left hand activity bar) - the "Agent Steering" panel should be empty.

2. Click on the "+" icon, which will bring up the steering document creation menu.

![Steering document pop up menu](/images/adding-steering-menu.png)

3. Select the first option "Global agent steering" and in the dialog that appears next. This will configure a project specific steering file. Enter a name for this steering file. The rule of thumb here is that it should be short but descriptive enough to help someone know what this might be. We are going to call ours "Project-Standards", so type that and then press enter.

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

## Local and Prod configurations

- Run local development setups on 127.0.0.1:5001
- Run production configurations via gunicorn
- Configure via env variables

## Python Package Management with uv

- Use uv exclusively for Python package management in all projects.
- All Python dependencies **must be installed, synchronized, and locked** using uv
- Never use pip, pip-tools, poetry, or conda directly for dependency management
- Use these commands - Install dependencies: `uv add <package>`,  Remove dependencies: `uv remove <package>` and Sync dependencies: `uv sync`
- Run a Python script with `uv run <script-name>.py`
- Run Python tools like Pytest with `uv run pytest` or `uv run ruff`
- Launch a Python repl with `uv run python`
- Configure [tool.hatch.build.targets.wheel] packages with the correct value for the project

```

Save the file and you should now have your steering file setup. What have we done? We have provided Kiro that when its thinking about design/code, that it needs to:

- use Python
- use specific Python frameworks
- use uv for package and dependency management

> **Where's my steering file?** You might be wondering why you cannot see your steering file in your project workspace. This is because we created a global steering file, and these reside outside of your project workspace in the **".kiro"** directory. Have a look at this directory in a separate terminal session and you will see your steering file.

5. As we have created a new steering document, we can update Kiro's document index to make sure that it includes this new file we have created. From Kiro's IDE, bring up the command palette (on a Mac this is SHIFT + COMMAND + P, and Windows it is CTRL + SHIFT + P) and from the dialog box type "Kiro" and then select "Kiro: Docs force re-index" option.

![re-indexing steering docs in Kiro](/images/kiro-reindex-docs.png)

6. In the Kiro IDE, click on the "+" at the top to open a new session, select Vibe. Now enter the following in the chat window. 

```
Show (don't create) me some code that implements a simple API that returns a json date object
```

Review the output - you should see that it has respected the preferences we have just defined.

---

![Lab](/images/lab-header.png)

We are going to develop a new application using the spec driven approach. The application itself is not important, but is a useful way to show the SDD workflow. We are going to create a deliberately simplified application (a web application to manage our tasks) so that we can complete a full iteration in the time of the workshop. 

#### Lab-03

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

#### Lab-04

1. Open up the requirements.md and review the introduction, which expands upon the initial prompt. You will typically not need to review/edit this section, but it is worth making sure this has aligned with the feature you are trying to create.

2. Review each Requirement and User Story - do they make sense? Do they include things that you would have expected, and maybe some you did not? Are the requirements defined to the right level (i.e. not over engineered)?

3. Add a new requirement of your own. We can do this one of two ways. We can directly edit the file, or we can ask Kiro to add a new requirement via the chat interface.

Lets add a new requirement to add a help page to this application (assuming this requirement was not generated after the initial generation)

First of all try via the chat interface and enter the following:

"Can you add a new requirement that adds a help page to help users understand how to use the application"

Review the output and check the requirements.md file. It should now have a new requirement. Does it look ok? Once you have looked at this delete this new requirement - don't worry, we are going to add it again, but this time by directly editing the document.

4. You can also directly update the requirement.md if you prefer. Edit your requirements.md file and remove the new requirement that was added in the previous step, and append the following new requirement in its place, making sure to change the number of the requirements so that its the next in sequence.

```
### Requirement {next in sequence}

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

> **Tip!** You do not need to do this when we asked Kiro to add a new requirement via the chat interface. This is something to think about as you start to work more in creating your specs. 

Review the output to confirm that Kiro has understood the changes you have made - it will typically echo these back to you.

6. We are now ready to proceed to the design phase. Click on the "Move to design phase" button in the chat interface. If that has disappeared, type "Move to the design phase" in the chat interface and hit return.

Kiro should start to work on the next artefact, the design.md, which we will dive into in the next lab.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

Kiro will now use the steering documents we created initially, together with the requirements we defined in the requirements.md file to build out an initial architecture and design. In this lab we are going to dive into this.

#### Lab-05

1. In the chat interface take a look at the output of the generation process. You might notice that you get prompted by Kiro to use one of its internal tools (web_search) as it looks to get external information about Flask best practices. You will need to click on the green triangle to accept and let Kiro run its search. You may need to do this several times.

It should provide some details as to what Kiro has done when creating the design.md file, before inviting you to review the design.md file.

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

We are going to quickly dive into Correctness Properties in the next lab, so keep the design document open.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

One of the big challenges with using AI coding assistants is making sure that the code that we ask them to generate actually gets produced. Correctness is how Kiro helps answer this question, or more specifically, how it produces code that matches your intent.

You can read more about property based testing and how it works in Kiro by [checking out the documentation](https://kiro.dev/docs/specs/correctness/?trk=71546b8e-c969-4ead-aa9f-9cd06f6d8610&sc_channel=el
)

#### Lab-06

1. Review the chat history - you should find that Kiro has output about formalizing requirements to correctness properties. What are these you might be wondering, lets dive deeper.

2. From the open design.md document, navigate down to the heading "Correctness Properties". You will notice that a number of items listed. Each correctness property that is listed validates a specific requirement. Correctness properties have not been created for everything. A property is a universal statement about how your system should behave. Kiro extracts properties from your EARS-formatted requirements (e.g. "WHEN a user types a task description and presses Enter or clicks an add button, THE Todo_System SHALL create a new Todo_Item and add it to the list", the **SHALL** is key here), and then determines which can be logically tested.

During the execution phase, Kiro will then generate hundreds or thousands of random test cases when you choose to run them. If you look further in the design.md document, you will see that Kiro defines which tools and their configuration (Hypothesis).

3. We are not going to make any changes to the design. We are going to proceed to the next step in the workflow, implementation. To do this, we can click on the "Move to implementation phase" in the chat interface, or if that is not present, we can type in the chat interface:

"Move to implementation phase"

and hit return. This is going to start the next step in the workflow, and Kiro is going to start creating the next artefact, the tasks.md. This might take 2-3 minutes.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

In this lab we will take a look at how Kiro has taken our requirements, together with the design, and creates an implementation plan. This plan outlines all the tasks needed to create our application. Each task will be used by Kiro to generate code.

#### Lab-07

1. Review the chat interface again. You should notice that you are being asked a question. It should look something like this:

![MVP or Prod](/images/kiro-mvp.png)

Kiro provides a way of marking tasks as required or optional. If we were testing Kiro out on an idea, we might only want to create an MVP. What Kiro will do is the review the tasks it has created and mark some of these as optional (typically this will be things like tests, including the property correctness tests). 

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

As you do this, pay attention to the chat interface. Whilst Kiro will be generating code, you will still be in the driving seat and Kiro will be prompting you as it asks your permission to run and execute various commands. At some point you will see a message like this appear:

![asking permission to run commands](/images/kiro-run-commands.png)

We have four options when Kiro asks us that it needs to do something:

- Edit the command -we can use the editor to make changes, which can be useful if we see that Kiro has made a mistake in the command
- Reject - we can block Kiro from running this command
- Trust command and Accept - we can add this command to Kiro's trusted commands (see more of this in the [Kiro Tools Reference section](/workshop/05-tools-and-resources.md))
- Accept command - allow Kiro to run the command

During this lab we are going to click on the "Accept command". So as it appears, click on that icon. You should now see the command run, and the output proceed in the chat interface.

5. After a short period of writing code, Kiro will announce that it has completed the task. It will typically provide a short summary of what it has done, and you will notice that in the main editor, the first task should now show as "Task Completed"

![task completed](/images/kiro-task-completed.png)

You should notice that for any completed task:

- All items under the task should show as completed, with the task box changing from [ ] to [x]
- You will see a "View Changes" link next to the Task Completed text - this will allow you to view a summarized diff of code changes made
- You will see a "View Execution" link which will take you to the start of the chat history where a given task started, allow you to review the commands that were run and the output

6. Click on the source control icon in the activity bar - you should see a list of all changes made. This will include code but also changes to your spec files.

In the message window enter "Task One" and click on Commit, answering Yes when prompted. 

You should now see Task One appear in the graph. Click back on the Kiro icon in the activity bar to get back to the Kiro screen.

7. We started the first task by clicking on the "Start task" link, but we can also do this via the chat interface. In the chat interface, type the following:

"Start the next task"

You should see Kiro begin the next task. You will follow the same process as for the first task.

- Monitor activity of what Kiro does
- When prompted, help Kiro to review and act
- Review the task summary

When finished, repeat the step and add a new commit in source control, naming the commit message after each task.

8. We can also use the chat interface to complete a number of tasks if we think there are a number of related tasks that can be executed together. We do this from the chat interface.

"Start tasks three and then four"

Review the chat interface. You should see now that it starts working on Task 3 and when complete Task 4. Once complete, add another commit (call this one Tasks three and four)

9. You might be wondering what happens if I click on multiple "Start Tasks" links? Kiro has a queue in which it will queue tasks as they are started. In the chat interface, you will see the following icon which will display the current task queue.

![Kiro task queue icon](/images/kiro-task-queue-icon.png)

If you click on another task before the current task has finished, it will do nothing. You will see it however in the task queue.

![view task queue](/images/kiro-task-queued.png)

10. Now work through the remaining tasks. Experiment with using the chat interface, the UI links. Make sure you commit changes to source control as you progress.

This will take around 10-15 minutes to complete, so feel free to grab some refreshments or stretch yours legs whilst you complete the remaining tasks.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

It is quite common that we might need to change or add new requirements after we have completed an iteration of the spec driven development workflow. In this lab we are going to show you how this works. We are going to add a new requirement to add a Contact Us page and then work through how Kiro supports this change through the spec driven workflow.

#### Lab-08

1. Make sure any files that are open in the editor are close, and that you have stopped the application. Open up the "requirements.md" file in the main editor.

2. From the chat interface, enter the following prompt:

"Add a new requirement to this current spec add a Contact Page"

Review the output from the chat interface, and then review the requirements.md file for changes. It might add a single or several new requirements to the end of the requirements.md file. 

For the purpose of this workshop, we want a much simpler Contact Us page, one that just displays some text and contact details (phone and email), so lets change this directly by editing the requirements.md file. Edit the updates Kiro added to remove the new added requirement or requirements, and then replace it with the following, making sure to update the {Next in Seq} with the next sequential number based on the previous requirements in your requirements.md


```
### Requirement {Next in Seq}

**User Story:** As a User, I want to access a contact page, so that I can find contact information for support

#### Acceptance Criteria

1. THE Todo Application SHALL provide a contact page accessible from the main interface
2. THE Todo Application SHALL display a telephone number on the contact page
3. THE Todo Application SHALL display an email address on the contact page
4. THE Todo Application SHALL display supporting text with instructions for contacting support
```

Save the file after you have made the change.

3. As we have made a change ourselves, we now need to ask Kiro to re-load the requirements via the chat interface.

"I have updated the requirements.md so please re-load and check"

Review the output. You should get confirmation of the change (it should identify that this is a simplified requirement) and Kiro should then provide a summary with next steps. **Don't click on the move to design phase link yet**.

4. The next step is to update the design. Depending on what new requirements you make or change, this might require changes to the design document. There are two ways you can do this. You can use the button/link in the chat interface to proceed to the updating the design.

The other way you can do this is directly from the design document itself. When you click on the "Design" link at the top of the page taking you to the design.md doc, you will notice that there is a link to the right hand side called "Refine". Move your cursor and hover (do not click yet) over the Refine link - you will notice that it says "Refresh your design based on the requirements". 

5. Click on the Refine link, and watch the output in the chat interface. You should notice that it:

- reviews any changes it identifies in the requirements and compares it against the design document
- provides feedback of changes needed to be made
- makes updates to the design.md

6. We can review changes quickly by using the diff feature in Kiro. You will have seen this as we have been working, but as we were generating files from scratch, the diff feature was not so useful. When we already have stuff in our design.md, the diff feature allows us to quickly see and review changes.

![view diff](/images/kiro-diff.png)

Take a few moments to review the diff and see how the design has been updated. To close the diff, just located the X in the main editor and you will close this view.

7. In the chat interface, you should now see that you will be prompted on whether you want to "Move to implementation plan". Click on that link. Kiro will begin working, and after 1-2 minutes, you should now see that your tasks.md file has been updated with new tasks. Kiro should also provide a summary explaining which tasks have been added.

You can use the diff icon to quickly view the changes in the tasks.md as you did in the previous steps with the design updates. Locate the last item in the chat history where it says "Accepted edits to tasks.md" and click on the diff icon. In the main editing panel, you should now see highlighted in green the new updates. After viewing it, close the page in the main editing panel to return back to the implementation plan.

8 You will be prompted whether you want to implement all tasks or just keep optional tasks for MVP, so click on the optional tasks for MVP.

Once that has finished, the output in the chat interface will provide you a detailed summary. You can now start executing these tasks. As you did in earlier labs, you can do this via the UI (by clicking on the Start Task) or via the chat interface.

"Complete any outstanding tasks"

After a short while, Kiro will begin working through these new tasks. Again, you might be prompted as Kiro needs to request permissions to run various commands. 

9. When Kiro has completed this new task, re-start the application and see if you now have a Contact Us page.


![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

In the previous lab we made some changes to add a Contact Us page. What if we decided that this update was not what we needed and we wanted to undo this change. Whilst it might be tempting to ask Kiro to undo the change, there are more effective ways you can achieve this.

At the beginning of this lab you used Kiro's source control integration features to commit changes after tasks where completed. Using source control is one approach you can take. Kiro also provides some capabilities you should be aware of that can help you, through its revert and checkpoint features. In this next lab will explore these.

#### Lab-09

1. In the previous lab we added a new feature called Contact Us, which added new code. We might want to undo some changes, perhaps only certain files. We can use the Undo Change and Revert features from within the chat interface to undo either one or a collection of code changes.

From the chat interface, review the code that was generated by Kiro in the previous lab. After code changes, you will see the following.

![Undo code change](/images/kiro-code-undo.png)

If you click on that link, it will undo that code change. Don't do that now.

You can also revert changes done throughout the entire conversation or task. Once a task has been completed, you will see the following link above the chat interface dialog window.

![Revert code](/images/kiro-code-revert.png)

Be very careful clicking on that link as there is no confirmation or undo option! Again, we will not click on this link yet - this was just to let you see that these options allow you to control code changes and allow you to undo/revert back to a previous state.


2. Using Undo and Revert is fine grain and allows you to manage updates to your project files. Kiro provides another feature called Checkpoint. Each time you send a prompt to Kiro (or start a task in the implementation plan), it creates a “checkpoint”. Checkpoints appear as markers in your chat history. You can hit Restore on a checkpoint marker to rewind both your codebase and Kiro’s context back to that point in time. Any changes made to your codebase by Kiro after that checkpoint are reverted, and any context additions (chat interactions) after that point are discarded as well. 

![Checkpoint in Kiro](/images/checkpoint.png)

In the previous lab we added a new feature called Contact Us. This actually is a collection of checkpoints:

* first checkpoint was asking to add a new requirement to our spec
* second checkpoint was updating of the design document
* third checkpoint was updating the implementation plan
* fourth checkpoint was writing the code during the plan execution

Depending on what you want to do, you might want to just revert the code or you might want to revert back to the requirements updates. All you have to do is select the specific checkpoint and Kiro will revert you back to that state (updating its context in the process). Lets see how these work, starting off with reverting just the code and then the requirements.

3. From the chat interface, scroll up and follow the conversation from where you started executing the tasks for the Contact Us page. It might be easier to search for "complete any outstanding tasks" as this is what we used to start those. 

After you have located it you will notice that there is some text above this. On the left you have "Checkpoint" and on the right, a link for "Restore" - it should look like this

Click on the Restore link. It should generate the following (or similar) text.

> Restoring this checkpoint discards all changes made after this point in this session and removes conversation history from context. Imports or references may break if related files changed elsewhere - you'll need to fix those manually.

It should display a list of changed or modified files that are in the scope of this change. You will be asked to confirm whether you want to "Restore Checkpoint". Click on the Confirm link, and after a few seconds you should see all those changes disappear.

Congratulations, you have now reverted back the code based cleanly to where it was before the Contact Us changes where made. Start the application and confirm that you no longer have the Contact Us page.


> As a side note. If you have just reverted the code changes, your implementation plan (tasks.md) and the code in your project workspace will now be out of sync (the tasks will be in the todo.md and marked as completed). You can address this either by manually editing the tasks file to uncheck any tasks (removing the "x" so that [x] becomes [ ]) and then saving this file. When you do this, you should notice that the task becomes active again within the implementation plan (tasks.md). The other approach is to use the "Update Tasks" link at the top of the implementation plan (tasks.md). This will then attempt to review and update the implementation plan for you, and after a few minutes Kiro will prompt you for what you want to do.
> 
> ![update tasks to refresh](/images/tasks-update.png)
> 
> I tend to edit the todo.md plan manually as this saves on tokens/credits

4. Now locate the chat window where you created the new requirement. Kiro will open new tabs for each conversation, so you will find this by looking for a tab called "Add a new requirement".

![revert whole requirement](/images/kiro-checkpoint-requirement.png)

Click on the Restore link, and then confirm when you see the Restore Checkpoint pop up appear above the chat interface dialog box. The current chat conversation will disappear once you have done this and you should now be back at where you started.

5. In the previous examples you used Kiro native features to help you navigate state within your project. You can also use source control. During the earlier labs you initialized git and committed code as tasks were completed.

We are not going to explore this in this workshop, but experiment and see which approach works best for you.


![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

You can create many specs for a given application. In this next lab we are going to create a completely new spec, building on from the code that Kiro has already generated for us. We are going to add a new feature to export our todo's in csv format.

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
- apply what you learned for the first spec as you work through the three phases: requirements, design, and implementation
- as you start running tasks during the implementation plan, make sure you watch out and respond to prompts when Kiro needs permissions to run commands 

6. Once Kiro has completed all the tasks, start the application and test out this new feature to make sure it works.


![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

Keeping track of changes of your spec files is something that you will need to plan for. Using source control within your project will help you track these changes at an atomic level, and you should be ensuring that you check in these assets into your version control (we have been doing that throughout this workshop so far).

In this final lab, we will look at another approach that might be useful to help you track changes at a higher level. We are going to use a feature of Kiro called "Agent Hooks" that allow you to automate development tasks. We will create a changelog file (changelog.md) within our project, and then manage changes via an agent hook that we create.

#### Lab-11

1. In the root of your project workspace, create a file called "changelog.md" and edit the file so that it looks like this:

```
# Changelog

This document captures updates to Kiro spec files and helps you track changes over time.

## Change history

```

2. From the Kiro navigation bar, open the Kiro icon and click on the **"+"** to create a new agent hook.

3. In the description field, add the following:

```
Create a new agent hook that will summarize changes to the Kiro spec files in the changelog.md file. Append entries into this file as Kiro specs are added, changed, or removed.
```

and hit return. Kiro will start the process of creating the Agent Hook. After a few seconds, the agent hook configuration screen will appear.

4. Under the "Event" pull down, make sure it says "Manual Trigger". This means that this agent hook will be invoked manually by us as we make changes.

5. Ensure that the action is "Ask Kiro". Kiro will have added something in the "Instructions for the Kiro agent" panel. I modified the text that was generated to use this.

```
Review changes to Kiro spec files:
- requirements.md
- design.md
- tasks.md. 

Analyze changes against ALL of these files. Append a summary entry to the changelog.md file. Include the following:

- date stamp of the change
- the file that has been changed (requirements.md, design.md, or tasks.md)
- a clear description (summary) of the change

You MUST include changes/updates made to each of requirements.md, design.md, and tasks.md
```

Once you have finished, your agent hook configuration should look something like this:

![agent hook for change log](/images/kiro-spec-changelog.png)

6. Close the Agent hook configuration screen from the main editor panel. Your hook will now be automatically enabled. As this is a manually trigger agent hook, we can invoke this using the "/" command, which will bring up any agent hooks you have created.

7. Before we proceed, from Kiro's navigation toolbar, select source control and commit the current changes. This will allow you to track changes more easily as we proceed.

8. From the Kiro screen, select the Export spec (it will be called something like todo-export or todo-csv-export). It should bring up the requirements.md file. From the Kiro chat interface, enter the following.

```
Add a new requirement that the export file is password protected. Passwords should be requested when the export is generated
```

9. Complete the three steps of the workflow, but do not start any of the tasks in the implementation plan - we don't need to see those for this lab.

10. Once these have been completed, invoke the agent hook by typing "/" in the Kiro chat interface. Once you enter "/" you should see the agent hook you create appear.

![manually triggered agent hook](/images/kiro-agent-hook-manual.png)

Click on the green triangle. This will add the agent hook to the chat dialog box. Hit return, and the agent hook should start doing its work.

11. Review the changes in the changelog.md file against the spec changes.

12. You can tweak the prompt within the agent hook to be as detailed or sparse as you want. With this approach, we can automate capturing information as we change add and remove specs from this project.


![Lab](/images/lab-header-end.png)

---

### Lab Completed

Congratulations, you have now completed the first set of labs and are now ready to explore the world of spec driven development. Before you go, if you are hungry for more, then take a look at some of these suggested next steps to give you

**Recommended next steps**

* To dive deeper, run through the labs again this time selecting to run all tasks during the implementation phase. This will take longer, and use more Kiro credits. You will get to see how Kiro generates and then runs property based testing.
* Add new requirements to an existing spec - Kiro will make an attempt to put a new requirement in either an existing spec or create a new one. Try adding a new feature that allows you to add comments or updates to a task to an existing spec (open the spec up and use the chat to add this as a new requirement)
* Go through and add additional specs to this project - perhaps add simple authentication using email addresses, or maybe add persistence to a database
* Dive deeper into steering documents and how these influence the output Kiro generates

Click on [Existing Codebases](/workshop/04-brownfield.md) to proceed to the next section where we show how you can use SDD with existing code you have

---

### Feedback

If you found this workshop useful (or not) please let me know - this will help me justify creating more workshops like this. Please complete [this short survey](https://pulse.aws/promotion/VWOXGKXF) - thank you!

Click on [Home](/README.md) to go back to the landing page

---

# Additional reading material

* [Official Kiro docs](https://kiro.dev/docs/?trk=71546b8e-c969-4ead-aa9f-9cd06f6d8610&sc_channel=el
)

* [Your first project on Kiro](https://kiro.dev/docs/getting-started/first-project/?trk=71546b8e-c969-4ead-aa9f-9cd06f6d8610&sc_channel=el
)

* [Spec best practices](https://kiro.dev/docs/specs/best-practices/?trk=71546b8e-c969-4ead-aa9f-9cd06f6d8610&sc_channel=el
)

