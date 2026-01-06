![Header - picture of Kiro ghost and title](/images/header.png)

# Using spec driven development on existing codebases

In this lab we are going to apply everything we have learned in the previous labs and use spec driven development to work on an existing application. We will be using [a sample book sharing application](https://github.com/beechgeek/sdd-workshop-book-sharing-app) as our starting point.

The goal of this lab is to:

* show how to apply the spec driven development approach with existing codebases
* understand how you can use features of Kiro to generate good steering files
* work through the spec workflow to add a new feature to an existing application

At the end of this lab, you will be able to apply this to your own projects and code.

It is recommended you start with the [greenfield labs](/workshop/03-greenfield.md) first, but it will work if you have not done that.

---


![Lab](/images/lab-header.png)

In this first lab we are going to create a new project workspace, check out the code from source control and then start generating steering files that will anchor Kiro's output. Steering files provide critical context for AI coding assistants like Kiro, helping them to understand your project and then generate more relevant output.

#### Lab-01

1. If you are doing this tutorial after having completed the [greenfield workshop](/workshop/03-greenfield.md) then you will need to remove the global steering file before we continue. Open up a terminal, and run the following commands:

```
cd ~/.kiro/steering
mv mv Project-Standards.md Project-Standards.disabled
```

Close this terminal.

2. Create a new project workspace on your machine - I am going to call mine "~/kiro/sdd-brownfield"

```
mkdir ~/kiro/sdd-brownfield && cd sdd-brownfield
```

and then check out the demo application into this directory and change directory to make it your project directory

```
git clone https://github.com/beechgeek/sdd-workshop-book-sharing-app
cd sdd-workshop-book-sharing-app
```

3. Launch Kiro from the command line

```
kiro .
```

4. We will now generate steering files from the code in this project. Select the Kiro icon from the navigation bar, and locate the Agent Steering panel. It should be empty, and you should see a button called "Generate Steering Docs".

Click on the button "Generate Steering Docs".

Review the output in the chat interface. It should generate a number of artifacts: product, structure, and tech. These should be visible now in the Agent Steering panel, under the Workspace heading.

5. Click on each of the artifacts created in turn, and review them. We looked at this in the [getting started section](/workshop/02-getting-started.md):

* Product Overview (product.md) - Defines your product's purpose, target users, key features, and business objectives. This helps Kiro understand the "why" behind technical decisions and suggest solutions aligned with your product goals.
* Technology Stack (tech.md) - Documents your chosen frameworks, libraries, development tools, and technical constraints. When Kiro suggests implementations, it will prefer your established stack over alternatives.
* Project Structure (structure.md) - Outlines file organization, naming conventions, import patterns, and architectural decisions. This ensures generated code fits seamlessly into your existing codebase.

It is important that you review these three artifacts after they have been generated. Check that they are accurate and reflect the project you are working on. If there are key pieces of information missing, you can edit the files and make revisions. This is important because these documents will be used throughout the workflow steps.

What we are in essence doing is providing Kiro with a strong foundation on which to understand the codebase which will help as we then start to create specs to add new features.

6. The steering files that were generated are project specific steering files. You might want to add additional steering files, for example defining your personal or organizational developer standards. Using the same approach that was used in the [greenfield tutorial](/workshop/03-greenfield.md), we will create a new steering file to configure our Python preferences.

From the Agent Steering panel, click on the + to create a new steering document. From the options, select project workspace steering.

Name this steering file "Python-Standards", and after pressing enter copy the following text into this new steering document in the main editor.

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
- Configure [tool.hatch.build.targets.wheel] packages with the correct value for the project%

```

Save and exit when you have copied this into the document. You should now see that this new steering document appears with the others.

> **Tip!** Before proceeding when you use this approach for real work, you will need to check any additional steering documents you add against the steering documents that have been generated. If there are differences, contradictions, or incompatibilities with what is between these steering documents, Kiro will likely get confused and the output you get will be difficult to predict.

7. As we have added these steering files, we now need to update Kiro's file index. From Kiro's IDE, bring up the command palette (on a Mac this is SHIFT + COMMAND + P, and Windows it is CTRL + SHIFT + P) and from the dialog box type "Kiro" and then select "Kiro: Docs force re-index" option.

We now have everything setup and ready to use the spec driven development workflow.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

Project documentation provides a great source of context for agentic tools like Kiro. The project we are working on currently has no documentation, which is typical of many applications you might encounter in a brownfield situation. In this next lab we are going to get Kiro to generate documentation that will help us understand how the application works and how to get it up and running.

## Lab-02

1. From the Kiro screen, click on the "+" next to Spec to create a new spec. In the dialog that comes up, enter the following:

"Create documentation that provides information on how this application works (include sequence diagrams) and shows me how to start the application"

2. Review the output from the chat interface. You should notice a few things:

- Kiro does **NOT** create a spec, but rather just creates documentation
- Steering documents are added as context
- Kiro reads the key files in the project workspace and starts generating documentation

As we saw in the Greenfield lab, Kiro is smart enough to know whether a spec request is better delivered outside of the spec workflow.

> **TIP!** For complex codebases and projects, you might want to ask Kiro to generate a spec that creates code to perform analysis and document the project. Kiro will generate and run tools that provide a more structured way of getting that documentation. For small projects like this, this is not required.

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

One of the techniques you will start to learn and get intuition for is how to trim over engineered requirements. Get in the habit of reviewing your requirements.

3. In this particular feature it is likely you can accept the requirements.md as is. So click on the "Move to design phase" button in the chat interface to kick start the design step of the workflow.

Once the design.md document has been completed, take a few minutes to review it.

In the chat interface, you should see that you are prompted whether you want to proceed to the implementation phase - so click on that to start the creation of the tasks.md

4. After a few minutes, the tasks.md will get generated, outlining the tasks needed to implement the export feature. It should not be a large list of tasks as we are only implementing a small feature.

You should also notice that in the chat interface you are being asked whether you want to keep optional tasks (faster MVP) or make all tasks required. Click on the "Faster MVP" option.

5. Now start working through the tasks in sequence - you can either click on the "Start Task" link above each task, or use the chat interface. Kiro will prompt you as it needs permission to do certain tasks, so pay attention to the chat interface.

After all the tasks have been completed (it will take around 10 minutes to work through every task), you can now start the application and test this new feature.

6. Start the application, login, and now click on your profile and test to make sure that the export button appears, and that it works as expected.

Congratulations, we have now used spec driven development to add a new feature to this application.

7. You have now completed this lab. Make sure you stop the application (CTRL + C) if it is running.

![Lab](/images/lab-header-end.png)

---

Click on [Tools and Resources](/workshop/05-tools-and-resources.md) to wrap up and get additional resources to help you carry on your learning on SDD

Click on [Home](/README.md) to go back to the landing page

---

# Additional reading material

* [Official Kiro docs](https://kiro.dev/docs/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el)