![Header - picture of Kiro ghost and title](/images/header.png)

# Tools and Resources

In this section you will explore some of Kiro's capabilities that are not specific to spec driven development, but will help you as you using Kiro to work on writing code.

## Kiro features

Kiro features some neat features that are very handy as you being to work with spec driven development.

### Agent Hooks

A really neat feature of Kiro is Agent Hooks. This allows you to create agents that run automatically on certain events (currently File Save, File Create, and File Delete). You can also create these and then trigger them manually too.

From the Kiro activity bar, will see the Agent Hook panel. Clicking on the "+" starts the process of creating an Agent Hook. A panel will appear where you enter as a prompt, what you want your hook to do. After entering your prompt Kiro will start the process of creating your agent hook. You will see output on the chat interface.

Once created you will see the agent hook screen where you define and configure your agent hook.

![The agent hook creation screen](/images/kiro-agent-hook-create.png)

We can see that each hook has a title and description (the title is how it will appear in the agent hook panel on the Kiro activity bar). You can then configure when this agent hook is triggered (in this example, it is when I file is created) as well as which files and directories you want to monitor. Finally the instruction (or prompt) that Kiro will fire off when this agent hook is triggered.

You can see that at any time we can disable/enable hooks by toggling the switch at the top of the screen. And if we want to, we can also delete this agent hook using the delete option. Agent hooks themselves are just json configuration files that will appear in the ".kiro/hooks" directory of your project workspace.

You can track when an agent hook will trigger by monitoring the Kiro task queue. When Kiro is working through a task (in implementation phase), you might be wondering why the agent hook is not running or being triggered (based on whatever you asked it to do, so in this example add copyright headers on newly created files). This is because the current task is running in the queue, and the agent hook will be queued after. Once the task has completed, the agent hook will fire and execute whatever is needed (in the example above, adding copyright headers to any newly created files).

---

### Powers

Powers give your AI agent instant access to specialized knowledge for any technology. Powers package your tools, workflows, and best practices into a format that Kiro can activate on-demand. When you mention relevant keywords, Kiro loads the power's context and tools automatically. They help address some of the context window challenges that working with AI coding agents brings, helping to reduce context overload and provide the right context just when its needed.

Powers are just a set of assets that you bundle together in a directory, which Kiro will recognize and provide the supporting integration into the Kiro IDE. A POWER.md file is created which provides a specialized steering file that combines information, as well as optional details about MCP servers that might be needed or Agent Hooks that are configured. The POWER.md file also provides details to Kiro on how it should be invoked (what keywords to watch out for). What makes this so useful is that you can bundle everything you need as a Power, and Kiro will load and then unload as needed during your working sessions, helping you to optimize how the context window is managed.

Installing Powers is super easy - there is a new Kiro Powers icon on the navigation bar which is where you will see available Powers you can use. Installing them is as simple as a few clicks and you are good to go.

![Installing Kiro Powers](/images/kiro-power-1.png)

After you have installed a Power, you will see it appear in the list of available Powers. Clicking on any Power will show you how you can update/remove or just try it out in the chat interface.

