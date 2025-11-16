![Header - picture of Kiro ghost and title](/images/header.png)

# Getting started with Spec Driven Development (SDD)

Spec driven development (SDD) is a systematic approach to software feature development that emphasizes thorough planning, clear documentation, and structured implementation. This methodology transforms rough feature ideas into well-defined, implementable solutions through a three-phase process that ensures quality, maintainability, and successful delivery.

![Three steps of SDD](/images/lifecycle-high-level.png)

## Kiro

We are going to be using Kiro throughout this workshop. Kiro provides an opinionated UI that walks you through the specs driven development workflow. 

![Kiro overview](/images/kiro-overview.png)

Kiro simplifies working with spec driven development by integrating into its user interface how to create a spec, and then walking you through the workflow: Creating detailed requirements, selecting the right technical design, and then building the implementation plan by breaking down what is needed into a series of tasks.


## What is a "spec"?

Specs bridge the gap between conceptual product requirements and technical implementation details, ensuring alignment and reducing development iterations. But what exactly is the "spec" in spec driven development? A spec is a collection of resources that are used to implement a feature. 

A spec has a number of characteristics:

* they are structured, written documents (in markdown)
* the structure is optimized for specific activities (requirements, design, or tasks)
* they are organized together as a collection

A spec has a lifecycle: you create a spec (and work through the three phases of an iteration), and you can update a spec (iterating through the same three phases, or just the relevant ones to the change being made). This will make more sense later on when we start working through our first spec, so don't worry too much right now.

---

## Creating a Spec

Creating a spec starts with intent - what are trying to do? 

We use an initial prompt to bootstrap the spec creation and start the workflow. You will see this in action later when you do the hands on labs. Working with specs about iterating and refining. It is not too important whether your spec is perfect when it is initially created as you will be spending lots of time reviewing and editing them.

Specs are a collection of markdown docs, which we will dive into during the hands on labs.

### How many specs

Each spec is a feature you want to work on - your intent. You can create multiple specs for any given project you are working on. 

![multiple specs](/images/multiple-specs.png)

Throughout this workshop we will use the term spec in the singular. When you start to use spec driven development to build features for your applications, you might work with many specs. Each spec delivers a specific feature.

Before we dive into the workflow in more detail, we need to talk about Steering documents - what they are and why they are important.

---

## Steering documents

Providing the right context is key to getting the best out of AI coding assistants, and steering documents help provide context. steering documents provide persistent knowledge about your project through markdown files. Instead of explaining your conventions in every chat, steering files ensure your AI coding assistant consistently follows your established patterns, libraries, and standards.

**Steering documents and intent have a close relationship**. The steering documents that you create will be aligned to the intent you have.

**Generating or adding steering files**

The "Agent Steering" panel from the Kiro activity bar is where any steering documents are listed. From here you can generate or create new steering docs. Steering documents are scoped at either a global (Global agent steering - they will appear in every project you use Kiro with) or project level (Workspace agent steering - the steering documents will appear in just this project). When creating steering files, you will be asked to specify what the scope of the steering file is. 

![steering file options in Kiro](/images/kiro-steering.png)

These steering documents are stored in a specific location in your computer:

* ".kiro/steering" for workspace agent steering files
* "~/.kiro/steering" for global steering files. 

How you create your steering documents will depend on whether you are working on an existing codebase (brownfield) or creating a new project (greenfield). In the next sections we will look at this.

---

### Steering documents with existing applications

When using Kiro with an existing codebase, you can use the "Generate Steering" button in the Steering Docs widget to automatically generate steering files for your project. Kiro will review your project workspace, and then generate its foundational steering files to establish core project context. It will create three files: product.md, tech.md, and structure.md

* Product Overview (product.md) - Defines your product's purpose, target users, key features, and business objectives. This helps Kiro understand the "why" behind technical decisions and suggest solutions aligned with your product goals.
* Technology Stack (tech.md) - Documents your chosen frameworks, libraries, development tools, and technical constraints. When Kiro suggests implementations, it will prefer your established stack over alternatives.
* Project Structure (structure.md) - Outlines file organization, naming conventions, import patterns, and architectural decisions. This ensures generated code fits seamlessly into your existing codebase.

