# Multi-Agent Systems

Instead of writing long, complex prompts that may not deliver results reliably, you can construct a flow of multiple, simple agents that can collaborate on complex problems by dividing tasks and responsibilities.

This architectural approach offers several key advantages such as:

* Easier to design: You can think in terms of agents with specific jobs and skills.
* Specialized functions with more reliable performance: Specialized agents can learn from clear examples to become more reliable at their specific tasks.
* Organization: Dividing the workflow into distinct agents allows for a more organized, and therefor easier to think about, approach.
* Improvability and maintainability: It is easier to improve or fix a specialized component rather than make changes to a complex agent that may fix one behavior but might impact others.
* Modularity: Distinct agents from one workflow can be easily copied and included in other similar workflows.

# The Hierarchical Agent Tree
![](/images/agent_tree.png "This is a sample image.")

 This helps limit the options for transfers for each agent in the tree, making it easier to control and predict the possible routes the conversation can take through the tree. Benefits of the hierarchical structure include:

* It draws **inspiration from real-world collaborative teams**, making it easier to design and reason about the behavior of the multi-agent system.
* It is **intuitive for developers**, as it mirrors common software development patterns.
* It provides **greater control over the flow** of information and task delegation within the system, making it easier to understand possible pathways and debug the system. For example, if a system has two report-generation agents at different parts of its flow with similar descriptions, the tree structure makes it easier to ensure that the correct one is invoked.

The structure always begins with the agent defined in the **root_agent** variable (although it may have a different user-facing **name** to identify itself). The root_agent may act as a **parent** to one or more **sub-agents**. Each sub-agent agent may have its own sub-agents.

# Explore transfers between parent, sub-agent, and peer agents

The conversation always begins with the agent defined as the **root_agent** variable.

The default behavior of a parent agent is to understand the **description** of each sub-agent and determine if control of the conversation should be transferred to a sub-agent at any point.

You can help guide those transfers in the parent's instruction by referring to the sub-agents by name (the values of their name parameter, not their variable names). Try an example:


## Three agents here:

* a **root_agent** named steering (its name is used to identify it in ADK's dev UI and command line interfaces). It asks the user a question (if they know where they'd like to travel or if they need some help deciding), and the user's response to that question will help this steering agent know which of its two sub-agents to steer the conversation towards. Notice that it only has a simple instruction that does not mention the sub-agents, but it is aware of its sub-agents' descriptions.
* a **travel_brainstormer** that helps the user brainstorm destinations if they don't know where they would like to visit.
* an **attractions_planner** that helps the user build a list of things to do once they know which country they would like to visit.


