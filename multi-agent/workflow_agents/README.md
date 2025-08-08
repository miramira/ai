# Workflow Agents

Parent to sub-agent transfers are ideal when you have multiple specialist sub-agents, and you want the user to interact with each of them.

However, if you would like agents to act one-after-another without waiting for a turn from the user, you can use **workflow agents**. Some example scenarios when you might use workflow agents include when you would like your agents to:

* **Plan and Execute:** When you want to have one agent prepare a list of items, and then have other agents use that list to perform follow-up tasks, for example writing sections of a document
* **Research and Write:** When you want to have one agent call functions to collect contextual information from Google Search or other data sources, then another agent use that information to produce some output.
* **Draft and Revise:** When you want to have one agent prepare a draft of a document, and then have other agents check the work and iterate on it

To accomplish these kinds of tasks, workflow agents have sub-agents and guarantee that each of their sub-agents acts. Agent Development Kit provides three built-in workflow agents and the opportunity to define your own:

* `SequentialAgent`
* `LoopAgent`
* `ParallelAgent`

Throughout the rest of this lab, you will build a multi-agent system that uses multiple LLM agents, workflow agents, and tools to help control the flow of the agent.

Specifically, you will build an agent that will develop a pitch document for a new hit movie: a biographical film based on the life of a historical character. Your sub-agents will handle the research, an iterative writing loop with a screenwriter and a critic, and finally some additional sub-agents will help brainstorm casting ideas and use historical box office data to make some predictions about box office results.

In the end, your multi-agent system will look like this (you can click on the image to see it larger):

# Sequential Agents


## Begin building a multi-agent system with a SequentialAgent

The `SequentialAgent` executes its sub-agents in a linear sequence. Each `sub-agent` in its sub_agents list is run, one after the other, in the order they are defined.

This is ideal for workflows where tasks must be performed in a specific order, and the output of one task serves as the input for the next.

In this task, you will run a `SequentialAgent`` to build a first version of your movie pitch-development multi-agent system. The first draft of your agent will be structured like this:

![](/images/sequentialAgent.png)

* A `root_agent` named `greeter` to welcome the user and request a historical character as a movie subject

* A SequentialAgent called `film_concept_team` will include:

    * A `researcher` to learn more about the requested historical figure from Wikipedia, using a LangChain tool covered in the lab Empower ADK agents with tools. An agent can choose to call its tool(s) multiple times in succession, so the researcher can take multiple turns in a row if it determines it needs to do more research.
    * A `screenwriter` to turn the research into a plot outline.
    * A `file_writer` to title the resulting movie and write the results of the sequence to a file.

## Add a LoopAgent for iterative work

The `LoopAgent` executes its sub-agents in a defined sequence and then starts at the beginning of the sequence again without breaking for a user input. It repeats the loop until a number of iterations has been reached or a call to exit the loop has been made by one of its sub-agents (usually by calling a built-in `exit_loop` tool).

This is beneficial for tasks that require continuous refinement, monitoring, or cyclical workflows. Examples include:

* **Iterative Refinement:** Continuously improve a document or plan through repeated agent cycles.
* **Continuous Monitoring:** Periodically check data sources or conditions using a sequence of agents.
* **Debate or Negotiation:** Simulate iterative discussions between agents to reach a better outcome.
You will add a `LoopAgent` to your movie pitch agent to allow multiple rounds of research and iteration while crafting the story. In addition to refining the script, this allows a user to start with a less specific input: instead of suggesting a specific historical figure, they might only know they want a story about an ancient doctor, and a research-and-writing iteration loop will allow the agents to find a good candidate, then work on the story.


![](/images/loopAgent.png)