It is important that you review these three artifacts after they have been generated. Check that they are accurate and reflect the project you are working on. If there are key pieces of information missing, you can edit the files and make revisions. This is important because these documents will be used throughout the workflow steps.

> **Note!** An important step to be aware of. If you do make edits and changes, make sure you ask Kiro to reload these files into its context window. If you fail to do this, it will retain the original versions in its "memory". The prompt I use is as follows (changing it based on which steering doc was updated):
> 
> "I have updated the steering document xx.md - please reload"
>


---

### Steering documents for new Applications

With a blank project, you use steering docs in a different way - to influence and guide the direction of Kiro when working through its workflow. To create then, in Kiro you use the Agent Steering widget, and click on the "+" icon, which will open up a dialog allowing you to enter the name of the steering file you want to create. Kiro will automatically create the markdown file in the correct directory, and open it up so that you can edit it.

Here are a few examples of steering files you can add, and provide an idea of how you can use them for your own projects.

* **API Standards (api-standards.md)** - Define REST conventions, error response formats, authentication flows, and versioning strategies. Include endpoint naming patterns, HTTP status code usage, and request/response examples.

* **Testing Approach (testing-standards.md)** - Establish unit test patterns, integration test strategies, mocking approaches, and coverage expectations. Document preferred testing libraries, assertion styles, and test file organization.

* **Code Style (code-conventions.md)** - Specify naming patterns, file organization, import ordering, and architectural decisions. Include examples of preferred code structures, component patterns, and anti-patterns to avoid.

* **Security Guidelines (security-policies.md)** - Document authentication requirements, data validation rules, input sanitization standards, and vulnerability prevention measures. Include secure coding practices specific to your application.

* **Deployment Process (deployment-workflow.md)** - Outline build procedures, environment configurations, deployment steps, and rollback strategies. Include CI/CD pipeline details and environment-specific requirements.


Now, you might be wondering what happens if you click on the "Generate Steering" docs button in the Kiro IDE when you have a blank project. Kiro will still run, but it will generate three steering files (product.md, tech.md, and structure.md) but these will have generic, placeholder text which you can then use as a starting point.

---

### Steering document "Inclusion Modes"

Providing context is critical in getting good output from AI coding assistants, so the temptation to put everything is very real. However, you should resist this. Edit your context files ruthlessly so that they are as small as you can make them.

Kiro provides a way to help you by looking for rules of what to include or exclude from context using something called "Inclusion Modes". Inclusion Modes is a header at the top of a markdown file that you have defined as a steering doc, that provides rules as to when it should be used. They look like this

```
---
inclusion: fileMatch
fileMatchPattern: "components/**/*.tsx"
---
```

* **Always Included** - the default mode (and where no Inclusion Mode header is provided). These files are loaded into every Kiro interaction automatically. Use this mode for core standards that should influence all code generation and suggestions. Examples include your technology stack, coding conventions, and fundamental architectural principles.
* **Conditional** - Files are automatically included only when working with files that match the specified pattern. This keeps context relevant and reduces noise by loading specialized guidance only when needed.
* **Manual** - Files are available on-demand by referencing them with #steering-file-name in your chat messages. This gives you precise control over when specialized context is needed without cluttering every interaction.

---

### Deleting steering files

You can easily delete any steering files, either directly by deleting them from the filesystem, or through the Agent Steering widget (right click, delete).

---

### Steering file strategies

It is tempting when thinking about what you want to include in your steering files to put everything in. Don't! Here are some strategies to help you add the right steering docs to your project.

* Always use Generate when working with existing projects and then review/edit the output for accuracy. If things are missing, add them.
* Start small and include just the core needs you want to influence
* Use the different inclusion modes to help the AI coding assistant optimize which steering files to use and optimize your context window utilization
* Use clear and descriptive names when naming your steering files (e.g. api-rest-conventions.md - REST API standards)
* Provide examples - use code snippets, example input/outputs, style and structure guides
* Security first - make sure you do NOT include sensitive information in your steering docs. **Never include** API keys, passwords, or sensitive data
* Review and maintain your steering files as you iterate and improve them.

---

### Model Context Protocol (MCP)

