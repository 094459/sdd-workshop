![Header - picture of Kiro ghost and title](/images/header.png)

# Using spec driven development on existing codebases

In this lab we are going to apply everything we have learned in the previous sections, and use spec driven development to work on an existing application. We will be using [a sample book sharing application](https://github.com/beechgeek/sdd-workshop-book-sharing-app) as our starting point.

The goal of this lab is to:

* show how to apply the spec driven development approach with existing codebases
* understand how you can use features of Kiro to generate good steering files
* work through the spec workflow to add a new feature to an existing application

At the end of this lab, you will be able to apply this to your own projects and code.

---


![Lab](/images/lab-header.png)

In this first lab we are going to create a new project workspace, check out the code from source control and then start generating steering files that will anchor Kiro's output.

#### Lab-01

1. Create a new project workspace on your machine - I am going to call mine "~/kiro/workshop-brownfield"

```
mkdir ~/kiro/workshop-brownfield && cd workshop-brownfield
```

2. Check out the demo application into this directory and change directory to make it your project directory

```
git clone https://github.com/beechgeek/sdd-workshop-book-sharing-app
cd sdd-workshop-book-sharing-app
```

3. Launch Kiro from the command line

```
kiro .
```

4. We will now generate steering files from the code in this project. From the Kiro screen, locate the Agent Steering panel and click on the button "Generate Steering Docs".

Review the output in the chat interface. It should generate a number of artifacts: product, structure, and tech. These should be visible now in the Agent Steering panel, under the Workspace heading.

5. Click on each of the artifacts created in turn, and review them.

6. From the Agent Steering panel, click on the + to create a new steering document. Call this "Python-Preferences" and in the main editor, copy the following text into this new steering document.

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

Save and exit when you have copied this into the document. You should now see that this new steering document appears with the others.

You might be wondering why do we need to do this? The steering documents created by Kiro reflect what it can reason about the project in the workspace. It can then use these when working. It does not however know about your preferences or how you might want to steer the direction of output from Kiro during its work. This is why you should think about what additional steering files you will need.

7. As we have added these steering files, we now need to update Kiro's file index. From Kiro's IDE, bring up the command palette (on a Mac this is SHIFT + COMMAND + P, and Windows it is CTRL + SHIFT + P) and from the dialog box type "Kiro" and then select "Kiro: Docs force re-index" option.

We now have everything setup and ready to use the spec driven development workflow.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

The project we are working on has no documentation, and we want to know how to get it started. In this next lab we are going to get Kiro to build documentation that will help us understand how the application works and how to get it up and running in local development mode as well as for production.

## Lab-02

1. From the Kiro screen, click on the "+" next to Spec to create a new spec. In the dialog that comes up, enter the following:

"Create documentation that provides information on how this application works (include sequence diagrams) and shows me how to start the application in local dev and production modes"

2. Review the output from the chat interface. You should notice a few things:

- Kiro does **NOT** create a spec, but rather just created the documentation
- the steering documents we created as used as context
- Kiro reads the key files in the project workspace and starts generating documentation

As we saw in the Greenfield lab, Kiro is smart enough to know whether a spec request is better delivered outside of the spec workflow.

3. Review the documentation, and use this to start the application on your local machine. 


You should see that the documentation provides an option for "uv" which matches our steering document. You should see something like the following.

```
uv pip install -r requirements.txt
uv run python run.py
```

Run the above commands to start the app and then:

- open up a browser on http://127.0.0.1:5000 to make sure that the application is working correctly
- register a user using your email address, using the invite code of INITIAL
- making sure you can login using the credential you created
- add a new book (in the next lab we are going to need this)

Once you have confirmed the application is working, exit (CTRL + C).

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

Now that we have confirmed the application is working, we are going to use Kiro to help us add a new feature. What we are going to do is add a new feature that allows logged in users to be able to export a list of all books in csv format.

## Lab-03

1. From the Kiro screen, click on the "+" next to Spec to create a new spec. In the dialog that comes up, enter the following:

"Add a new feature so that a user can export all their books in csv format. The export feature should appear in their profile page"

Review the chat interface, and this time you will see that Kiro decided that for this request a spec is required. You should see:

- a new spec appear in the Spec panel (called something like book-export-csv or similar)
- Kiro provides our steering documents as context
- starts the spec driven workflow, and creates the requirements.md 

2. Review the requirements.md file and make sure that the key elements of the requirements are there. Reviewing the requirements, make sure that they include the key details:

- export is available from the profile page
- exports book information in csv format
- provides some sort of validation and error checking functionality during the export process

Also make sure that the requirements are not over engineered.

3. In this particular feature, it is likely you can accept the requirements.md as is. So click on the "Move to design phase" button in the chat interface to kick start the design step of the workflow.

Once the design.md document has been completed, take a few minutes to review it. Is there anything missing?

In the chat interface, you should see that you are prompted whether you want to proceed to the implementation phase - so click on that to start the creation of the tasks.md

4. After a few minutes, the tasks.md will get generated, outlining the tasks needed to implement the export feature. It should not be a large list of tasks as we are only implementing a small feature.

You should also notice that in the chat interface you are being asked whether you want to keep optional tasks (faster MVP) or make all tasks required. Click on the "faster MVP" option.

5. Now start working through the tasks in sequence - you can either click on the "Start Task" link above each task, or use the chat interface. Kiro will prompt you as it needs permission to do certain tasks, so pay attention to the chat interface.

After all the tasks have been completed, we are now ready to start the application and test this new feature.

6. Start the application, login, and now click on your profile and test to make sure that the export button appears, and that it works as expected.

Congratulations, we have now used spec driven development to add a new feature to this application.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

We have added a new feature, but we forgot to add a requirement to make sure the documentation was updated. In this lab we will update the requirements to rectify this, and see this new requirement flow through the spec driven workflow.

## Lab-04

1. From the chat interface, enter the following:

"Update the requirements.md to make sure that the documentation in the project workspace is updated to cover this new feature"

Review the output in the chat interface, and open up the requirements.md - you should see a new requirement be added. Review to make sure that this new requirement correctly updates the documentation in the project vs adding documentation for the end user. Sometimes using prompts to add new requirements is sub optimal, especially when you want to have control and precision. Your new requirement should look something like this:

```
### Requirement 5

**User Story:** As a developer or user, I want the project workspace documentation to be updated with the CSV export feature, so that the feature is properly documented for future reference and user guidance

#### Acceptance Criteria

1. THE BookShare System SHALL update the project README file to include a description of the CSV export feature in the features section
2. THE BookShare System SHALL document the CSV export endpoint and its functionality in the project documentation
3. THE BookShare System SHALL document the list of fields included in the CSV export with descriptions of each field in the project documentation
4. THE BookShare System SHALL include instructions on how users can access and use the export feature from their profile page
5. THE BookShare System SHALL document any technical implementation details relevant for developers maintaining the export feature
```

If you do edit the requirements directly, make sure you nudge Kiro you have done this by entering something like this in the chat interface:

"I have updated the requirements.md"

Which will ensure Kiro reloads the requirements.md.

2. From the top of the main editor panel, click on the design button and then use the "Refine" button to kick start Kiro to move the spec workflow to the next phase - reviewing what changes are needed to the design based on changes to the requirements. Review the chat interface output to see what Kiro is doing.

3. Once you have reviewed changes to the design, click on the Move to implementation phase to start the generation of tasks.

Again, Kiro will update the chat interface with key information of what it is doing. Once finished, you will again be asked if you want to implement all tasks or faster MVP - select faster MVP.

4. Open up the tasks.md and you should now see you have new tasks. Work through each task in sequence until they have all be completed. During this:

- ensure you pay attention to Kiro asking you for permission
- review the output for what Kiro is generating
- look at the file explorer to review the output of these tasks in creating/updating documentation

When finished, you can use the diff feature to see how the documentation has changed based on the updated requirement.

5. Congratulations, you have now completed this lab. Make sure you stop the application (CTRL + C) if it is running.

![Lab](/images/lab-header-end.png)

---

Click on [Tools and Resources](/workshop/05-tools-and-resources.md) to wrap up and get additional resources to help you carry on your learning on SDD

Click on [Home](/README.md) to go back to the landing page


---

# Additional reading material

* [Official Kiro docs](https://kiro.dev/docs/)