![Installed Powers](/images/kiro-power-2.png)

 There are already many Powers available that you can use, and you can create your own easily. Creating Powers is outside the scope of this workshop, but you can find out more by checking out the [Powers](https://kiro.dev/docs/powers/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el) details on the Kiro website.

---

## Providing context

Kiro provides a wide array of sources for you to provide context. These are accessible when you hit the "#" character in the chat interface. This will bring up a menu option which lists all of the available sources. These include output from the terminal, git diffs, steering documents, specs and more.

If when you attempt to use "#" and reference a steering or spec and they are not listed, you might need to force a re-index - see next, Codebase indexing.

---

## Codebase Indexing

During the labs we forced Kiro to re-index the docs so that we just created. Whilst Kiro automatically indexes your codebase and documentation to provide intelligent code suggestions, navigation, and context-aware assistance, sometimes you might need to re-index.

To force a re-index, use COMMAND + SHIFT + P (Mac) or CTRL + SHIFT + P to access Kiro's command palette and then type in Index to the search bar to view the available indexing options.

You can read more in the official documentation pages, [Codebase Indexing](https://kiro.dev/docs/editor/codebase-indexing/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el)

---

## Choosing the right model

Kiro provides a number of different AI agent options to handle your development tasks, and these will change over time. As a developer you can either explicitly set a model you want to use (for example, Claude Sonnet 4.0, Claude Sonnet 4.5, etc) or you can set this to Auto.

Auto is Kiro's default intelligent model router that combines multiple frontier models with advanced optimization techniques. Auto uses best in class LLM models (Claude Sonnet 4 and alike) to provide you the best quality for the type of tasks assigned to the agent.

You configure the model via the pull down option in the chat interface. Auto is selected by default, but when you click on that it will bring up a menu as to which models are available.

**Credits**

You will notice when you bring up the available models that there is "credit" associated with each model. Your Kiro usage is tied to your service tier you have subscribed to (Kiro free, Kiro Pro, Kiro Pro+, and Kiro Power) therefore this is a consideration you should take when selecting a given model for work. You can dive deeper into this by reading the [Billing page](https://kiro.dev/docs/billing/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el).

Switching to cheaper models or more expensive models based on the tasks you are running is something that you will start to get an intuition for. 

There are some great resources to help you think about which models to use. Start off by reading the section on [Model Selection from the official Kiro docs](https://kiro.dev/docs/chat/model-selection/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el) and then read this blog post, [Making your Kiro credits go further](https://kiro.dev/blog/making-credits-go-further/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el) to dive deeper.

---

## Keyboard shortcuts

Kiro IDE provides a wide range of keyboard shortcuts to help you work efficiently. You can view these on the official [Kiro documentation pages here](https://kiro.dev/docs/editor/keyboard-shortcuts/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el)

---

## Kiro settings

Kiro has a number of settings that allow you to customize it to your preferences. In this section we look at some of the more interesting options available to you.

### Agent Autonomy

Agent Autonomy can be configured both in settings, but is also present in the chat interface (the toggle option labeled Autopilot). There are two settings: Autopilot and Supervised.

* Autopilot mode is Kiro's autonomous execution mode that allows the agent to make code changes across your codebase and complete complex tasks with minimal intervention. It's a key feature that enables Kiro to work more independently on your behalf.
* Supervised mode applies each proposed change and then presents it for your review. You can accept, reject, or request further adjustments to any changes made. This approach gives you full visibility into each modification and lets you guide the development process to maintain code quality standards.

To understand how these work in more detail, and when you might want to use one mode over another, read the [Autopilot](https://kiro.dev/docs/chat/autopilot/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el) documentation page.

### Model Context Protocol (MCP)

You can disable MCP Servers from the settings. There are two options: Enabled and Disabled, with the default being Enabled.

### Trusted Commands

You can define a list of commands you are happy for Kiro to run without prompting you. These are defined within this property in the settings file.

You can manually add these, or as you are using Kiro, as a command is being run, you can add it to the trusted list. You can use wild cards to open up a broader range of commands, or be explicit as you want.

**Warning!**

It goes without saying, you should never trust destructive commands, so be careful if you define wild cards that might allow those commands to run.

### Agent Notification

When Kiro starts generating code to complete a task, you might start working on other tasks and move Kiro to the background. What happens if Kiro then needs your attention? What if there is an issue that stops its progress? This is where Agent Notifications are used, providing you with notifications using your operating systems level notifications to warn you that it needs your attention!

### Autocomplete

If you have used AI Coding Assistants when writing code, you might have found autocomplete helpful. This is where Kiro will provide blocks of code based on what you are typing.

This is **disabled** by default in Kiro, but can be enabled via Settings, or by clicking on the Autocomplete link in the bottom status bar.

---

## Kiroignore

You can create a file in your project workspace that prevents Kiro from reading specific files in your workspace. Using familiar gitignore syntax, you define patterns for files that should remain private—credentials, secrets, or content you prefer to keep out of agent context.

You create a **".kiroignore"** in the root directory of your project workspace, and then add items as you would a .gitignore file.

Read more about some of the additional configuration options [here](https://kiro.dev/docs/editor/kiroignore/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el)

---

## Source Control and Checkpoints

As you generate code using Kiro, there will be times when you need to undo changes that have been made. Making sure that you have initialized the project directory to use version control (for example, git init) should be something you think about. Using Kiro, you have multiple ways of managing the state of files in your project workspace.

### Source Control

Kiro's Source Control view provides comprehensive Git integration with AI-enhanced features to streamline your version control workflow.

There are two nice features you get with Kiro.

1. Kiro can automatically generate useful commit messages based on the activity and changes that have been made.
2. You can include your current git changes in any chat conversation by typing #Git Diff which allows Kiro to see your staged and unstaged changes, making it easier to get contextual help with your modifications. 

Read the official [documentation on Source Control here](https://kiro.dev/docs/editor/source-control/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el)

### Checkpoints

In addition to providing a visual overview of your files version control, Kiro also provides something called Checkpoints. Each time you send a prompt to Kiro, it creates a “checkpoint”. Checkpoints appear as markers in your chat history. You can hit Restore on a checkpoint marker to rewind both your codebase and Kiro’s context back to that point in time. Any changes made to your codebase by Kiro after that checkpoint are reverted, and any context additions (chat interactions) after that point are discarded as well.

Checkpoints act as a safety net that enables you to confidently explore multiple approaches to a problem, try different models for a given task, recover from mistakes or misunderstandings by the agent, etc.

Checkpoints work by snapshotting the contents of a file each time the Kiro agent modifies it using one of its built-in file modification tools, and then restoring that snapshot when you revert to that checkpoint.

Note that Kiro does not track any changes to a file made outside of the Kiro agent. This means that if Kiro snapshots a file and then you, for example, manually edit that same file or run a code formatting tool on it, when you revert to that checkpoint, your changes will be lost. Kiro also does not track file changes made by any MCP tools or bash commands that it may run as part of its execution.

### Reverting changes

Reverts are similar to checkpoints, but differ in two key aspects. First, reverts only undo changes made by the latest turn of the agent, whereas checkpoints can undo changes made over multiple turns. Second, reverts only revert file changes, whereas checkpoints undo file changes as well as discard context additions past the checkpoint.



---

Click on [Home](/README.md) to go back to the landing page

---

# Additional reading material

* [Official Kiro docs](https://kiro.dev/docs/?trk=fd6bb27a-13b0-4286-8269-c7b1cfaa29f0&sc_channel=el)