In addition to steering docs, Model Context Protocol (MCP) provides AI coding assistant with up to date or specialized context that will help it generate more specific outputs. This is done via configuring MCP Servers within your AI Coding assistant, which will then provide additional tools which the AI coding assistant can use to get that additional context. There are many hundreds (if not thousands) of MCP servers available to developers to help them with generalized or very specific tasks.

> **How does this work?** You AI coding assistant will make a judgement call based on the prompt which MCP servers it might want to use. You can force this by being specific in your prompt.

You have a couple of strategies open to you as you think about how you want to incorporate the context from MCP Servers.

* Configure MCP Servers within your AI coding assistant tool
* Generate markdown steering docs from the output of running prompts against an MCP Server

The key difference between the two approaches is around how you manage what context is provided. MCP Servers can fill up the AI coding assistant context window, and its hard to see what is being included (you are kind of at the mercy of the MCP Server). Piping the output to a markdown file and then adding this as steering can be an optimization technique. It will also allow you to review and edit what you provide - for many queries, you might actually only need a small portion of what the MCP Server might bring back. The other side however is that if the AI coding assistant needs information (context) that you did not include, you might get unexpected results. Depending on what you are doing, having the latest, up to date information might be important. These are things you need to think about.

---

## Spec Workflow

Now that we have looked at providing the right context via steering files and MCP servers, we are ready to get back to the spec creation workflow. The workflow follows a logical progression between three phases with decision points, ensuring each step is properly completed before moving to the next.

The workflow is initiated when we create a new spec via a prompt in the chat interface. Kiro will transform that prompt and create the initial spec, creating a detailed set of requirements. It is important to note that at this stage, Kiro creates a new directory which is used as a container for all the artifacts produced (.kiro/{specname}). You can take a look at these as Kiro is working.

After reviewing and iterating on the requirements, the next stage in the workflow is defining the technical design. This is where those steering files and MCP servers help direct the output of the LLM. 

After the design has been reviewed and accepted (by you), you move onto the final step of the workflow, generating the implementation plan. This step generates a set of tasks that will implement the requirements against the technical design. These tasks will then be used to start the process of generating code.

![Three phases of SDD](/images/spec-three-phases.png)

Each phase builds upon the previous one, with explicit approval gates to ensure quality and alignment before proceeding.

Kiro also provides visual cues within the chat interface to help you move from one stage to the next. So when Kiro has completed the generation of requirements.md for example, you will see a cue to "proceed to the design stage" within the chat interface.

Lets dive into each of these workflow steps in more detail.

---

## Requirements

### Initial requirements generation

The first artefact created by Kiro is a requirements file, "requirements.md". The top of the requirements.md file will look like the following:

```
# Requirements Document

## Introduction

This feature will {text that describes in more details what you requested when creating the spec}

```

The text will vary based on what you asked from the initial spec request. It is important that you review this carefully and edit as needed. 

Following the top section, the rest of the requirements.md file is written in the form of user stories with acceptance criteria in **EARS** notation. **EARS** (Easy Approach to Requirements Syntax) notation provides a structured format for writing clear, testable requirements. In a spec's requirements\.md file, each requirement follows this pattern:

```
WHEN [condition/event]
THE SYSTEM SHALL [expected behavior]
```
This structured approach offers several benefits:

* Clarity: Requirements are unambiguous and easy to understand
* Testability: Each requirement can be directly translated into test cases
* Traceability: Individual requirements can be tracked through implementation
* Completeness: The format encourages thinking through all conditions and behaviors

Requirements helps you transform vague feature requests into these well-structured requirements, making the development process more efficient and reducing misunderstandings between product and engineering teams.

In addition the requirements.md will use other common terms to help provide clarity and consistentency:

* **role**: Describes the user persona you are referring to (you may have many)
* **feature**: Describes the feature you are wanting to implement
* **event**: Describes a specific event within the system
* **system**: Indicates the application or system 
* **response**: Describes the specific response

**Examples**

* Simple Event-Response - WHEN [user clicks submit button] THEN [system] SHALL [validate form data]
* Conditional Behavior - IF [user is authenticated] THEN [system] SHALL [display user dashboard]
* Complex Conditions - WHEN [user submits form] AND [all required fields are completed] THEN [system] SHALL [process the submission]
* Error Handling - WHEN [user submits invalid data] THEN [system] SHALL [display specific error messages]

* State-Based Requirements - WHEN [system is in maintenance mode] THEN [system] SHALL [display maintenance message to all users]

* Performance Requirements - WHEN [user requests data] THEN [system] SHALL [respond within 2 seconds]

* Security Requirements - IF [user session expires] THEN [system] SHALL [redirect to login page]

---

### Refining and improving your requirements

The first version of the requirements.md file is rarely 100%, and so you will need to iterate on this. Consider the following as you do this:

* **Over-engineered requirements** - Check for over engineered requirements and edit ruthlessly based on what you actually need
* **Review with Stakeholders** - Get feedback on completeness and accuracy from users and other stakeholders
* **Identify Gaps** - Look for missing scenarios or unclear requirements
* **Clarify Ambiguities** - Resolve any vague or conflicting requirements
* **Add Missing Details** - Include edge cases and error handling

**Common Pitfalls**

There are some common pitfalls that you might fall into when you first start off, so check this list and adjust your requirements as needed.

* **Vague Requirements** - Problem: "System should be fast" Solution: "WHEN user requests data THEN system SHALL respond within 2 seconds"
* **Implementation Details in Requirements** - Problem: "System shall use Redis for caching" Solution: "WHEN user requests frequently accessed data THEN system SHALL return cached results"
* **Missing Error Cases** - Problem: Only defining happy path scenarios Solution: Always include WHEN/IF statements for error conditions
* **Conflicting Requirements** - Problem: Requirements that contradict each other Solution: Review all requirements together and resolve conflicts explicitly
* **Untestable Requirements** - Problem: "System should be user-friendly" Solution: "WHEN new user completes onboarding THEN system SHALL require no more than 3 clicks to reach main features"

---

### Example requirements

Here are some simple examples to show how these come together

**File Upload Feature**

```
User Story: As a user, I want to upload files, so that I can share documents with my team.

Acceptance Criteria:

WHEN user selects file under 10MB THEN system SHALL accept file for upload
WHEN user selects file over 10MB THEN system SHALL display "file too large" error
WHEN user selects unsupported file type THEN system SHALL display "unsupported format" error
WHEN upload is in progress THEN system SHALL display progress indicator
WHEN upload completes successfully THEN system SHALL display success message
WHEN upload fails THEN system SHALL display retry option
IF user is not authenticated THEN system SHALL redirect to login before upload
```

**User Authentication Feature**

```
User Story: As a new user, I want to create an account, so that I can access personalized features.

Acceptance Criteria:

WHEN user provides valid email and password THEN system SHALL create new account
WHEN user provides existing email THEN system SHALL display "email already registered" error
WHEN user provides invalid email format THEN system SHALL display "invalid email format" error
WHEN user provides password shorter than 8 characters THEN system SHALL display "password too short" error
WHEN account creation succeeds THEN system SHALL send confirmation email
WHEN account creation succeeds THEN system SHALL redirect to welcome page
```
---

### Updating the requirements.md file

You can update the requirements.md file in two ways. You can use the Kiro editor to make changes, or you can ask Kiro to make those changes via the chat interface.

In practice (and as you being to work with specs on a more frequent basis) you are likely to use both. As good as Kiro is at taking your prompts and making changes, sometimes it is just quicker to edit requirements.md by hand, or perhaps you need to provide a level of detail that only hand editing will provide. 

It is worth re-iterating that when you make any changes to the specification documents through edits in the editor, you will need to remind Kiro to reload them. We need to do this because when Kiro generated the initial requirements.md, it is still in its short term memory (context window). A prompt such as:

```
Please reload the requirements.md as I have made changes
```

Kiro will provide you a positive confirmation of the changes made, so make sure you look out for that and confirm that it is what you have done.

With the requirements completed, we are now ready to move to the next step in the workflow: Design.

---

## Design

Kiro makes this easy for us as it provides visual cues within the IDE. We can start this process by clicking on the "Move to Design phase" button which will appear in the chat interface. You can also start the design process from the chat interface by using a prompt:

"Move to the design phase"

Once you start the design phase, Kiro will start initiating the generation of the design.md document. The process should take around 2-3 minutes, and once finished you should see the new file appear in the project workspace.

The design.md provides a number of sections:

* **Architecture**
* **Components and Interfaces**
* **Data Models**
* **Error Handling**
* **Test Strategy**
* **Security Considerations**
* **Performance Optimizations**

Each section drills down into more detail. There is a lot of detail that will need to spend time reviewing (and editing). We will do that in the next section. 

---

### Reviewing the design.md

It is important to spend time reviewing and editing the design.md file. When reviewing the design.md make sure that you:

* **Include examples** - throughout the document you should see relevant examples that will help steer the AI coding agent when generating code
* **Edit ruthlessly** - as these are generated by an LLM, design documents can be longer and more verbose than they need to. They often over-engineer, so look out for this and edit as needed based on your use case
* **Missing items** - check and find out what is missing - missing components or missing details are frequent things that you will catch during the review
* **Alignment** - review to make sure design choices make sense (context)
* **Clarity** - ensure that technology choices are clear - do these line up with what you expect? do they match your steering documents? 

You should also consider the use case you have - if you are doing a simple PoC, then maybe you can edit the design down and remove some of the sections. This will simplify the next step in the workflow, which uses a combination of the requirements and design to break down the development task into more discrete tasks.

Over time you can expect to have standard section you can copy and paste into these design documents. You can simplify this by adding these to your steering docs, although you will still need to review as the non deterministic nature means these will now always flow through (in my experience).

The output of this stage is that you have an updated design.md document. Again, as you will typically update your design you need to prompt Kiro by using a prompt like:

"I have updated the design.md please review and reload"

It should provide you a summary of the key changes you have made. We are now ready to proceed to the final step in the workflow, Tasks. 

To start this either click on the "Proceed to implementation" button, or from the chat interface type:

"Proceed to Implementation phase"

---

## Tasks

You will see Kiro begin the the final step in the workflow, and after 2-3 minutes you will have a new doc, tasks.md.

So what just happened? Kiro has done the following:  

* **Review Design Components** - it identifies all system components that need to be built
* **Identify Dependencies** - reviews and looks at what needs to be built before other components
* **Consider Testing Requirements** - create a plan for test creation alongside implementation
* **Sequence Tasks** - reviews the order of tasks to validate core functionality quickly

When the tasks.md document has been completed, you will be prompted for the following question:

> The current task list marks some tasks (e.g. unit tests, documentation) as optional to focus on core features first.

And you have two options: enable the use of optional tasks, or make all tasks required. What is the key difference? One (enable the use of optional tasks) allows you to define tasks as optional, thereby Kiro skipping them. We will see how that works in a minute. The second (make all tasks required) will do exactly that and configure every task as required.

After responding, the tasks.md file will get generated and you can review.

---

### Review and optimize your tasks.md

When you look at your tasks.md file, you will notice that Kiro has structured it in a particular way.

* **Two-Level Maximum** - Uses only top-level tasks and sub-tasks (to avoid deep nesting)
* **Logical Grouping** - Group related tasks under meaningful categories
* **Sequential Dependencies** - Order tasks so each builds on previous work
* **Testable Increments** - Each task should result in testable functionality

If you selected the use of optional tasks, you will also see:

* **Skip non critical tasks** Provides the ability to mark tasks as optional, by marking the task number with a "*"

![a look at tasks](/images/nested-tasks.png)

**In most cases** Kiro does a good job at identifying the tasks and the order in which they should be executed. In the next section, you will dive deeper into this topic - this is useful knowledge to have and be aware of, although you might not need to use it when using Kiro.

---

#### Reviewing Tasks

When reviewing your tasks.md file, there are two dimensions you need to think about: the tasks themselves, and the order in which tasks are ordered within the tasks.md

This is the mental model I follow, from the point of view of an agent having the info it needs to generate code:

* **Clear Objective** - What specific code needs to be written or modified as part of this task
* **Implementation Details** - Specific files, components, or functions to create, and how these match requirements/design
* **Requirements Traceability** - All tasks should reference specific requirements being implemented
* **Testing Expectations** - Depending on what you have asked, make sure that the appropriate level of tests that should be written or updated are included

---

#### Review Task Sequence

Task sequence refers to how the tasks are grouped together to form a cohesive execution plan. Kiro will structure tasks in a logical sequence, and normally these are good enough to use. However it is worth diving deeper into this so that you can understand and potentially change how these tasks are completed.

There are a number of different strategies you can take when structuring your tasks. These include:

* **Core First** - Build essential functionality before optional features
* **Risk First** - Tackle uncertain or complex tasks early
* **Value First** - Implement high value features that can be tested quickly

**Core First**

The sequence of tasks will typically look like:

1. Project setup and core interfaces
2. Data models and validation
3. Data access layer
4. Business logic services
5. API endpoints
6. Integration and wiring

* Advantages - Establishes solid foundation before building features, reduces rework from architectural changes, clear dependency chain
* Disadvantages - Longer time before visible functionality, risk of over-engineering foundation

**Risk First**

The sequence of tasks will typically look like:

1. Most uncertain/complex components
2. External integrations and dependencies
3. Core business logic
4. User interface and experience
5. Polish and optimization

* Advantages -  Early validation of technical feasibility, reduces project risk, informs architectural decisions
* Disadvantages -may not deliver user value early, requires strong technical expertise

**Value First**

The sequence of tasks will typically look like:

1. Core user registration (end-to-end)
2. User authentication (end-to-end)
3. User profile management (end-to-end)
4. Advanced features and optimizations

* Advantages - Early user value delivery, faster feedback cycles, and reduced integration risk
* Disadvantages - May require refactoring as features expand, and potential for technical debt

**Hybrid**

There is another approach, which may be suitable for many as a starting point. The Hybrid approach balances out features from the previous.

The sequence of tasks will typically look like:

1. Minimal foundation (core interfaces, basic setup)
2. High-risk/high-value feature slice
3. Expand foundation as needed
4. Additional feature slices
5. Integration and polish

* Advantages - Balances risk management with early value, flexible and adaptable, and  pragmatic approach

Throughout the rest of this workshop we are going to stick with the default sequence that Kiro generates. You should however consider these alternative sequence approaches based on the use case you are working on as they may give you a better outcome.

---

#### Managing Task dependencies

One thing you need to think about as you review and potentially update the tasks is how your tasks related to each other, specifically which tasks depend on others and whether some tasks need to be completed before others can be started.

You can group Task dependency in three categories:

* **Technical** - Code components that must exist before others can be built. For example, Database models before services that use them, Authentication middleware before protected endpoints, or Configuration setup before feature implementation
* **Logical** - Features that build conceptually on others. For example, User profile editing requires user registration, Password reset requires user authentication,Advanced search requires basic search
* **Data** - Tasks that require specific data or state to exist. For example, User dashboard requires user data, Reporting features require transaction data, or Admin features require user roles

**Circular Dependencies**

In some situations you might encounter a situation where you have a circular dependency. For example, you might have a User service that depends on an Auth service, but that Auth service itself depends on the User service. Three strategies that can help:

**Interface extraction**

```
- [ ] 1.1 Create IUserService and IAuthService interfaces
- [ ] 1.2 Implement UserService using IAuthService interface
- [ ] 1.3 Implement AuthService using IUserService interface
- [ ] 1.4 Wire up dependency injection

```

**Layered approach**

```
- [ ] 1.1 Create User data model and basic CRUD
- [ ] 1.2 Create Auth service using User CRUD
- [ ] 1.3 Enhance User service with Auth integration

```

**Decoupling**

```
- [ ] 1.1 Create event system for user/auth communication
- [ ] 1.2 Implement User service with event publishing
- [ ] 1.3 Implement Auth service with event listening

```

---

### Good practices

So you have now had a chance to review your tasks.md file. Here are some final thoughts and good practices to consider.

* **Detail** - Ensure that you have written tasks with the right level of detail and clarity (clear specific objective)
* **Scope** - Set the appropriate scope for a task – should be completed with 1-4 hours of focused work, produces working, testable code, has a clear completion criteria, and builds incrementally
* **Traceability** - Always include references to specific requirements being implemented, to provide a clear connection between task and user value

---

### Preparing for implementation

You are now ready for your AI coding assistant (in our case, Kiro) to start generating code. Before you do this, a final checklist you should review:

* **Foundation** - After reviewing your tasks, make sure you have built the foundation first (Kiro does a good job at doing this in most cases)
* **Context preparation** - After reviewing the tasks, do you have the appropriate context to support code generation (agent steering files)
* **Check dependencies** - Review and check your task dependencies and order – follow dependencies to make sure they flow correctly

If you have updated/changed your tasks.md, again its important to let your AI coding assistant know, so submit a prompt like:

"I have updated the tasks.md - please reload"

We are now ready to kick off the code generation.

---

### Implementation - Code Generation

You now have a set of tasks (and potentially sub tasks), and each task is a unit of work, or code generation. Tasks are numbers logically, with sub tasks marked with a decimal point (i.e. 1. Task 1, 1.1 Sub task of 1, 1.2 Sub task of 1, 2 Task 2).

Kiro provides a simple way to start and review tasks. If you look at your tasks.md, you will notice "Start Task" appears above the task block to be completed. If you have sub tasks, each block will have its own "Start Task" link.

Starting at the very first task, when you click on "Start Task" Kiro will work through the task details and start generating code. It will work through each item in the task until it has completed. You can follow progress by monitoring the chat window, where all output will be displayed.

> **Heads up!** As and when needed, Kiro will also use the terminal to run commands. You will see the terminal pop up, and it will be called "Kiro" (vs zsh or bash which would be more normal for VSCode users)

Whilst you can use the UI to start a task, you can also use the chat interface. For example you can use"

"Start task 1.2"

You can also ask it to complete all tasks and subtasks. For example, I can use the following prompt:

"Start tasks 1.1 and 1.2"

And Kiro will start completing these tasks in sequence. You can also use something like:

"Start tasks 3 and 4"

And Kiro will work through all tasks and sub tasks, reporting back through the chat interface.

**Pay attention!**

Kiro uses agentic AI to generate code. As such, by default its permissions will be limited (i.e. it will not have write access to your system). Therefore, as and when it needs to do certain things (create directories, use MCP Tools, etc), you will be prompted by Kiro to confirm. Pay attention, otherwise you might have Kiro waiting and doing nothing until you respond.

You will see this in action when you start the labs later.

---

#### Completed Tasks

Once a task has been completed, the tasks.md will be updated to reflect this, and "Start Task" will be replaced by "Task Completed". There will also be two other links:

* **View Changes** - this will show you the code that was generated, in diff format. It will aggregate all the code changes, so this can get quite large depending on the task it is working on
* **View Execution** - this will go back to the chat interface and take you back to the output of Kiro as it was generating the code, which can be useful to trace what it did. If it encountered issues or did something strange, you will catch those by looking at this.

In addition to this, the chat interface should provide a detailed summary of what was achieved during the task completion. Pay attention to this and make sure it correlates with what the tasks objective was. Here is an example of what these look like.

![completed task summary](/images/task-summary.png)

---

#### Progressing through tasks

Kiro will work through each task as and when prompted. You might be wondering why it does not just start working through all the tasks, or why there isn't a "Complete all tasks" button. This is by design, as you should be reviewing and checking progress (review) after each task has been completed. Completing all tasks would make this a more significant challenge. 

If you REALLY wanted to do this, use the chat interface and use something like "Execute all tasks in the spec".

---

#### What happens when things go wrong!

Occasionally you might encounter a problem - maybe your computer crashes, the network goes down, or Kiro just fails to respond. Don't panic. After you have recovered the issue, when you restart Kiro, it should detect the status of any in-flight tasks. You will see that there is a "retry" link that you can now use to re-do the task that had been interrupted. Kiro will take care of picking up context from where it was and completing the task.

![Kiro retry](/images/kiro-task-fail-retry.png)

---

#### Completing all your tasks

Once all tasks have been completed, you will get a final summary within the chat interface.

We have walked you through at a high level the workflow steps of a typical iteration of a spec. These things of course do not live in isolation - we need to do many of them, or perhaps we need to update/change them. Lets look at the lifecycle of specs next.

---

## The spec driven development lifecycle

*Spec driven development is still emerging and so areas such as the spec driven development lifecycle are still evolving - bear that in mind as we explore the current approach to this*

In the previous sections we looked at the process of creating a new spec, and followed it through the three step workflow of requirements, design, and implementation (tasks). What if we wanted to change something though? Specs are living documents that track what was/is built. In this section we look at the typical lifecycle of specs, and how we manage change.

![The SDD lifecycle](/images/sdd-lifecycle-detailed.png)

---

### Change scenarios

There are a number of scenarios where you might need or want to make changes to your specs. Each scenario will require you to approach it in slightly different ways. Lets dive into this.

**Clarification**

Minor updates that do not functionally change design or implementation but might help improve precision. Some examples of this include fixing typos, formatting improvements, clearer wording.

For these kinds of trivial changes, you and adjust/amend the documents directly as they will not impact any downstream workflow changes. The exception perhaps being where those typos are reflect in artifacts that are built (e.g you wanted to create a page called "Help" but created a typo called "Welp" and now you want to change that back - this would require you to kick off a workflow refresh which we will come to in a bit)

**Discoveries**

During the implementation phase you might discover implementation details (tech) that lead to changes in design. This is part of the development process, and you will likely be able to recall your own examples of where you started off with a design, and then ran into issues or limitations during implementation. Examples of these kinds of changes might include:

* **Technical constraints** - During code generation you identified sub optimization choices: limitations with libraries or APIs, performance issues, security concerns
* **Integration challenges** - Data or interface format issues, complexities with authentication and authorization, new/updated interfaces
* **Feedback** - Testing or user feedback, which includes accessibility, mobile support, responsiveness, browser compatibility and more

For these kinds of changes we would update the design.md, and then kick off an update which we will come to in a moment.

**Changes**

Probably the most straightforward change is where you want to update an existing spec (maybe add or update a requirement).

For these kinds of changes we would need to implement a full refresh of the lifecycle, which depending on what was asked, could lead to working through the workflow steps again. We will look at this during the labs.

---

### Change History

You might find it useful to create a new artifact within your report to track changes. For example, I create a new file called changelog.md which looks like the following:

```
# Change History

1.0.0 - First version of this doc
1.0.1 - Update doc to remove the "Contact Us" feature
```

I then use a feature of Kiro to automate the tracking of changes through something called an Agent Hook. This makes it easy for me to keep a tracking change in a separate document of what changes are being made.

This is what my Agent Hook looks like:

![Agent Hook to update the changelog.md](/images/kiro-agent-hook.png)

when you make subsequent changes you will find that Kiro updates these.

```
# Change History

1.0.0 - First version of this doc
1.0.1 - Update doc to remove the "Contact Us" feature
1.0.2 - Add back "Contact Us" feature with email address requirement
```

---

### Versioning

As you work with specs, you will need to implement a versioning strategy that helps you track updates and changes across both your specs and your code. The simplest way to do this is to version control your entire project workspace. This will enable ou to use Git to track changes and push commits atomically for the workflow steps (you can keep task implementation as separate commits).

You should think about what version control strategy makes sense when you are working with specs. For example, do you want to create branches for each spec and then merge in later, or does a simpler workflow work?

#### Deleting a specification

A good version control strategy is important when it comes to deleting a spec. So far we have looked at creating and modifying specs, but you might be wondering what happens if I create a spec within my project and I now want to delete it. In this instance, you will need to fall back on your version control, and ensure you create a version control strategy that allows you to atomically revert back.

---

### Good practices

Good practices for managing specs are still emerging but we are beginning to see a few things you can do that will help you stay in control:

* Version control artifacts so you can manage changes
* Create a version control strategy that allows you to manage changes at a spec level
* Create a changelog to track changes in your project, and automate these using your AI Coding Tool (for example, Agent Hooks)

---

Click on [New Projects](/workshop/03-greenfield.md) to proceed with building the simple todo web application

Click on [Home](/README.md) to go back to the landing page


---

# Additional reading material

* [Kiro Blog](https://kiro.dev/blog/from-chat-to-specs-deep-dive/) - a deeper dive into how we got to SDD
* [Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) - a methodology and tooling perspective of SDD
* [Advanced Development with Amazon Q Developer](https://catalog.workshops.aws/qadvanced/en-US?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el) - a workshop that looks at how you can apply SDD using Amazon Q Developer
* [Kiro Steering files](https://kiro.dev/docs/steering/) - official documentation for Kiro steering files